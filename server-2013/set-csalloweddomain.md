---
title: Set-CsAllowedDomain
TOCTitle: Set-CsAllowedDomain
ms:assetid: d5b25b66-2b11-40ef-9ea4-efcae0b610e6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398931(v=OCS.15)
ms:contentKeyID: 49302096
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAllowedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di uno o più domini inclusi nell'elenco dei domini approvati per la federazione. Dopo l'approvazione di un dominio per la federazione, ovvero l'aggiunta del dominio all'elenco dei domini consentiti, gli utenti possono scambiare messaggi istantanei e informazioni sulla presenza con persone che dispongono di account nel dominio federato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAllowedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsAllowedDomain [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MarkForMonitoring <$true | $false>] [-ProxyFqdn <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 modifica la proprietà Comment per il dominio consentito con "fabrikam.com" come valore per il parametro Identity. A tale scopo, viene incluso il parametro Comment con il valore di parametro appropriato: "Contact: Davide Garghentini (davidegarghentini@fabrikam.com)".

    Set-CsAllowedDomain -Identity fabrikam.com -Comment "Contact: Ken Myer (kenmyer@fabrikam.com)"

## ESEMPIO 2

Nell'esempio 2 vengono modificate le proprietà Comment e MarkForMonitoring di tutti i domini consentiti con il valore stringa "fabrikam" all'interno del parametro Identity. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsAllowedDomain** e il parametro Filter. Il valore di filtro "\*fabrikam\*" indica al cmdlet **Get-CsAllowedDomain** di restituire tutti i domini con valore Identity che include il valore stringa "fabrikam". Questo comando restituisce, ad esempio, i domini come fabrikam.com, us.fabrikam.net e fabrikam-users.org. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsAllowedDomain**, che modifica la proprietà Comment e imposta la proprietà MarkForMonitoring su True ($True) per ogni elemento della raccolta.

    Get-CsAllowedDomain -Filter *fabrikam* | Set-CsAllowedDomain -Comment "Contact: Ken Myer (kenmyer@fabrikam.com)" -MarkForMonitoring $True

## ESEMPIO 3

Il comando riportato nell'esempio 3 modifica tutti i domini presenti nell'elenco dei domini consentiti che non sono attualmente monitorati da Monitoring Server, ovvero tutti i domini con proprietà MarkForMonitoring impostata su False. A tale scopo, viene chiamato il cmdlet **Get-CsAllowedDomain** senza parametri aggiuntivi per recuperare una raccolta di tutti i domini presenti nell'elenco dei domini consentiti. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini con valore MarkForMonitoring uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsAllowedDomain**, che imposta la proprietà MarkForMonitoring per ogni dominio della raccolta su True.

    Get-CsAllowedDomain | Where-Object {$_.MarkForMonitoring -eq $False} | Set-CsAllowedDomain -MarkForMonitoring $True

## ESEMPIO 4

Nell'esempio 4 viene aggiunto un commento generico ("Need contact information.") a ogni dominio presente nell'elenco dei domini consentiti in cui la proprietà Comment non contiene attualmente alcun valore. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsAllowedDomain** per recuperare una raccolta di tutti i domini presenti nell'elenco dei domini consentiti. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona i domini con proprietà Comment uguale a Null. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsAllowedDomain**, che modifica la proprietà Comment di ogni elemento della raccolta.

    Get-CsAllowedDomain | Where-Object {$_.Comment -eq $Null} | Set-CsAllowedDomain -Comment "Need contact information."

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Una volta stabilita una federazione, gli utenti delle due organizzazioni possono scambiare messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare comunque tra loro utilizzando le applicazioni SIP, ad esempio Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

l'impostazione di una federazione diretta con altre organizzazioni richiede diverse attività. Per iniziare, è necessario configurare i server che eseguono il servizio Access Edge di Lync Server in modo da consentire la federazione. Inoltre, anche l'altra organizzazione deve abilitare la federazione; non è possibile stabilire una federazione, a meno che entrambe le parti non siano concordi nell'impostare una relazione.

Per stabilire una relazione federata, potrebbe inoltre essere necessario gestire due elenchi correlati alla federazione: l'elenco consentito e l'elenco bloccato. l'elenco dei domini consentiti rappresenta le organizzazioni con cui si è scelto di stabilire una relazione federata. Se un dominio è presente nell'elenco dei domini consentiti, a seconda delle impostazioni di configurazione gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con utenti che dispongono di account in tale dominio federato. l'elenco dei domini bloccati invece rappresenta i domini con i quali è espressamente vietato agli utenti di stabilire una federazione. I messaggi provenienti da un dominio bloccato ad esempio verranno automaticamente rifiutati da Lync Server.

Il cmdlet **Set-CsAllowedDomain** consente di modificare i valori delle proprietà di un domino presente nell'elenco dei domini consentiti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsAllowedDomain** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAllowedDomain"}

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
<td><p><em>Comment</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Valore stringa facoltativo che fornisce ulteriori informazioni sul dominio da modificare. È ad esempio possibile aggiungere un commento che fornisce le informazioni di contatto del dominio federato.</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio consentito di cui vengono modificati i valori delle proprietà, ad esempio</p>
<p>-Identity fabrikam.com</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto dominio bloccato</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MarkForMonitoring</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la connessione di federazione tra il dominio e il dominio remoto verrà monitorata da Monitoring Server. Per impostazione predefinita, MarkForMonitoring è impostato su False, ovvero la connessione non sarà monitorata.</p>
<p>Questa proprietà verrà ignorata se Monitoring Server non è stato distribuito.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (ad esempio proxy-server.fabrikam.com) del server proxy SIP distribuito nel dominio che deve essere aggiunto all'elenco dei domini consentiti. Questa proprietà è facoltativa. Se non viene specificata, verranno utilizzate le procedure di individuazione DNS SRV per determinare la posizione del server proxy SIP.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain. Il cmdlet **Set-CsAllowedDomain** accetta le istanze da pipeline dell'oggetto dominio consentito.

## Tipi restituiti

Il cmdlet **Set-CsAllowedDomain** non restituisce un valore o un oggetto. Il cmdlet configura piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsAllowedDomain](get-csalloweddomain.md)  
[New-CsAllowedDomain](new-csalloweddomain.md)  
[Remove-CsAllowedDomain](remove-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

