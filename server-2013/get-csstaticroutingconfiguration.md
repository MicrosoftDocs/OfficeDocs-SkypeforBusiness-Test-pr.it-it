---
title: Get-CsStaticRoutingConfiguration
TOCTitle: Get-CsStaticRoutingConfiguration
ms:assetid: 94f126b4-b714-42ba-b9b6-81269634875f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398754(v=OCS.15)
ms:contentKeyID: 49301367
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsStaticRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione del routing statico utilizzate nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsStaticRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsStaticRoutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono restituite le informazioni su tutte le raccolte di configurazioni del routing statico in uso nell'organizzazione.

    Get-CsStaticRoutingConfiguration

## ESEMPIO 2

Con l'esempio 2 vengono restituite informazioni su una singola raccolta di configurazioni del routing statico, la raccolta con identità service:Registrar:atl-cs-001.litwareinc.com.

    Get-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com"

## ESEMPIO 3

Con l'esempio 3 viene utilizzato il parametro Filter per restituire informazioni sulle raccolte di configurazioni del routing statico assegnate nell'ambito del servizio. Il valore del filtro "service:\*" limita i dati restituiti alle raccolte con un'identità che inizia con il valore stringa "service:"

    Get-CsStaticRoutingConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni dettagliate sulle route per tutte le raccolte di configurazioni del routing statico in uso nell'organizzazione. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsStaticRoutingConfiguration** senza alcun parametro per restituire le informazioni complete per ogni raccolta di routing statico. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per "espandere" il valore della proprietà Route. Quando si espande una proprietà, tutti gli oggetti e i valori in essa contenuti vengono visualizzati in un modo facilmente leggibile.

    Get-CsStaticRoutingConfiguration | Select-Object -ExpandProperty Route

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce informazioni su tutte le route statiche configurate per soddisfare solamente URI (Uniform Resource Identifier) di telefoni. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsStaticRoutingConfiguration** senza alcun parametro per restituire tutte le raccolte di configurazioni del routing statico con le route associate. La raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che utilizza ExpandProperty per espandere tutti gli oggetti archiviati nella proprietà Route. Questi oggetti route vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo le route la cui proprietà MatchOnlyPhoneUri è uguale a True.

    Get-CsStaticRoutingConfiguration | Select-Object -ExpandProperty Route | Where-Object {$_.MatchOnlyPhoneUri -eq $True}

## Descrizione dettagliata

Quando si invia un messaggio SIP, il messaggio potrebbe dover attraversare molteplici subnet e reti prima di essere recapitato; il percorso seguito dal messaggio è spesso definito route. Nelle reti esistono due tipi di route: dinamiche e statiche. Con il routing dinamico, i server utilizzano algoritmi per determinare la posizione successiva (vale a dire l'hop successivo) a cui dovrebbe essere inoltrato un messaggio. Con il routing statico, i percorsi seguiti dai messaggi sono determinati anticipatamente dagli amministratori di sistema. Quando riceve un messaggio, il server controlla l'indirizzo del messaggio e inoltra il messaggio stesso al server dell'hop successivo configurato anticipatamente da un amministratore. Se la configurazione è corretta, le route statiche aiutano a garantire un recapito tempestivo e accurato dei messaggi, applicando un sovraccarico minimo sui server. Lo svantaggio delle route statiche è dovuto al fatto che i messaggi non vengono reinstradati in modo dinamico se si verifica un errore di rete.

Quando si installa Lync Server, viene creata automaticamente una raccolta globale di route statiche. La raccolta viene creata, ma non le vengono assegnate route. Il software inoltre consente di creare raccolte aggiuntive applicate all'ambito del servizio. Queste nuove raccolte possono essere assegnate esclusivamente al servizio di registrazione. Il cmdlet **Get-CsStaticRoutingConfiguration** consente di restituire informazioni su tutte le raccolte di configurazioni del routing statico in uso nell'organizzazione. È inclusa la possibilità di restituire informazioni dettagliate su ogni route assegnata a una raccolta.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsStaticRoutingConfiguration** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsStaticRoutingConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare la raccolta (o le raccolte) di configurazione del routing statico da restituire. Ad esempio, la sintassi riportata di seguito restituisce tutte le raccolte di routing statico configurate nell'ambito del servizio: -Filter &quot;service:*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta di configurazioni di routing statico. Per restituire informazioni sulla raccolta globale, utilizzare la seguente sintassi: -Identity global. Per recuperare informazioni su una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity. Tuttavia, se è necessario utilizzare caratteri jolly, utilizzare il parametro Filter.</p>
<p>Se non si include il parametro Identity o Filter, il cmdlet <strong>Get-CsStaticRoutingConfiguration</strong> restituisce informazioni su tutte le raccolte di configurazioni del routing statico.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione del routing statico dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsStaticRoutingConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsStaticRoutingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

