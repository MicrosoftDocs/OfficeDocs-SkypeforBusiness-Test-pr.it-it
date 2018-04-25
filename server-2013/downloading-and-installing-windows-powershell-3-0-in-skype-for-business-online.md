---
title: 'Lync Online: Download e installazione di Windows PowerShell 3.0'
TOCTitle: Download e installazione di Windows PowerShell 3.0
ms:assetid: 39ae065d-02d7-4ce3-9e6f-6ad550a1777e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362783(v=OCS.15)
ms:contentKeyID: 56269897
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Download e installazione di Windows PowerShell 3.0 in Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Se si utilizza Windows Server 2012, Windows Server 2012 R2, Windows 8 o Windows 8.1, Windows PowerShell 3.0 è già disponibile, in quanto l'applicazione viene preinstallata con questi sistemi operativi.

Se si esegue Windows 7 o Windows Server 2008 R2, è possibile che sia disponibile anche Windows PowerShell 3.0, ma potrebbe essere in esecuzione la versione 2.0 fornita in origine con questi sistemi operativi. Per determinare la versione di Windows PowerShell in uso, eseguire le operazioni seguenti nel computer Windows 7 o Windows Server 2008 R2:

1.  Fare clic sul pulsante **Start**, scegliere Tutti i programmi, fare clic su **Accessori**, su **Windows PowerShell** e quindi su **Windows PowerShell**.

2.  Nella console di Windows PowerShell digitare il comando seguente e premere INVIO:
    
        Get-Host | Select-Object Version

3.  Nella finestra della console verranno visualizzate informazioni simili alle seguenti:
    
        Version
        -------
        3.0

Se il numero di versione restituito è 3.0, è in esecuzione Windows PowerShell 3.0. In caso contrario, sarà necessario installare Windows PowerShell 3.0. È possibile scaricare Windows Management Framework 3.0, che include Windows PowerShell 3.0, dall' [Area download Microsoft](http://www.microsoft.com/en-us/download/details.aspx?id=34595).

Dopo avere verificato che Windows PowerShell 3.0 è installato, accertarsi che Windows PowerShell sia stato configurato per l'esecuzione di script remoti. A questo scopo, avviare Windows PowerShell come amministratore. In Windows 7, Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2 procedere come segue:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Accessori**, **Windows PowerShell**, fare clic con il pulsante destro del mouse su **Windows PowerShell** e quindi scegliere **Esegui come amministratore**.

2.  Se viene visualizzata la finestra di dialogo **Controllo dell'account utente** fare clic su **Sì** per confermare l'intenzione di eseguire Windows PowerShell con credenziali di amministratore.

Se si esegue Windows 8, eseguire invece la procedura seguente:

1.  Accedere alla barra degli accessi, fare clic su **Ricerca** e quindi fare clic con il pulsante destro del mouse su **Windows PowerShell**. Per accedere rapidamente alla barra degli accessi in qualsiasi computer Windows 8 (touchscreen o non touchscreen), tenere premuto il tasto WINDOWS e premere C.

2.  Sulla barra degli strumenti nella parte inferiore dello schermo fare clic su **Esegui come amministratore**.

3.  Se viene visualizzata la finestra di dialogo **Controllo dell'account utente** fare clic su **Sì** per confermare l'intenzione di eseguire Windows PowerShell con credenziali di amministratore.

Dopo avere avviato Windows PowerShell, modificare i criteri di esecuzione per consentire l'uso di script remoti. Nella console di Windows PowerShell digitare il comando seguente e premere INVIO:

    Set-ExecutionPolicy RemoteSigned -Force


> [!NOTE]
> Quando si esegue questo comando, è possibile che venga visualizzato il messaggio di errore seguente:<BR>Set-ExecutionPolicy : Accesso negato alla chiave 'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Micrsoft.PowerShell' del Registro di sistema.<BR>Questo errore si verifica in genere se Windows PowerShell non viene eseguito con credenziali di amministratore. Chiudere la sessione corrente di Windows PowerShell e avviare una nuova sessione come amministratore.



Per verificare che i criteri di esecuzione siano stati configurati correttamente, digitare quanto segue al prompt di Windows PowerShell e premere INVIO:

    Get-ExecutionPolicy

Se viene restituito il valore seguente, la configurazione è corretta:

    RemoteSigned

Se Windows PowerShell 3.0 non è attualmente disponibile, sarà necessario scaricare e installare anche Windows Management Framework 3.0 dall'Area download Microsoft. Questo pacchetto di installazione include Windows PowerShell 3.0 e Gestione remota Windows (WinRM) 3.0 e potrebbe essere necessario se si esegue Windows 7 e non è ancora stato effettuato l'aggiornamento a Windows PowerShell 3.0. Se si esegue Windows Server 2012, Windows Server 2012 R2, Windows 8 o Windows 8.1, non dovrebbe essere necessario installare Windows PowerShell 3.0, perché Windows PowerShell 3.0 viene preinstallato in questi sistemi operativi.

Prima di installare Windows Management Framework 3.0:

  - Assicurarsi di avere scaricato la versione corretta del pacchetto di installazione. Se si esegue la versione a 64 bit di Windows 7, scaricare il file Windows6.1-KB2506143-x64.msu. Per la versione a 32 bit di Windows 7 scaricare invece il file Windows6.1-KB2506143-x86.msu.

  - Se nel computer è in esecuzione Windows 7, assicurarsi di avere installato Windows 7 Service Pack 1.

Se non si è certi della versione di Windows in esecuzione o non si è sicuri di avere installato Windows 7 Service Pack 1, fare clic sul pulsante **Start**, fare clic con il pulsante destro del mouse su **Computer** e quindi scegliere **Proprietà**. Le informazioni sono riportate nella finestra di dialogo Sistema:

![Finestra di dialogo Sistema con le impostazioni](images/Dn362783.30bff2e8-2862-4dd7-828f-43732f4b9314(OCS.15).png "Finestra di dialogo Sistema con le impostazioni")

Per installare Windows Management Framework 3.0, eseguire la procedura seguente:

1.  Fare doppio clic sul file di installazione con estensione MSU ( **Windows6.1-KB2506143-x64.msu** o **Windows6.1-KB2506143-x86.msu**).

2.  Nella pagina **Leggere le condizioni di licenza (1di 1)** della procedura guidata Scarica e installa aggiornamenti fare clic su **Accetto**.

3.  Al termine dell'installazione fare clic su **Riavvia ora** per riavviare il computer.

Dopo il riavvio del computer verificare che sia possibile avviare Windows PowerShell e che l'applicazione possa essere eseguita con credenziali amministrative. A questo scopo:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Accessori**, **Windows PowerShell**, fare clic con il pulsante destro del mouse su **Windows PowerShell** e quindi scegliere **Esegui come amministratore**.

2.  Se viene visualizzata la finestra di dialogo Controllo dell'account utente fare clic su **Sì** per confermare l'intenzione di eseguire Windows PowerShell con credenziali di amministratore.

Quando viene visualizzata la console di Windows PowerShell verificare che il servizio WinRM sia in esecuzione e configurato correttamente. Per verificare se il servizio è in esecuzione, digitare il comando seguente al prompt di Windows PowerShell e premere INVIO:

    Get-Service winrm

Verranno visualizzate le informazioni relative al servizio WinRM:

    Status   Name               DisplayName
    ------   ----               -----------
    Running  winrm              Windows Remote Management (WS-Manag...

Se la voce Stato relativa al servizio non è "In esecuzione", avviare il servizio WinRM digitando il comando seguente e premendo INVIO:

    Start-Service winrm

Una volta avviato il servizio, eseguire il comando seguente per verificare che WinRM usi l'autenticazione di base:

    winrm set winrm/config/client/auth '@{Basic="True"}'

Verranno visualizzate informazioni simili alle seguenti:

    Auth
        Basic = true
        Digest = true
        Kerberos = true
        Negotiate = true
        Certificate = true
        CredSSP = false

Se l'autenticazione di base è stata impostata su true, è possibile iniziare a usare Windows PowerShell per connettersi a Skype for Business online.

