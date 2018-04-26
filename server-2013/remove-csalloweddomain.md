---
title: Remove-CsAllowedDomain
TOCTitle: Remove-CsAllowedDomain
ms:assetid: d38afb34-627e-4772-990c-4f6676c54000
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398913(v=OCS.15)
ms:contentKeyID: 49302076
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAllowedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un dominio dall'elenco di domini approvati per la federazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsAllowedDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 rimuove il dominio fabrikam.com dall'elenco dei domini consentiti.

    Remove-CsAllowedDomain -Identity fabrikam.com

## ESEMPIO 2

Nell'esempio 2 tutti i domini con il valore stringa "fabrikam" all'interno del valore del parametro Identity vengono rimossi dall'elenco dei domini consentiti. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsAllowedDomain** e il parametro Filter per restituire una raccolta di domini con il valore stringa "fabrikam" all'interno del valore del parametro Identity, l'unica proprietà in base alla quale è possibile applicare il filtro. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAllowedDomain** che, a sua volta, rimuove dall'elenco dei domini consentiti tutti gli elementi presenti nella raccolta filtrata.

    Get-CsAllowedDomain -Filter *fabrikam* | Remove-CsAllowedDomain

## ESEMPIO 3

Nell'esempio 3 vengono rimossi tutti i domini senza un server proxy identificato dall'elenco dei domini consentiti. Per eseguire questa attività, viene chiamato il cmdlet **Get-CsAllowedDomain** per restituire una raccolta di tutti i domini attualmente presenti nell'elenco dei domini consentiti. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini con proprietà ProxyFqdn uguale a un valore Null. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAllowedDomain**, che rimuove dall'elenco dei domini consentiti ogni dominio presente nella raccolta.

    Get-CsAllowedDomain | Where-Object {$_.ProxyFqdn -eq $Null} | Remove-CsAllowedDomain 

## ESEMPIO 4

Nell'esempio 4 vengono rimossi dall'elenco dei domini consentiti tutti i domini in cui il campo Comment contiene il valore stringa "Ken Myer". A tale scopo nel comando viene innanzitutto utilizzato il cmdlet **Get-CsAllowedDomain** per recuperare una raccolta di tutti i domini presenti attualmente nell'elenco dei domini consentiti. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini con proprietà Comment contenente il valore stringa "Ken Myer". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAllowedDomain**, che rimuove dall'elenco dei domini consentiti ogni elemento presente nella raccolta.

    Get-CsAllowedDomain | Where-Object {$_.Comment -match "Ken Myer"} | Remove-CsAllowedDomain 

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Una volta stabilita una federazione, gli utenti delle due organizzazioni possono scambiare messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare comunque tra loro utilizzando le applicazioni SIP, ad esempio Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

L'impostazione di una federazione diretta con altre organizzazioni richiede diverse attività. Per iniziare, è necessario configurare i server che eseguono il servizio Access Edge di Lync Server in modo da consentire la federazione. Inoltre, anche l'altra organizzazione deve abilitare la federazione; non è possibile stabilire una federazione, a meno che entrambe le parti non siano concordi nell'impostare una relazione.

Per stabilire una relazione federata, potrebbe inoltre essere necessario gestire due elenchi correlati alla federazione: l'elenco consentito e l'elenco bloccato. L'elenco dei domini consentiti rappresenta le organizzazioni con cui si è scelto di stabilire una relazione federata. Se un dominio è presente nell'elenco dei domini consentiti, a seconda delle impostazioni di configurazione gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che dispongono di account in tale dominio federato. L'elenco dei domini bloccati invece rappresenta i domini con i quali è espressamente vietato agli utenti di stabilire una federazione. I messaggi provenienti da un dominio bloccato ad esempio verranno automaticamente rifiutati da Lync Server.

Se si desidera interrompere una relazione di federazione, è possibile utilizzare il cmdlet **Remove-CsAllowedDomain** per rimuovere il dominio appropriato dall'elenco dei domini consentiti e quindi, se opportuno, utilizzare il cmdlet **New-CsBlockedDomain** per aggiungerlo all'elenco dei domini bloccati. Si noti che un dominio non può essere presente contemporaneamente in un elenco di domini consentiti e in un elenco di domini bloccati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsAllowedDomain** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAllowedDomain"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio da rimuovere dall'elenco dei domini consentiti, ad esempio fabrikam.com. Non è possibile utilizzare i caratteri jolly per specificare il valore Identity di un dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain. Il cmdlet **Remove-CsAllowedDomain** accetta le istanze da pipeline dell'oggetto dominio consentito.

## Tipi restituiti

Elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsAllowedDomain](get-csalloweddomain.md)  
[New-CsAllowedDomain](new-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsAllowedDomain](set-csalloweddomain.md)

