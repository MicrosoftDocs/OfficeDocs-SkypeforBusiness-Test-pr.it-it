---
title: "Lync Server 2013: Reimposta i criteri globali per l'accesso utenti esterni"
TOCTitle: Reimpostare i criteri globali per l'accesso degli utenti esterni
ms:assetid: 8207e1b1-de9e-461f-975f-fcc5c526849a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182545(v=OCS.15)
ms:contentKeyID: 49301155
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reimpostare i criteri globali per l'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Non è possibile eliminare completamente i criteri globali. Utilizzando l'opzione **Elimina** per i criteri globali vengono solo reimpostate le impostazioni predefinite dei criteri, che non includono il supporto per opzioni di accesso utente esterno.

## Per reimpostare le impostazioni predefinite dei criteri globali

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e quindi su **Criteri di accesso esterno** .

4.  Nella scheda **Criteri di accesso esterno** fare clic sui criteri globali, quindi su **Modifica** e infine su **Elimina** .

5.  Quando viene richiesto di confermare l'eliminazione, fare clic su **OK** . Verrà visualizzato un messaggio nella parte superiore della pagina che informa che i criteri globali sono stati reimpostati.

## Reimpostazione dei criteri globali di accesso esterno tramite i cmdlet di Windows PowerShell

I criteri globali di accesso esterno possono essere reimpostati tramite Windows PowerShell e il cmdlet Remove-CsExternalAccessPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per reimpostare i criteri globali di accesso esterno

  - Questo comando reimposta i criteri globali per l'accesso esterno
    
        Remove-CsExternalAccessPolicy -Identity "global"

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Remove-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsExternalAccessPolicy).

