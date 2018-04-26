---
title: Configurazione di Windows 8 per le smart card virtuali
TOCTitle: Configurazione di Windows 8 per le smart card virtuali
ms:assetid: 4916c167-4ee3-4f3e-b65c-33e588595112
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308564(v=OCS.15)
ms:contentKeyID: 56269901
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Windows 8 per le smart card virtuali

 

_**Ultima modifica dell'argomento:** 2013-07-03_

Un fattore da valutare per la distribuzione dell'autenticazione a due fattori e della tecnologia per smart card è il costo dell'implementazione. Windows 8 offre numerose nuove funzionalità di sicurezza e, tra queste, una delle caratteristiche più interessanti è il supporto per le smart card virtuali.

Per i computer dotati di chip TPM (Trusted Platform Module) che soddisfa la versione di specifiche 1.2, le organizzazioni possono ora avvalersi dei vantaggi offerti dall'accesso tramite smart card senza alcun ulteriore investimento in termini di hardware. Per ulteriori informazioni, vedere l'articolo relativo all'uso delle smart card virtuali con Windows 8 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=313365](http://go.microsoft.com/fwlink/p/?linkid=313365).

## Per configurare Windows 8 per le smart card virtuali

1.  Accedere al computer Windows 8 usando le credenziali di un utente abilitato per Lync.

2.  Nella schermata Start di Windows 8 spostare il cursore nell'angolo inferiore destro dello schermo.

3.  Selezionare l'opzione **Cerca** e quindi cercare **Prompt dei comandi**.

4.  Fare clic con il pulsante destro del mouse su **Prompt dei comandi** e quindi scegliere **Esegui come amministratore**.

5.  Per aprire la console di gestione TPM (Trusted Platform Module), eseguire il comando seguente:
    
        Tpm.msc

6.  Dalla console di gestione TPM, verificare che la versione delle specifiche TPM sia almeno 1.2
    

    > [!NOTE]
    > Se viene visualizzata una finestra di dialogo che indica che non è possibile trovare un modulo TPM compatibile, verificare che il computer disponga di un modulo TPM compatibile e che questo sia abilitato nel BIOS del sistema.



7.  Chiudere la console di gestione TPM

8.  Dal prompt dei comandi, creare una nuova smart card virtuale digitando il comando seguente:
    
        TpmVscMgr create /name MyVSC /pin default /adminkey random /generate
    

    > [!NOTE]
    > Per specificare un valore PIN personalizzato durante la creazione della smart card virtuale, usare il prompt /pin.



9.  Dal prompt dei comandi, aprire la console di Gestione computer digitando il comando seguente:
    
        CompMgmt.msc

10. Nella console di Gestione computer selezionare **Gestione dispositivi**.

11. Espandere **Lettori smart card**.

12. Verificare che il nuovo lettore di smart card virtuali sia stato creato correttamente.

