---
title: Aggiunta di comandi ai menu di Lync
TOCTitle: Aggiunta di comandi ai menu di Lync
ms:assetid: a8443bc2-e234-4022-870a-00700f38b1ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412788(v=OCS.15)
ms:contentKeyID: 52062279
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiunta di comandi ai menu di Lync

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile aggiungere comandi personalizzati ai menu di Lync 2013 e passare l'URI (Uniform Resource Identifier) SIP dell'utente corrente e i contatti selezionati all'applicazione avviata dal comando personalizzato.

È possibile visualizzare i comandi personalizzati aggiunti all'interno di uno o più dei menu seguenti:

  - Menu Strumenti, sulla barra dei menu della finestra principale di Lync

  - Menu di scelta rapida per i contatti nell'elenco Contatti

  - Menu Altre opzioni nella finestra Conversazione

  - Menu di scelta rapida per gli utenti elencati nell'elenco dei partecipanti della finestra Conversazione

  - Menu Opzioni in una scheda contatto

È possibile definire comandi personalizzati per due tipi di applicazioni, ovvero per le applicazioni con una delle caratteristiche seguenti:

  - Si applicano solo all'utente corrente e vengono avviate nel computer locale.

  - Coinvolgono altri utenti, come avviene con i programmi di collaborazione online, e devono essere avviate nel computer di ogni utente.

È possibile richiamare il comando personalizzato nei modi seguenti:

  - Selezionare uno o più utenti e quindi scegliere il comando personalizzato.

  - Avviare una conversazione con due o più partecipanti e quindi scegliere il comando personalizzato.

## Per aggiungere un comando personalizzato

Per aggiungere comandi ai menu, utilizzare le impostazioni del Registro di sistema nella tabella seguente. Queste voci si trovano nel percorso seguente all'interno del Registro di sistema:

HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Office\\15.0\\Lync\\CustomCommands

### Voci del Registro di sistema dei comandi personalizzati

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
<td><p>0 = Eseguibile (impostazione predefinita)</p>
<div class="alert">

> [!NOTE]
> Richiede ApplicationInstallPath.


</div>
<p>1 = Protocollo</p></td>
</tr>
<tr class="odd">
<td><p>ApplicationInstallPath</p></td>
<td><p>REG_SZ</p></td>
<td><p>Percorso completo dell'eseguibile.</p>
<div class="alert">

> [!NOTE]
> Deve essere specificato se ApplicationType è 0 (Eseguibile).


</div></td>
</tr>
<tr class="even">
<td><p>Path</p></td>
<td><p>REG_SZ</p></td>
<td><p>Percorso completo di avvio con eventuali parametri, compresi i parametri predefiniti<em>%user-id%</em> e <em>%contact-id%</em>.</p></td>
</tr>
<tr class="odd">
<td><p>SessionType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = Sessione locale. L'applicazione viene avviata nel computer locale.</p>
<p>1 = Sessione con due utenti (impostazione predefinita). Lync 2013 avvia l'applicazione in locale e quindi invia una notifica desktop all'altro utente, che avvia l'applicazione nel computer in uso facendo clic sulla notifica.</p>
<p>2 = Sessione con più utenti. Lync 2013 avvia l'applicazione in locale e quindi invia le notifiche desktop agli altri utenti, che avviano l'applicazione specificata nel computer in uso facendo clic sulla notifica.</p></td>
</tr>
<tr class="even">
<td><p>ExtensibleMenu</p></td>
<td><p>REG_SZ</p></td>
<td><p>Elenco dei menu, delimitati da punto e virgola, in cui verrà visualizzato il comando. I valori possibili sono:</p>
<p>MainWindowActions</p>
<p>MainWindowRightClick</p>
<p>ConversationWindowActions</p>
<p>ConversationWindowRightClick</p>
<p>ContactCardMenu</p>
<p>Se ExtensibleMenu non è definito, vengono utilizzati i valori predefiniti MainWindowRightClick e ConversationWindowActions.</p></td>
</tr>
</tbody>
</table>


Ad esempio, nel file dell'editor del Registro di sistema (con estensione REG) seguente sono illustrati i risultati dell'aggiunta della voce di menu Contoso Sales Contact Manager al menu Azioni nella finestra Conversazione:

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\CustomCommands\{1F9F07C6-7E0B-462B-AAD7-98C6DBEA8F69}]
    "Name"="Contoso Sales Contact Manager"
    "HelpMessage"="The Contoso Sales Contact Manager is not installed. Contact the Help Desk for more information."
    "ApplicationType"=dword:00000000
    "ApplicationInstallPath"="C:\\cscm.exe"
    "Path"="C:\\cscm.exe %user-id% %contact-id%"
    "SessionType"=dword:00000001
    "ExtensibleMenu"="ConversationWindowActions;MainWindowRightClick"

## Per accedere a un comando personalizzato

Per accedere a un comando personalizzato al termine dell'aggiunta, eseguire una delle operazioni seguenti, a seconda dei valori di ExtensibleMenu definiti:

  - **MainWindowActions**   Nella finestra principale di Lync fare clic su **Strumenti** e quindi scegliere il comando personalizzato.

  - MainWindowRightClick   Nella finestra principale di Lync fare clic con il pulsante destro del mouse su un contatto e quindi scegliere il comando personalizzato.

  - **ConversationWindowActions**   Nella finestra Conversazione fare clic sull'icona **Altre opzioni** e quindi scegliere il comando personalizzato.

  - **ConversationWindowRightClick**   Nella finestra Conversazione fare clic con il pulsante destro del mouse su un nome di contatto e quindi scegliere il comando personalizzato.

  - **ContactCardMenu**   Nella scheda contatto di un utente fare clic sull'icona Opzioni e quindi scegliere il comando personalizzato.

