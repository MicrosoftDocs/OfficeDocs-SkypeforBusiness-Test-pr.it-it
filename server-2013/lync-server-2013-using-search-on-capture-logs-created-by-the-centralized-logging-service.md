---
title: Utilizzo della ricerca sui log di acquisizione creati dal servizio di registrazione centralizzato
TOCTitle: Utilizzo della ricerca sui log di acquisizione creati dal servizio di registrazione centralizzato
ms:assetid: 1b75b218-d84f-47a7-8a0a-b7e016b1cc79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687982(v=OCS.15)
ms:contentKeyID: 49887463
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo della ricerca sui log di acquisizione creati dal servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Le funzionalità di ricerca del servizio di registrazione centralizzato sono utili e potenti per i seguenti motivi:

  - Le ricerche e i risultati vengono eseguiti su un unico computer, un pool, un sito o un ambito globale in base ai criteri definiti.

  - Inizialmente è possibile eseguire ricerche ad ampio spettro e successivamente restringerle adottando criteri più mirati, ad esempio un'ora, un componente o un computer. Le ricerche vengono eseguite negli stessi log e quando i criteri di ricerca cambiano non è necessario effettuare di nuovo una sessione di registrazione.

  - I risultati di ricerca prelevati da tutti i computer e i pool compresi nell'ambito vengono raccolti e aggregati in un singolo file di output che rappresenta tutti i risultati dei criteri di ricerca, limitatamente agli scenari eseguiti e ai dati acquisiti. È possibile utilizzare strumenti noti come **Snooper** o **Blocco note** per leggere il file di output e i messaggi di traccia di tutta la distribuzione.

In ogni singolo computer il componente Agente del servizio di registrazione centralizzato (CLSAgent) crea i log in base allo scenario o agli scenari in esecuzione (è possibile eseguire due scenari per computer in un dato momento). I log e i file di indice e cache associati sono gestiti da CLSAgent. Quando si definisce ed esegue una ricerca, il comando di ricerca indica a CLSAgent quali informazioni recuperare. CLSAgent esegue la query nei file di log, cache e indice e restituisce i risultati della ricerca al Controller servizio di registrazione centralizzato (CLSContoller). Quest'ultimo riceve i risultati di ricerca da tutti i computer e pool compresi nell'ambito della ricerca. Quindi aggrega (combina) i log e li ordina in base a un intervallo di tempo, dalla voce meno recente alla più recente.

Al termine di ogni ricerca viene eseguito il cmdlet **Sync-CsClsLogging**, che scarica la cache utilizzata per le ricerche (da non confondere con i file cache gestiti da CLSAgent). Lo scaricamento della cache aiuta a garantire la presenza di un buffer di acquisizione del log e del file di traccia vuoto in CLSController per la successiva operazione di ricerca.

Per sfruttare al meglio il servizio di registrazione centralizzato, è necessario sapere come configurare la ricerca affinché restituisca solo i messaggi di traccia dei log di computer e pool pertinenti per il problema ricercato.

Per eseguire le funzioni di ricerca del servizio di registrazione centralizzato utilizzando la Lync Server Management Shell, è necessario essere membri dei gruppi di sicurezza del controllo di accesso basato sui ruoli CsAdministrator o CsServerAdministrator oppure di un ruolo di controllo di accesso basato sui ruoli personalizzato contenente uno di questi gruppi. Per ottenere un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui questo cmdlet è stato assegnato (compresi i ruoli personalizzati creati dall'utente), eseguire il comando seguente nella Lync Server Management Shell o nel prompt di Windows PowerShell:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

Ad esempio:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

Nel resto di questo argomento viene illustrato come definire una ricerca per ottimizzare la risoluzione dei problemi.

## Per eseguire una ricerca di base utilizzando il servizio di registrazione centralizzato

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Verificare che nella distribuzione presso l'ambito globale sia in esecuzione lo scenario AlwaysOn e digitare quanto segue al prompt dei comandi:
    
        Search-CsClsLogging -OutputFilePath <string value of path and file to write the output file>
    

    > [!NOTE]
    > Per impostazione predefinita, Search-CsClsLogging invia i risultati della ricerca alla console. Se si desidera salvare i risultati in un file, utilizzare -OutputFilePath <EM>&lt;stringa di percorso completo del file&gt;</EM>. Per definire il parametro -OutputFilePath, specificare un percorso e un nome file come parte del parametro in un formato stringa tra virgolette, ad esempio C:\LogFiles\SearchOutput.txt). Nell'esempio fornito è necessario verificare che la directory C:\LogFiles esista e di disporre delle autorizzazioni di lettura e scrittura (autorizzazione NTFS Modifica) dei file nella cartella. L'output viene aggiunto e non sovrascritto. Se sono necessari singoli file, definire un nome di file per ogni ricerca.

    
    Ad esempio:
    
        Search-CsClsLogging -OutputFilePath "C:\LogFiles\logfile.txt"

## Per eseguire una ricerca di base in un pool o in un computer utilizzando il servizio di registrazione centralizzato

1.  Per limitare la ricerca a uno specifico pool o computer, utilizzare il parametro -Computers con il computer definito da un nome completo tra virgolette e separato da una virgola come segue:
    
        Search-CsClsLogging -Computers <string value of computer names> -OutputFilePath <string value of path and file to write the output file>
    
    Ad esempio:
    
        Search-CsClsLogging -Computers "fe01.contoso.net" -OutputFilePath "C:\LogFiles\logfile.txt"

2.  Per eseguire la ricerca in più computer, digitare più nomi di computer racchiusi tra virgolette e separati da virgole, come l'esempio seguente:
    
        Search-CsClsLogging -Computers "fe01.contoso.net", "fe02.contoso.net", "fe03.contoso.net" -OutputFilePath "C:\LogFiles\logfile.txt"

3.  Se è necessario eseguire la ricerca in un intero pool, anziché in un singolo computer, modificare il parametro -Computers in -Pools, rimuovere il nome del computer e sostituirlo con il pool o i pool tra virgolette separati da virgole.
    
    Ad esempio:
    
        Search-CsClsLogging -Pools "pool01.contoso.net" -OutputFilePath "C:\Logfiles\logfile.txt"

4.  Utilizzando i comandi di ricerca, è possibile utilizzare qualsiasi pool della distribuzione, come pool Front End, pool di server perimetrali, pool di server Chat persistente o altri pool definiti tali.
    
    Ad esempio:
    
        Search-CsClsLogging -Pools "pool01.contoso.net", "pchatpool01.contoso.net", "intedgepool01.contoso.net" -OutputFilePath "C:\Logfiles\logfile.txt"

## Per eseguire una ricerca utilizzando parametri temporali

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per impostazione predefinita, l'ora di inizio dei parametri di tempo per una ricerca precede di 30 minuti l'ora di avvio della ricerca. In altre parole, se una ricerca viene avviata alle 16.00.00, nei log dei computer e dei pool definiti la ricerca sarà eseguita dalle 15.30.00 alle 16.00.00. Qualora sia necessario effettuare la ricerca 60 minuti o 3 ore prima dell'ora attuale, utilizzare il parametro -StartTime e impostare la stringa di data e ora per indicare l'ora in cui si desidera avviare la ricerca.
    
    Ad esempio, impostando un intervallo di data e ora con i parametri -StartTime ed -EndTime, è possibile definire che nel pool venga effettuata una ricerca tra le 08.00 e le 09.00 del 20 novembre 2012. È possibile impostare il percorso di output in modo da scrivere i risultati in un file denominato c:\\logfile.txt come segue:
    
        Search-CsClsLogging -Pools "pool01.contoso.net" -StartTime "11/20/2012 08:00:00 AM" -EndTime "11/20/2012 09:00:00 AM" -OutputFilePath "C:\Logfiles\logfile.txt"
    

    > [!NOTE]
    > È possibile specificare come stringa di data e ora "data ora" o "ora data". Il comando analizzerà la stringa e utilizzerà i valori relativi alla data e all'ora appropriati.



3.  Se si desidera recuperare i log che iniziano alle 11.00.00 del 20 novembre 2012, definire il parametro -StartTime. Se non viene specificato il parametro -EndTime, l'intervallo di tempo predefinito per la ricerca è pari a 30 minuti e vengono pertanto restituiti i log dei computer o pool specificati dalle 11.00.00 alle 11.30.00.
    
    Ad esempio:
    
        Search-CsClsLogging -Pools "pool01.contoso.net" -StartTime "11/20/2012 11:00:00 AM" -OutputFilePath "C:\Logfiles\logfile.txt"

4.  Per cercare i log all'interno di uno specifico periodo, definire i parametri -StartTime ed -EndTime. Vengono cercati i log dalle 13.00 alle 14.45 del computer edge01.contoso.net.
    
    Ad esempio:
    
        Search-CsClsLogging -Computers "edge01.contoso.net" -StartTime "11/20/2012 1:00:00 PM" -EndTime "11/20/2012 2:45:00 PM" -OutputFilePath "C:\Logfiles\logfile.txt"

## Per eseguire una ricerca avanzata utilizzando altri criteri e opzioni di corrispondenza

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per eseguire un comando per raccogliere le tracce di specifici componenti, digitare quanto segue:
    
        Search-CsClsLogging -Components <components to search on> -OutputFilePath <fully qualified path to output logs>
    
    Ad esempio:
    
        Search-CsClsLogging -Components "SIPStack","S4","UserServices" -OutputFilePath "C:\Logfiles\logfile.txt"
    
    Vengono restituite tutte le voci di log con componenti di traccia per SIPStack, S4 e UserServices in tutti i computer e pool della distribuzione negli ultimi 30 minuti.

3.  Per limitare la ricerca degli stessi componenti solo al pool Front End denominato pool01.contoso.net, digitare:
    
        Search-CsClsLogging -Components "SIPStack","S4","UserServices" -OutputFilePath "C:\Logfiles\logfile.txt"

4.  La logica di ricerca predefinita per i comandi che dispongono di più parametri consiste nell'utilizzo dell'operatore logico OR con ogni parametro definito. Questo comportamento può essere modificato specificando il parametro **-MatchAll**. A tal fine, digitare quanto segue:
    
        Search-CsClsLogging -CallId "d0af828e49fa4dcb99f5f80223a634bc" -Components "SIPStack","S4","UserServices" -MatchAll -OutputFilePath "C:\Logfiles\logfile.txt"

5.  Se è stata impostata l'esecuzione costante degli scenari, come AlwaysOn, o è stato definito uno scenario di lunga durata, è possibile riportare i log del computer locale nella condivisione file. È possibile definire la condivisione file utilizzando il parametro CacheFileNetworkFolder con New-CsClsConfiguration per creare una nuova configurazione e con Set-CsClsConfiguration per modificarne una esistente. Se non si desidera includere la condivisione file nella raccolta dei log per la ricerca, utilizzare il parametro SkipNetworkLogs come segue:
    
        Search-CsClsLogging -Components "SIPStack","S4","UserServices" -StartTime "11/1/2012 00:00:01 AM" -EndTime "11/20/2012 2:45:00 PM" -SkipNetworkLogs -OutputFilePath "C:\Logfiles\logfile.txt"

