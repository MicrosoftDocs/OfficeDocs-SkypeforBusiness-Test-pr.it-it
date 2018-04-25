---
title: Get-CsBlockedDomain
TOCTitle: Get-CsBlockedDomain
ms:assetid: 5fa2c2a3-b5e4-430c-970a-0c506a6924b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398424(v=OCS.15)
ms:contentKeyID: 49300717
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBlockedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui domini inclusi nell'elenco dei domini bloccati per la federazione. Per definizione, agli utenti non è consentito utilizzare le applicazioni di Lync Server per comunicare con utenti del dominio bloccato. Gli utenti non possono utilizzare ad esempio Lync per scambiare messaggi istantanei con altri utenti con account SIP (Session Initiation Protocol) in un dominio incluso nell'elenco dei domini bloccati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsBlockedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsBlockedDomain [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce una raccolta di tutti i domini presenti nell'elenco dei domini bloccati. A tale scopo, viene chiamato il cmdlet **Get-CsBlockedDomain** senza alcun parametro aggiuntivo.

    Get-CsBlockedDomain

## ESEMPIO 2

Nell'Esempio 2 l'unico dominio bloccato restituito è quello con l'identità "fabrikam.com". Dal momento che i domini nell'elenco dei domini bloccati devono avere identità univoche, il comando restituirà al massimo un unico elemento.

    Get-CsBlockedDomain -Identity fabrikam.com

## ESEMPIO 3

Nell'Esempio 3 viene utilizzato il parametro Filter per ottenere una raccolta di tutti i domini bloccati la cui identità termina con il valore ".net". Questo comando restituisce domini come northwindtraders.net, contoso.net e fabrikam.net.

    Get-CsBlockedDomain -Filter *.net

## ESEMPIO 4

Nell'esempio 4 viene restituita una raccolta di tutti i domini in cui la proprietà Comment non presenta valori. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsBlockedDomain** per restituire una raccolta di tutti i domini inclusi nell'elenco dei domini bloccati. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini in cui la proprietà Comment è uguale a Null.

    Get-CsBlockedDomain | Where-Object {$_.Comment -eq $Null}

## ESEMPIO 5

Nell'esempio 5 vengono restituiti tutti i domini bloccati che includono il valore stringa "Ken Myer" nella proprietà Comment. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsBlockedDomain** per ottenere una raccolta di tutti i domini nell'elenco dei domini bloccati. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona i domini in cui la proprietà Comment include il valore stringa "Ken Myer".

    Get-CsBlockedDomain | Where-Object {$_.Comment -match "Ken Myer"}

## Descrizione dettagliata

La federazione consente a due organizzazioni di instaurare una relazione di trust che facilita la comunicazione tra i due gruppi. Quando viene stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare in altri modi tra loro utilizzando applicazioni SIP come Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

La configurazione di una federazione con un'altra organizzazione implica diverse attività. Per iniziare, è necessario configurare il servizio Access Edge di Lync Server per consentire la federazione. Inoltre, l'altra organizzazione deve a sua volta abilitare il processo federativo; la federazione non può essere instaurata se entrambe le parti non sono d'accordo.

Per impostare una relazione federata potrebbe inoltre essere necessario gestire due elenchi relativi alla federazione: l'elenco dei domini consentiti e quello dei domini bloccati. L'elenco dei domini consentiti rappresenta l'organizzazione con la quale si è scelto di attuare la federazione. Se un dominio è incluso in questo elenco, gli utenti, subordinatamente alle impostazioni di configurazione, saranno in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti il cui account è incluso nel dominio federato. Al contrario, l'elenco bloccato rappresenta i domini con i quali viene espressamente proibito agli utenti di attuare la federazione, ad esempio un messaggio inviato da un dominio bloccato viene automaticamente rifiutato da Lync Server.

Il cmdlet **Get-CsBlockedDomain** consente di ottenere le informazioni sui domini che fanno parte dell'elenco dei domini bloccati.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsBlockedDomain** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBlockedDomain"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per ottenere uno o più domini dall'elenco dei domini bloccati. Per ottenere tutti i domini che hanno un'identità che inizia con la lettera &quot;r&quot;, utilizzare la seguente sintassi: -Filter r*. Per ottenere tutti i domini con un'identità che termina con &quot;.net&quot;, utilizzare la seguente sintassi: -Filter &quot;*.net&quot;. Per ottenere tutti i domini che hanno un'identità che inizia con la lettera &quot;f&quot; o la lettera &quot;g&quot;, utilizzare la seguente sintassi: -Filter [fg]*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome del dominio da ottenere. Nell'elenco dei domini bloccati, i domini sono riportati con il loro nome completo (FQDN); pertanto, l'identità di un dominio potrebbe essere simile a fabrikam.com o contoso.net e non è possibile utilizzare i caratteri jolly per specificarla. Per utilizzare i caratteri jolly per ottenere un determinato dominio o gruppo di domini è necessario utilizzare il parametro Filter.</p>
<p>Se questo parametro non viene specificato, verranno restituiti tutti i domini inclusi nell'elenco dei domini bloccati.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei domini bloccati dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsBlockedDomain** non accetta input da pipeline.

## Tipi restituiti

Restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain.

## Vedere anche

#### Ulteriori risorse

[New-CsBlockedDomain](new-csblockeddomain.md)  
[Remove-CsBlockedDomain](remove-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsBlockedDomain](set-csblockeddomain.md)

