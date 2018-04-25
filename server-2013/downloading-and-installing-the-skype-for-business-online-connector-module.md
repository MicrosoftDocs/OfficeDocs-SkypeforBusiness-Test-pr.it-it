---
title: Download e installazione del modulo del connettore di Lync Online
TOCTitle: Download e installazione del modulo del connettore di Lync Online
ms:assetid: a0c87219-b642-4201-85d4-a85c2163d1eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362829(v=OCS.15)
ms:contentKeyID: 56269966
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Download e installazione del modulo del connettore di Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Il modulo del connettore di Skype for Business online include il cmdlet **New-CsOnlineSession**, che consente di creare una sessione di Windows PowerShell remota che si connette a Skype for Business online. Questo modulo, supportato solo nei computer a 64 bit (vedere [Configurazione del computer per la gestione di Lync Online](configuring-your-computer-for-skype-for-business-online-management.md) per altre informazioni), può essere scaricato dall'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=294688](http://go.microsoft.com/fwlink/?linkid=294688). Scaricare il file LyncOnlinePowershell.exe e completare la procedura seguente:

1.  Fare doppio clic sul file **LyncOnlinePowershell.exe**.

2.  Nella pagina **Microsoft Software License Terms** della procedura guidata Skype for Business online Tenant PowerShell Setup selezionare **I accept the terms in the License Agreement** e quindi fare clic su **Install**. Se viene visualizzata la finestra di dialogo **User Account Control**, fare clic su **Yes** per continuare l'installazione.

3.  Nella pagina **Completed the Microsoft Lync Online, Tenant PowerShell Setup** fare clic su **Finish**.

Il programma di installazione copia il modulo del connettore di Skype for Business online (e il cmdlet **New-CsOnlineSession**) nel computer locale. Per accedere al modulo, avviare una sessione di Windows PowerShell con credenziali di amministratore, quindi eseguire il comando seguente:

    Import-Module LyncOnlineConnector

Se si vuole evitare di digitare questo comando ogni volta che si avvia Windows PowerShell, è possibile aggiungerlo al profilo di Windows PowerShell, digitando il comando seguente al prompt di Windows PowerShell e premendo INVIO:

    notepad.exe $profile

Quando viene visualizzato il Blocco note, aggiungere la riga seguente in fondo ai comandi eventualmente già inclusi nel profilo:

    Import-Module LyncOnlineConnector

Salvare il file. Al successivo avvio di Windows PowerShell, il modulo del connettore di Skype for Business online viene importato automaticamente. Tenere presente che se non si esegue Windows PowerShell con credenziali di amministratore, viene visualizzato un messaggio di errore e il modulo non viene caricato.

Oltre al modulo del connettore di Skype for Business online, LyncOnlinePowershell.exe installa anche due componenti aggiuntivi: .NET Framework 4.5 e Microsoft Visual C++ 2012 Redistributable (x64) Package (versione 11.0.50727). .NET Framework 4.5 fornisce l'infrastruttura usata per la creazione e l'esecuzione di applicazioni .NET, incluso Windows PowerShell. Visual C++ Redistributable Package installa i componenti di runtime di Visual C++ per i computer in cui non è installato Microsoft Visual Studio 2012.

## Vedere anche

#### Concetti

[Configurazione del computer per la gestione di Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

