---
title: Integrazione di un'applicazione di collaborazione di terze parti con Lync
TOCTitle: Integrazione di un'applicazione di collaborazione di terze parti con Lync
ms:assetid: 00b9312c-b0c8-4f79-8b76-05b2d820e197
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398068(v=OCS.15)
ms:contentKeyID: 52062082
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Integrazione di un'applicazione di collaborazione di terze parti con Lync

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile integrare Lync 2013 con applicazioni di collaborazione online di terze parti aggiungendo informazioni sull'applicazione nel Registro di sistema. È possibile utilizzare Lync 2013 per avviare sessioni di conferenza dati ospitate in un server interno, un servizio basato su Internet o entrambi. La sessione di collaborazione o di conferenza dati può essere avviata dall'elenco contatti oppure da una sessione video, vocale o di messaggistica istantanea esistente. Lync 2013 opera esclusivamente come mezzo per l'avvio dell'applicazione. Le eventuali conversazioni di Lync 2013 esistenti rimangono attive dopo l'inizio della sessione di collaborazione online.

Nelle sezioni seguenti viene illustrata l'integrazione di Lync 2013 con applicazioni di collaborazione basate su Internet e su server.

## Integrazione di un'applicazione di collaborazione basata su Internet con Lync 2013

In generale, la procedura per integrare un'applicazione di collaborazione di terze parti è la seguente:

1.  Le informazioni relative all'applicazione vengono aggiunte al Registro di sistema.

2.  L'organizzatore esegue l'accesso a Lync 2013 e seleziona i contatti per la condivisione dei dati e la collaborazione. È anche possibile che l'organizzatore sia già impegnato in una conversazione e decida di aggiungere la funzionalità per conferenze dati.

3.  Lync 2013 legge il Registro di sistema, avvia l'applicazione di collaborazione e quindi invia un messaggio SIP personalizzato (appINVITE) ai partecipanti selezionati.

4.  I partecipanti accettano l'invito e l'applicazione di collaborazione viene avviata nel computer di ognuno di essi. Lync 2013 utilizza il Registro di sistema per determinare quale applicazione di collaborazione utilizzare e quindi avvia tale applicazione utilizzando i parametri inclusi nel messaggio appINVITE.

Nella tabella seguente vengono illustrate le voci del Registro di sistema necessarie per integrare un'applicazione di collaborazione basata su Internet con Lync 2013. Tali voci sono disponibili nel Registro di sistema nel percorso seguente:

  - HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Office\\15.0\\Lync\\SessionManager\\Apps\\Parameters

### Voci del Registro di sistema per un'applicazione di collaborazione basata su Internet

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Tipo</th>
<th>Dati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Name</p></td>
<td><p>REG_SZ</p></td>
<td><p>Nome dell'applicazione per i menu di Lync 2013.</p></td>
</tr>
<tr class="even">
<td><p>SmallIcon</p></td>
<td><p>REG_SZ</p></td>
<td><p>Percorso dell'icona 16 x 16 pixel in formato BMP o PNG.</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>REG_SZ</p></td>
<td><p>Percorso dei partecipanti per l'avvio dell'applicazione di collaborazione online.</p></td>
</tr>
<tr class="even">
<td><p>OriginatorPath</p></td>
<td><p>REG_SZ</p></td>
<td><p>Percorso dell'organizzatore per l'avvio dell'applicazione di collaborazione online. Questo percorso può contenere uno o più parametri personalizzati, definiti nella sottochiave Parameters. Ad esempio, <code>https://meetserv.adatum.com/cc/%param1%/join?id=%param2%&amp;role=present&amp;pw=%param3%</code></p></td>
</tr>
<tr class="odd">
<td><p>SessionType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = Sessione locale. L'applicazione viene avviata nel computer locale.</p>
<p>1 = Sessione tra due parti (impostazione predefinita). Lync 2013 avvia l'applicazione in locale e quindi invia una notifica di sistema all'altro utente. L'altro utente fa clic sulla notifica e avvia l'applicazione specificata nel proprio computer.</p>
<p>2 = Sessione tra più parti. Lync 2013 avvia l'applicazione in locale e quindi invia notifiche di sistema agli altri utenti, chiedendo loro di avviare l'applicazione specificata nel rispettivo computer.</p></td>
</tr>
<tr class="even">
<td><p>ExensibleMenu</p></td>
<td><p>REG_SZ</p></td>
<td><p>Elenco dei menu, separati da punti e virgola, in cui verrà visualizzato il comando. I valori possibili sono i seguenti:</p>
<ul>
<li><p>MainWindowActions</p></li>
<li><p>MainWindowRightClick</p></li>
<li><p>ConversationWindowActions</p></li>
<li><p>ConversationWindowButton</p></li>
<li><p>ConversationWindowRightClick</p></li>
</ul>
<p>Se la voce ExtensibleMenu non è definita, verranno utilizzati i valori predefiniti MainWindowRightClick e ConversationWindowActions.</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente vengono illustrate le voci del Registro di sistema per i parametri. Tali voci sono disponibili in HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\15.0\\Lync\\SessionManager\\Apps\\Parameters.

### Voci del Registro di sistema per un'applicazione di collaborazione basata su Internet

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Tipo</th>
<th>Dati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Param1</p></td>
<td><p>REG_SZ</p></td>
<td><p>Utilizzata in formato token (<code>%Parm1%</code>) per aggiungere valori specifici dell'utente alla chiave OriginatorPath del Registro di sistema.</p></td>
</tr>
<tr class="even">
<td><p>Param2</p></td>
<td><p>REG_SZ</p></td>
<td><p>Vedere Param1.</p></td>
</tr>
<tr class="odd">
<td><p>Param3</p></td>
<td><p>REG_SZ</p></td>
<td><p>Vedere Param1.</p></td>
</tr>
</tbody>
</table>


Le seguenti impostazioni del Registro di sistema di esempio consentono di integrare il client di collaborazione ADatum con Lync 2013:

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps\{C3F6E17A-855F-44a0-B90D-C0B92D38E5F1}]
    "Path"="https://meetingservice.adatum.com/cc/%param1%/meet/%param2%"
    "OriginatorPath"="https://meetserv.adatum.com/cc/%param1%/join?id=%param2%&role=present&pw=%param3%"
    "SessionType"=dword:00000002
    "ApplicationType"=dword:00000001
    "LiveServerIntegration"=dword:00000000
    "Name"="ADatum Online Collaboration Service"
    "Extensiblemenu"="MainWindowActions;MainWindowRightClick;ConversationWindowActions;ConversationWindowRightClick"
    
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager]
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager\Apps]
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager\Apps\Parameters]
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager\Apps\Parameters\{C3F6E17A-855F-44a0-B90D-C0B92D38E5F1}]
    "Param1"="meetserv"
    "Param2"="admin"
    "Param3"="abcdefg123"

## Integrazione di un'applicazione di collaborazione basata su server con Lync 2013

Le impostazioni per aggiungere i comandi per l'avvio di un'applicazione di collaborazione basata su server da Lync 2013 sono simili a quelle descritte nella sezione precedente: Integrazione di un'applicazione di collaborazione basata su Internet con Lync 2013. La voce OriginatorPath tuttavia non è necessaria e alcuni valori sono diversi. Le voci del Registro di sistema sono disponibili nel percorso seguente:

  - HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Office\\15.0\\Lync\\SessionManager\\Apps\\Parameters

### Voci del Registro di sistema per un'applicazione di collaborazione basata su server

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Tipo</th>
<th>Dati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Name</p></td>
<td><p>REG_SZ</p></td>
<td><p>Nome dell'applicazione visualizzato nel menu.</p></td>
</tr>
<tr class="even">
<td><p>ApplicationType</p></td>
<td><p>DWORD</p></td>
<td><p>Valore = 1. Imposta il tipo di applicazione su Protocollo. In questo caso non si applicano gli altri valori possibili. Se non presente, come tipo di applicazione viene impostato 0 (Eseguibile).</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>REG_SZ</p></td>
<td><p>Protocollo utilizzato per avviare l'applicazione di collaborazione. Per Live Meeting 2007 il valore di Path è impostato su <code>meet:%conf-uri%</code>.</p></td>
</tr>
<tr class="even">
<td><p>SessionType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = Sessione locale. L'applicazione viene avviata nel computer locale.</p>
<p>1 = Sessione tra due parti (impostazione predefinita). Lync 2013 avvia l'applicazione in locale e quindi invia una notifica di sistema all'altro utente. L'altro utente fa clic sulla notifica e avvia l'applicazione specificata nel proprio computer.</p>
<p>2 = Sessione tra più parti. Lync 2013 avvia l'applicazione in locale e quindi invia notifiche di sistema agli altri utenti, chiedendo loro di avviare l'applicazione specificata nel rispettivo computer.</p></td>
</tr>
<tr class="odd">
<td><p>MCUType</p></td>
<td><p>REG_SZ</p></td>
<td><p>DATI = Tipo di server.</p></td>
</tr>
<tr class="even">
<td><p>ExtensibleMenu</p></td>
<td><p>REG_SZ</p></td>
<td><p>Elenco dei menu, separati da punti e virgola, in cui verrà visualizzato il comando. I valori possibili sono i seguenti:</p>
<ul>
<li><p>MainWindowActions</p></li>
<li><p>MainWindowRightClick</p></li>
<li><p>ConversationWindowActions</p></li>
<li><p>ConversationWindowButton</p></li>
<li><p>ConversationWindowRightClick</p></li>
</ul>
<p>Se la voce ExtensibleMenu non è definita, verranno utilizzati i valori predefiniti MainWindowRightClick e ConversationWindowActions.</p></td>
</tr>
</tbody>
</table>


Nell'esempio seguente vengono aggiunti i comandi per avviare il client di collaborazione ADatum da Lync 2013:

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps\{27877e66-615c-4582-ab88-0cb2ca05d951}]
    "Path"="meet:%conf-uri%"
    "SessionType"=dword:00000002
    "LiveServerIntegration"=dword:00000001
    "ApplicationType"=dword:00000001
    "Name"="ADatum Collaboration Client"
    "MCUType"="Data"
    "Extensiblemenu"="MainWindowActions;MainWindowRightClick;ConversationWindowActions;ConversationWindowRightClick"

