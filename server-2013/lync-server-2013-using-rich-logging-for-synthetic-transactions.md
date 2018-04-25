---
title: Utilizzo della registrazione dettagliata per le transazioni sintetiche
TOCTitle: Utilizzo della registrazione dettagliata per le transazioni sintetiche
ms:assetid: 32714a71-9f42-4d5b-a508-e176d8f08bbf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204798(v=OCS.15)
ms:contentKeyID: 49300111
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo della registrazione dettagliata per le transazioni sintetiche

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Le transazioni sintetiche (introdotte in Microsoft Lync Server 2010) consentono agli amministratori di verificare che gli utenti possano completare correttamente attività comuni come l'accesso al sistema, lo scambio di messaggi istantanei o l'invio di chiamate a un telefono connesso alla rete PSTN (Public Switched Telephone Network). Queste attività (offerte sotto forma di pacchetto contenente un set di cmdlet di Lync ServerWindows PowerShell) possono essere eseguite manualmente da un amministratore o automaticamente mediante un'applicazione come System Center Operations Manager.

In Lync Server 2010 le transazioni sintetiche si sono rivelate estremamente utili per aiutare gli amministratori a identificare i problemi relativi al sistema. Il cmdlet **Test-CsRegistration**, ad esempio, poteva avvisare gli amministratori nel caso in cui alcuni utenti riscontravano problemi durante la registrazione con Lync Server. Le transazioni sintetiche, tuttavia, erano meno utili per stabilire il motivo di tale difficoltà, in quanto non fornivano informazioni di registrazione dettagliate che potessero consentire agli amministratori di risolvere i problemi relativi a Lync Server. Nella migliore delle ipotesi, l'output dettagliato di una transazione sintetica offriva informazioni passo passo grazie alle quali un amministratore poteva formulare un'ipotesi plausibile sulla probabile ubicazione del problema.

In Microsoft Lync Server 2013 le transazioni sintetiche sono state riprogettate in modo da offrire una registrazione completa ovvero contenente, per ogni attività eseguita da una transazione sintetica, informazioni simili alle seguenti:

  - L'ora di inizio dell'attività

  - L'ora di fine dell'attività

  - L'azione eseguita, ad esempio la creazione, la partecipazione o l'abbandono di una conferenza, l'accesso a Lync Server, l'invio di un messaggio istantaneo e così via

  - Messaggi informativi, dettagliati, di avviso o di errore generati durante l'esecuzione dell'attività

  - Messaggi di registrazione SIP

  - Record delle eccezioni o codici diagnostici generati durante l'esecuzione dell'attività

  - Il risultato dell'esecuzione dell'attività

Queste informazioni vengono generate automaticamente a ogni esecuzione di una transazione sintetica, tuttavia non vengono visualizzate né salvate automaticamente in un file di log. Gli amministratori che eseguono manualmente una transazione sintetica possono invece usare il parametro OutLoggerVariable per specificare una variabile di Windows PowerShell in cui verranno archiviate le informazioni. Partendo da questa, gli amministratori possono quindi usare una coppia di metodi con cui salvare e/o visualizzare il log completo in formato XML o HTML.

Gli amministratori di Lync Server 2010 possono, ad esempio, eseguire il cmdlet **Test-CsRegistration** specificando un comando simile al seguente:

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com

Possono inoltre scegliere se includere il parametro OutLoggerVariable seguito dal nome di variabile desiderato:

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -OutLoggerVariable RegistrationTest


> [!NOTE]
> Non anteporre il carattere $ al nome di variabile. Un nome valido può essere ad esempio RegistrationTest, mentre non lo è il nome $RegistrationTest.



Il comando precedente restituisce un contenuto simile al seguente:

    Target Fqdn   : atl-cs-001.litwareinc.com
    Result        : Failure
    Latency       : 00:00:00
    Error Message : This machine does not have any assigned certificates.
    Diagnosis     :

Per questo errore, sono tuttavia disponibili informazioni ancora più dettagliate che non si limitano al messaggio di errore riportato sopra. Per accedere a tali informazioni in formato HTML, specificare un comando simile al seguente in modo da salvare in un file HTML le informazioni archiviate nella variabile RegistrationTest:

    $RegistrationTest.ToHTML() | Out-File C:\Logs\Registration.html

In alternativa, è possibile usare il metodo ToXML() per salvare i dati in un file XML:

    $RegistrationTest.ToXML() | Out-File C:\Logs\Registration.xml

Questi file possono essere quindi visualizzati usando Internet Explorer, Visual Studio o qualsiasi altra applicazione che consenta l'apertura di file HTML/XML.

Le transazioni sintetiche eseguite dall'interno di System Center Operations Manager genereranno automaticamente questi file di log in presenza di errori. I log, tuttavia, non verranno generati se l'esecuzione ha esito negativo prima che Windows PowerShell possa caricare ed eseguire la transazione sintetica.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per impostazione predefinita, Lync Server 2013 salva i file di log in una cartella non condivisa. Per rendere i log immediatamente accessibili, è necessario condividere la cartella, ad esempio \\atl-watcher-001.litwareinc.com\WatcherNode.</td>
</tr>
</tbody>
</table>

