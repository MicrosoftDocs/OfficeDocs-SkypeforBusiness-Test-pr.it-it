---
title: Set-CsMobilityPolicy
TOCTitle: Set-CsMobilityPolicy
ms:assetid: 660fcd74-24fc-496e-8aa0-1aadd9334ad3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690021(v=OCS.15)
ms:contentKeyID: 49300810
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMobilityPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio per dispositivi mobili esistente. I criteri per dispositivi mobili determinano se un utente può o meno utilizzare Lync Mobile. Questi criteri gestiscono inoltre la capacità di un utente di utilizzare la funzionalità Chiamata tramite ufficio, che consente agli utenti di effettuare e ricevere chiamate telefoniche sul cellulare utilizzando il numero dell'ufficio anziché quello del cellulare. I criteri per dispositivi mobili possono essere utilizzati inoltre per richiedere connessioni Wi-Fi quando si effettuano o si ricevono chiamate. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Set-CsMobilityPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMobilityPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCustomerExperienceImprovementProgram <$true | $false>] [-AllowExchangeConnectivity <$true | $false>] [-AllowSaveCallLogs <$true | $false>] [-AllowSaveCredentials <$true | $false>] [-AllowSaveIMHistory <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableIPAudioVideo <$true | $false>] [-EnableMobility <$true | $false>] [-EnableOutsideVoice <$true | $false>] [-Force <SwitchParameter>] [-RequireWIFIForIPAudio <$true | $false>] [-RequireWIFIForIPVideo <$true | $false>] [-RequireWiFiForSharing <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 la caratteristica Chiamata tramite ufficio viene disabilitata nel criterio per dispositivi mobili assegnato al sito Redmond. A tale scopo, la proprietà EnableOutsideVoice viene impostata su False.

    Set-CsMobilityPolicy -Identity "site:Redmond" -EnableOutsideVoice $False

## ESEMPIO 2

Il comando illustrato nell'esempio 2 consente di disabilitare la caratteristica Chiamata tramite ufficio per tutti i criteri per dispositivi mobili configurati nell'ambito per utente. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsMobilityPolicy** insieme al parametro Filter. Il valore di filtro "tag:\*" consente di limitare i dati restituiti ai criteri con un parametro Identity che inizia con il valore stringa "tag:". La raccolta filtrata di criteri viene quindi inviata tramite pipe al cmdlet **Set-CsMobilityPolicy**, che prende ogni criterio nella raccolta e imposta la proprietà EnableOutsideVoice su False.

    Get-CsMobilityPolicy -Filter "tag:*" | Set-CsMobilityPolicy -EnableOutsideVoice $False

## ESEMPIO 3

Nell'esempio 3 viene aggiunta una nuova descrizione alle proprietà dei criteri per dispositivi mobili per cui non è attualmente disponibile una descrizione. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsMobilityPolicy** per restituire una raccolta di tutti i criteri per dispositivi mobili attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo i criteri in cui la proprietà Description è uguale a (-eq) un valore Null. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsMobilityPolicy**, che imposta la proprietà Description per ogni criterio sul valore stringa "Policy owner: kenmyer@litwareinc.com".

    Get-CsMobilityPolicy | Where-Object {$_.Description -eq $Null} | Set-CsMobilityPolicy -Description "Policy owner: kenmyer@litwareinc.com"

## Descrizione dettagliata

Lync Mobile è un'applicazione client che consente agli utenti di eseguire Lync nei cellulari. La funzionalità Chiamata tramite ufficio consente agli utenti di effettuare chiamate con il cellulare che risultano provenire dal numero dell'ufficio anziché da quello del cellulare. Gli utenti abilitati per la funzionalità Chiamata tramite ufficio possono ottenere questo risultato componendo il numero direttamente dal cellulare oppure utilizzando l'opzione di conferenza telefonica con chiamata in uscita. Con questa opzione, un utente richiede al server dei servizi per dispositivi mobili Lync Server di effettuare una chiamata al suo posto. La chiamata viene configurata dal server e quindi l'utente viene richiamato sul cellulare. Dopo che l'utente ha risposto, il server compone il numero della parte chiamata. Entrambe queste funzionalità possono essere gestite utilizzando criteri per dispositivi mobili.

Con Lync Server 2013, i dispositivi mobili possono effettuare o ricevere chiamate tramite la rete cellulare standard oppure tramite connessioni Wi-Fi. I criteri per dispositivi mobili possono essere utilizzati per richiedere connessioni Wi-Fi e impedire le chiamate tramite la rete cellulare.

Questi criteri possono essere modificati in qualsiasi momento utilizzando il cmdlet **Set-CsMobilityPolicy**.

Per abilitare la funzionalità Chiamata tramite ufficio è necessario configurare due proprietà diverse. La prima, EnableOutsideVoice, determina se la funzionalità Chiamata tramite ufficio è abilitata. La seconda, EnableMobility, determina se gli utenti possono utilizzare Lync Mobile. Per consentire a un utente di utilizzare la funzionalità Chiamata tramite ufficio, entrambe queste proprietà devono essere impostate su True. Se EnableMobility è impostata su True ed EnableOutsideVoice è impostata su False, l'utente può eseguire Lync Mobile, ma non può utilizzare la funzionalità Chiamata tramite ufficio. Se EnableMobility è impostata su False ed EnableOutsideVoice è impostata su True, l'utente non può eseguire Lync Mobile e, di conseguenza, non può utilizzare la funzionalità Chiamata tramite ufficio, indipendentemente dal valore della proprietà EnableOutsideVoice.

Per utilizzare la caratteristica Chiamata tramite ufficio, gli utenti devono essere gestiti da criteri vocali che consentano lo squillo simultaneo.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsMobilityPolicy** in locale: RTCUniversalServerAdmins.

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
<td><p><em>AllowCustomerExperienceImprovementProgram</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti dei dispositivi mobili possono partecipare al programma Analisi utilizzo software.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExchangeConnectivity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono connettersi a Microsoft Exchange Server 2013 utilizzando un dispositivo mobile.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSaveCallLogs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono salvare un registro delle chiamate effettuate o ricevute da un dispositivo mobile.</p>
<p>Questa impostazione non si applica ai dispositivi Android.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSaveCredentials</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono salvare informazioni relative alle credenziali, ad esempio la password, su un dispositivo mobile. Tali informazioni potranno quindi essere applicate negli scenari di accesso automatico.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSaveIMHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono salvare trascrizioni di sessioni di conferenza e messaggistica istantanea su un dispositivo mobile.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo aggiuntivo da associare a un criterio per dispositivi mobili. Il parametro Description potrebbe ad esempio includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableIPAudioVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se viene impostato su False, questo parametro impedisce all'utente di effettuare chiamate VoIP (Voice over IP) utilizzando il dispositivo mobile. Il valore predefinito è True, ovvero le chiamate VoIP sono consentite.</p>
<p>Questo parametro è stato introdotto in Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMobility</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti sono autorizzati a utilizzare Lync Mobile.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOutsideVoice</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti sono autorizzati a utilizzare la caratteristica Chiamata tramite ufficio. Quando è impostato su False, gli utenti non possono utilizzare tale caratteristica.</p>
<p>Il valore predefinito è True.</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco assegnato al criterio al momento della creazione. I criteri per dispositivi mobili possono essere assegnati nell'ambito globale, del sito o per utente. Per fare riferimento all'istanza globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per fare riferimento ai criteri nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per fare riferimento a un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity RedmondMobilityPolicy</p>
<p>Se il parametro Identity non viene specificato, il cmdlet Set-CsMobilityPolicy modificherà il criterio globale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto Mobility</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireWIFIForIPAudio</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True, l'utente può utilizzare l'audio IP nelle chiamate effettuate quando il dispositivo mobile è connesso a una rete Wi-Fi. Ciò significa che l'utente potrà effettuare chiamate audio solo mediante Wi-Fi e non potrà utilizzare la rete standard del telefono cellulare. Il valore predefinito è False.</p>
<p>Questo parametro è stato introdotto in Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>RequireWIFIForIPVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True, l'utente può utilizzare il video IP nelle chiamate effettuate quando il dispositivo mobile è connesso a una rete Wi-Fi. Se il dispositivo mobile verrà spostato al di fuori della rete Wi-Fi, le videochiamate verranno ricevute solo come chiamate audio. Se la proprietà è impostata su False, l'utente può effettuare o ricevere videochiamate IP utilizzando la rete Wi-Fi oppure la connessione alla rete dati.</p>
<p>Questo parametro è stato introdotto in Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireWiFiForSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True, per partecipare a una sessione di condivisione applicazioni, gli utenti dei dispositivi mobili devono utilizzare una connessione Wi-Fi. Se è impostato su False (valore predefinito), gli utenti dei dispositivi mobili possono partecipare a una sessione di condivisione applicazioni mediante una connessione Wi-Fi o alla rete dati (3G/4G).</p>
<p>Se questo valore è impostato su True, gli utenti non potranno modificare le opzioni di configurazione della condivisione. Se è impostato su False, gli utenti potranno utilizzare la pagina Opzioni per modificare le impostazioni di configurazione della condivisione.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility. Il cmdlet **Set-CsMobilityPolicy** accetta istanze inviate tramite pipeline dell'oggetto Mobility.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsMobilityPolicy** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility.

