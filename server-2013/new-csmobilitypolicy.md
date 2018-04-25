---
title: New-CsMobilityPolicy
TOCTitle: New-CsMobilityPolicy
ms:assetid: 1fba8c3e-087d-4ba4-918b-371f8757df7c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh689987(v=OCS.15)
ms:contentKeyID: 49299893
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMobilityPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio per dispositivi mobili nell'ambito del sito o per utente. I criteri per dispositivi mobili determinano se un utente può o meno utilizzare Lync Mobile. Questi criteri gestiscono inoltre la capacità di un utente di utilizzare la funzionalità Chiamata tramite ufficio, che consente di effettuare e ricevere chiamate telefoniche sul cellulare utilizzando il numero dell'ufficio anziché quello del cellulare. I criteri per dispositivi mobili possono anche essere utilizzati per richiedere connessioni Wi-Fi quando si effettuano o ricevono chiamate. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    New-CsMobilityPolicy -Identity <XdsIdentity> [-AllowCustomerExperienceImprovementProgram <$true | $false>] [-AllowExchangeConnectivity <$true | $false>] [-AllowSaveCallLogs <$true | $false>] [-AllowSaveCredentials <$true | $false>] [-AllowSaveIMHistory <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableIPAudioVideo <$true | $false>] [-EnableMobility <$true | $false>] [-EnableOutsideVoice <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-RequireWIFIForIPAudio <$true | $false>] [-RequireWIFIForIPVideo <$true | $false>] [-RequireWiFiForSharing <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di creare un nuovo criterio per dispositivi mobili per il sito Redmond e di disabilitare l'utilizzo della funzionalità Chiamata tramite ufficio per tutti gli utenti a cui il criterio viene applicato. A tale scopo, il parametro EnableOutsideVoice viene impostato su False.

    New-CsMobilityPolicy -Identity site:Redmond -EnableOutsideVoice $False

## ESEMPIO 2

Nell'esempio 2 viene illustrato come creare un nuovo criterio per dispositivi mobili in memoria, modificare un valore di una proprietà per tale criterio e quindi utilizzare il cmdlet **Set-CsMobilityPolicy** per convertire il criterio virtuale in un criterio per dispositivi mobili effettivo di Lync Server. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **New-CsMobilityPolicy** e il parametro InMemory per creare un nuovo criterio per il sito Redmond. Poiché il parametro InMemory fa in modo che questo criterio sia presente solo in memoria, l'oggetto risultante deve essere archiviato in una variabile ($x).

Nel comando 2 la proprietà EnableOutsideVoice per il criterio virtuale è impostata su False. Nel comando 3 vengono quindi utilizzati il cmdlet **Set-CsMobilityPolicy** e il parametro Instance per scrivere le modifiche in Lync Server e creare un criterio per dispositivi mobili per il sito Redmond. Se non si chiama il cmdlet **Set-CsMobilityPolicy**, il criterio non verrà creato e, anzi, verrà eliminato non appena si termina la sessione dell' interfaccia della riga di comando Windows PowerShell o si elimina la variabile $x.

    $x = New-CsMobilityPolicy -Identity site:Redmond -InMemory
    $x.EnableOutsideVoice = $False
    Set-CsMobilityPolicy -Instance $x

## Descrizione dettagliata

Lync Mobile è un'applicazione client che consente agli utenti di eseguire Lync nei cellulari. La funzionalità Chiamata tramite ufficio consente agli utenti di effettuare chiamate con il cellulare che risultano provenire dal numero dell'ufficio anziché da quello del cellulare. Gli utenti abilitati per la funzionalità Chiamata tramite ufficio possono ottenere questo risultato componendo il numero direttamente dal cellulare oppure utilizzando l'opzione di conferenza telefonica con chiamata in uscita. Con questa opzione, un utente richiede al server dei servizi per dispositivi mobili Lync Server di effettuare una chiamata al suo posto. La chiamata viene configurata dal server e quindi l'utente viene richiamato sul cellulare. Dopo che l'utente ha risposto, il server compone il numero della parte chiamata. Entrambe queste funzionalità possono essere gestite utilizzando criteri per dispositivi mobili.

Con Lync Server 2013, i dispositivi mobili possono effettuare o ricevere chiamate tramite la rete cellulare standard oppure tramite connessioni Wi-Fi. I criteri per dispositivi mobili possono essere utilizzati per richiedere connessioni Wi-Fi e impedire le chiamate tramite la rete cellulare.

Quando si installa Lync Server, è presente un singolo criterio per dispositivi mobili globale che si applica a tutti gli utenti. Gli amministratori possono tuttavia utilizzare il cmdlet **New-CsMobilityPolicy** per creare criteri personalizzati nell'ambito del sito o per utente.

Per abilitare la funzionalità Chiamata tramite ufficio è necessario configurare due proprietà diverse. La prima, EnableOutsideVoice, determina se la funzionalità Chiamata tramite ufficio è abilitata. La seconda, EnableMobility, determina se gli utenti possono utilizzare Lync Mobile. Per consentire a un utente di utilizzare la funzionalità Chiamata tramite ufficio, entrambe queste proprietà devono essere impostate su True. Se EnableMobility è impostata su True ed EnableOutsideVoice è impostata su False, l'utente può eseguire Lync Mobile, ma non può utilizzare la funzionalità Chiamata tramite ufficio. Se EnableMobility è impostata su False ed EnableOutsideVoice è impostata su True, l'utente non può eseguire Lync Mobile e, di conseguenza, non può utilizzare la funzionalità Chiamata tramite ufficio, indipendentemente dal valore della proprietà EnableOutsideVoice.

Per utilizzare la caratteristica Chiamata tramite ufficio, gli utenti devono essere gestiti da criteri vocali che consentano lo squillo simultaneo.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsMobilityPolicy** in locale: RTCUniversalServerAdmins.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca da assegnare al criterio. I nuovi criteri per dispositivi mobili possono essere creati nell'ambito del sito o per utente. Per creare un nuovo criterio di sito, utilizzare il prefisso &quot;site:&quot; e il nome del sito come identità. Utilizzare, ad esempio, la sintassi seguente per creare un nuovo criterio per il sito Redmond:</p>
<p>-Identity site:Redmond</p>
<p>Per creare nuovi criteri per utente, utilizzare una sintassi analoga alla seguente:</p>
<p>-Identity SalesDepartmentPolicy</p>
<p>Notare che non è possibile creare nuovi criteri globali. Se si desidera apportare modifiche ai criteri globali, utilizzare invece il cmdlet <strong>Set-CsMobilityPolicy</strong>. Analogamente, non è possibile creare nuovi criteri di sito o per utente se esistono già criteri con tale identità. Se è necessario apportare modifiche a criteri esistenti, utilizzare il cmdlet <strong>Set-CsMobilityPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCustomerExperienceImprovementProgram</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti dei dispositivi mobili possono partecipare al programma Analisi utilizzo software.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExchangeConnectivity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono connettersi a Microsoft Exchange Server 2013 utilizzando un dispositivo mobile.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSaveCallLogs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono salvare un registro delle chiamate effettuate o ricevute da un dispositivo mobile.</p>
<p>Questa impostazione non si applica ai dispositivi Android.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSaveCredentials</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono salvare informazioni relative alle credenziali, ad esempio la password, su un dispositivo mobile. Tali informazioni potranno quindi essere applicate negli scenari di accesso automatico.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSaveIMHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True (valore predefinito), gli utenti possono salvare trascrizioni di sessioni di conferenza e messaggistica istantanea su un dispositivo mobile.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo descrittivo da associare al criterio. Il parametro Description potrebbe ad esempio includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableIPAudioVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se viene impostato su False, questo parametro impedisce all'utente di effettuare chiamate VoIP (Voice over IP) utilizzando il dispositivo mobile. Il valore predefinito è True, ovvero le chiamate VoIP sono consentite.</p>
<p>Questo parametro è stato introdotto in Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobility</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti sono autorizzati a utilizzare Lync Mobile.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOutsideVoice</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti sono autorizzati a utilizzare la caratteristica Chiamata tramite ufficio. Quando è impostato su False, gli utenti non possono utilizzare tale caratteristica.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output di un comando chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsMobilityPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility.

