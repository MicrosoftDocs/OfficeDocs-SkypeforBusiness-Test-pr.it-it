---
title: Configurazione degli utenti test e delle impostazioni di configurazione del nodo Watcher
TOCTitle: Configurazione degli utenti test e delle impostazioni di configurazione del nodo Watcher
ms:assetid: ab00e9cb-f539-4aa6-bcb4-5533fbe7bc44
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205152(v=OCS.15)
ms:contentKeyID: 49301624
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione degli utenti test e delle impostazioni di configurazione del nodo Watcher

 

_**Ultima modifica dell'argomento:** 2013-07-29_

Dopo avere configurato il computer che fungerà da nodo Watcher, è necessario eseguire le operazioni seguenti:

1.  Creare gli account di test che devono essere utilizzati da questi nodi Watcher. Se si utilizza il metodo di autenticazione Negotiate, è inoltre necessario utilizzare il cmdlet [Set-CsTestUserCredential](set-cstestusercredential.md) per abilitare questi account di test per l'utilizzo nel nodo Watcher.

2.  Aggiornare le impostazioni di configurazione del nodo Watcher.

In questa sezione vengono trattati i temi seguenti:

  - Configurazione degli account utente di test

  - Configurazione di un nodo Watcher di base con le transazioni sintetiche predefinite

  - Configurazione dei test estesi

  - Aggiunta e rimozione di transazioni sintetiche

  - Visualizzazione e verifica della configurazione del nodo Watcher

## Configurazione degli account utente di test

Gli utenti di test non devono necessariamente rappresentare persone reali, ma devono essere account validi di Servizi di dominio Active Directory. Tali account devono inoltre essere abilitati per Lync Server 2013, avere indirizzi SIP validi ed essere abilitati per VoIP aziendale (per utilizzare la transazione sintetica Test-CsPstnPeerToPeerCall). Se si utilizza il metodo di autenticazione TrustedServer, è sufficiente verificare che tali account esistano e siano stati configurati come qui specificato. È consigliabile assegnare almeno tre utenti di test per ogni pool da testare.

Se si utilizza il metodo di autenticazione Negotiate, è inoltre necessario utilizzare il cmdlet **Set-CsTestUserCredential** e Lync Server Management Shell per consentire a tali account di test di funzionare con le transazioni sintetiche. A tale scopo, è possibile eseguire un comando simile al seguente. In questi comandi si presuppone che i tre account utente di Active Directory siano già stati creati e abilitati per Lync Server 2013:

    Set-CsTestUserCredential -SipAddress "sip:watcher1@litwareinc.com" -UserName "litwareinc\watcher1" -Password "P@ssw0rd"
    Set-CsTestUserCredential -SipAddress "sip:watcher2@litwareinc.com" -UserName "litwareinc\watcher2" -Password "P@ssw0rd"
    Set-CsTestUserCredential -SipAddress "sip:watcher3@litwareinc.com" -UserName "litwareinc\watcher3" -Password "P@ssw0rd"

È necessario includere non solo l'indirizzo SIP, ma anche il nome e la password dell'utente. Se non si include la password, Set-CsTestUserCredential chiederà di immetterla. Il nome utente può essere specificato nel formato nome dominio\\nome utente sopra riportato oppure nel formato nome utente@nome dominio. Ad esempio:

    -UserName "watcher3@litwareinc.com"

Per verificare che le credenziali degli utenti di test siano state create, eseguire questi comandi da Lync Server Management Shell:

    Get-CsTestUserCredential -SipAddress "sip:watcher1@litwareinc.com"
    Get-CsTestUserCredential -SipAddress "sip:watcher2@litwareinc.com"
    Get-CsTestUserCredential -SipAddress "sip:watcher3@litwareinc.com"

Per ogni utente vengono restituite informazioni simili alle seguenti:

    UserName                        Password
    --------                        --------
    Litwareinc\watcher1              System.Security.SecureString

## Configurazione di un nodo Watcher di base con le transazioni sintetiche predefinite

Dopo avere creato gli utenti di test, è possibile creare un nodo Watcher usando un comando simile al seguente:

    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers @{Add= "sip:watcher1@litwareinc.com","sip:watcher2@litwareinc.com", "sip:watcher3@litwareinc.com"}

Questo comando crea un nuovo nodo Watcher che usa le impostazioni predefinite ed esegue il set predefinito di transazioni sintetiche. Il nuovo nodo Watcher inoltre usa gli utenti di test watcher1@litwareinc.com, watcher2@litwareinc.com e watcher3@litwareinc.com. Se il nodo Watcher usa l'autenticazione TrustedServer, i tre account di test possono corrispondere a qualsiasi account utente valido abilitato per Active Directory e Lync Server. Se il nodo Watcher usa il metodo di autenticazione Negotiate, è inoltre necessario abilitare questi account utente per il nodo Watcher mediante il cmdlet **Set-CsTestUserCredential**.

## Configurazione dei test estesi

Se si vuole abilitare il test PSTN, che verifica la connettività alla rete PSTN (Public Switched Telephone Network), è necessario eseguire alcune attività di configurazione aggiuntive durante l'impostazione del nodo Watcher. Prima di tutto occorre associare gli utenti di test al tipo di test PSTN. A questo scopo eseguire un comando simile al seguente da Lync Server Management Shell:

    $pstnTest = New-CsExtendedTest -TestUsers "sip:watcher1@litwareinc.com", "sip:watcher2@litwareinc.com", "sip:watcher3@litwareinc.com"  -Name "Contoso Provider Test" -TestType PSTN

I risultati di questo comando devono essere archiviati in una variabile. In questo esempio la variabile è denominata $pstnTest.

A questo punto è possibile usare il cmdlet **New-CsWatcherNodeConfiguration** per associare il tipo di test, archiviato nella variabile $pstnTest, a un pool di Lync Server 2013. Il comando seguente ad esempio crea la configurazione di un nuovo nodo Watcher per il pool atl-cs-001.litwareinc.com, aggiungendo i tre utenti di test creati in precedenza e il tipo di test PSTN:

    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers @{Add= "sip:watcher1@litwareinc.com","sip:watcher2@litwareinc.com", "sip:watcher3@litwareinc.com"} -ExtendedTests @{Add=$pstnTest}

Il comando precedente non riesce se il database RTCLocal e i file principali di Lync Server non sono stati installati nel computer nodo Watcher.

Per testare più criteri vocali, è necessario creare un test esteso per ogni criterio usando il cmdlet **New-CsExtendedTest**. Gli utenti assegnati a questo test devono essere configurati con i criteri vocali desiderati. I test estesi vengono quindi passati al cmdlet **New-CsWatcherNodeConfiguration** mediante un comando simile al seguente:

    -ExtendedTests @{Add=$pstnTest1,$pstnTest2,$pstnTest3}

Se New-CsWatcherNodeConfiguration viene chiamato senza usare il parametro Tests, solo le transazioni sintetiche predefinite e la transazione sintetica estesa specificata saranno abilitate per il nuovo nodo Watcher. Questo significa che il nodo Watcher testerà i componenti seguenti:

  - Registration

  - IM

  - GroupIM

  - P2PAV (Sessioni audio/video peer-to-peer)

  - AvConference (Conferenze audio)

  - Presence

  - ABS (Servizio Rubrica)

  - ABWQ (Servizio Web Rubrica)

  - PSTN (Chiamate di gateway PSTN, specificate come test esteso. Per impostazione predefinita, il test PSTN è disabilitato. Il test è abilitato in questo caso solo perché è stato abilitato dal comando mediante il parametro ExtendedTests).

Questo inoltre significa che, per impostazione predefinita, non verranno testati i componenti seguenti:

  - AVEdgeConnectivity

  - MCXP2PIM (messaggistica istantanea dei dispositivi mobili)

  - ExumConnectivity (Messaggistica unificata di Exchange)

  - JoinLauncher

  - PersistentChatMessage

  - DataConference

  - XmppIM

  - UnifiedContactStore

## Aggiunta e rimozione di transazioni sintetiche

Dopo avere configurato un nodo Watcher, è possibile usare il cmdlet **Set-CsWatcherNodeConfiguration** per aggiungere o rimuovere transazioni sintetiche dal nodo. Ad esempio, per aggiungere il test PersistentChatMessage al nodo Watcher, usare il metodo Add e un comando simile al seguente:

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Add="PersistentChatMessage"}

È possibile aggiungere più test separandone i nomi con le virgole. Ad esempio:

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Add="PersistentChatMessage","DataConference","UnifiedContactStore"}

Se uno o più di questi test, ad esempio DataConference, sono già stati abilitati per il nodo Watcher, si verifica un errore. In questo caso viene visualizzato un messaggio di errore simile al seguente:

    Set-CsWatcherNodeConfiguration : Sequenza di chiave duplicata 'DataConference' per la chiave 'urn:schema:Microsoft.Rtc.Management.Settings.WatcherNode.2010:TestName' o per il vincolo di identità univoco.

Quando si verifica questo errore, non vengono apportate modifiche. Il comando deve essere eseguito di nuovo dopo avere rimosso il test duplicato.

Per rimuovere una transazione sintetica da un nodo Watcher, usare il metodo Remove invece del metodo Add. Ad esempio, questo comando rimuove il test ABWQ da un nodo Watcher:

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Remove="ABWQ"}

È anche possibile usare il metodo Replace per sostituire tutti i test attualmente abilitati con uno o più test nuovi. Ad esempio, per fare in modo che un nodo Watcher esegua solo il test IM, è possibile configurare questa condizione usando il comando seguente:

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Replace="IM"}

Quando si esegue il comando precedente, per il nodo Watcher specificato verranno disabilitate tutte le transazioni sintetiche tranne IM.

## Visualizzazione e verifica della configurazione del nodo Watcher

Per visualizzare i test assegnati a un nodo Watcher, usare un comando simile al seguente:

    Get-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" | Select-Object -ExpandProperty Tests

Il comando precedente restituirà informazioni simili alle seguenti, a seconda delle transazioni sintetiche assegnate al nodo:

    Registration
    IM
    GroupIM
    P2PAV
    AvConference
    Presence
    PersistentChatMessage
    DataConference

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per visualizzare le transazioni sintetiche in ordine alfabetico, usare invece il comando seguente:<br />
Get-CsWatcherNodeConfiguration –Identity &quot;atl-cs-001.litwareinc.com&quot; | Select-Object –ExpandProperty Tests | Sort-Object</td>
</tr>
</tbody>
</table>


Per verificare che un nodo Watcher sia stato creato, digitare il comando seguente da Lync Server Management Shell:

    Get-CsWatcherNodeConfiguration

Verranno restituite informazioni simili alle seguenti:

    Identity      : atl-cs-001.litwareinc.com
    TestUsers     : {sip:watcher1@litwareinc.com, sip:watcher2@litwareinc.com ...}
    ExtendedTests : {TestUsers=IList<System.String>;Name=PSTN Test; Te...}
    TargetFqdn    : atl-cs-001.litwareinc.com
    PortNumber    : 5061

Per verificare che il nodo Watcher sia stato configurato correttamente, digitare il comando seguente da Lync Server Management Shell:

    Test-CsWatcherNodeConfiguration

Il comando precedente verificherà ogni nodo Watcher nella distribuzione e restituirà informazioni che indicano se:

  - Il ruolo Funzione di registrazione necessario è stato installato.

  - La chiave del Registro di sistema necessaria è stata creata automaticamente durante l'esecuzione di Set-CsWatcherNodeConfiguration.

  - I server eseguono la versione corretta di Lync Server.

  - Le porte sono state configurate correttamente.

  - Gli utenti di test assegnati dispongono delle credenziali necessarie.

