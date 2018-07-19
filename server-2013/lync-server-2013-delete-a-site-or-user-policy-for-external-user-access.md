---
title: "Lync Server 2013: Eliminare criteri di sito o utente per l'accesso degli utenti esterni"
TOCTitle: Eliminare criteri di sito o utente per l'accesso degli utenti esterni
ms:assetid: 6d907507-825b-4354-9c03-337a459f72de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521013(v=OCS.15)
ms:contentKeyID: 49300907
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare criteri di sito o utente per l'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile eliminare criteri sito o utente elencati nella pagina **Criteri di accesso esterno** del Pannello di controllo di Lync Server. L'eliminazione di criteri globali non ne implica l'effettiva rimozione, ma solo il ripristino delle impostazioni predefinite, che non includono il supporto per alcuna opzione di accesso utente esterno. Per informazioni dettagliate sui criteri globali, vedere [Reimpostare i criteri globali per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-reset-the-global-policy-for-external-user-access.md).

## Per eliminare criteri sito o utente per l'accesso utente esterno

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Fare clic su **Accesso utente esterno** e quindi su **Criteri di accesso esterno** .

4.  Nella scheda **Criteri di accesso esterno** fare clic sui criteri sito o utente che si desidera eliminare, fare clic su **Modifica** e quindi su **Elimina** .

5.  Quando viene richiesto di confermare l'eliminazione, fare clic su **OK** .

## Rimozione dei criteri PIN tramite i cmdlet di Windows PowerShell

È possibile rimuovere i criteri di accesso esterno tramite Windows PowerShell e il cmdlet Remove-CsExternalAccessPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere criteri di accesso esterno specifici

  - Questo comando rimuove i criteri di accesso esterno applicati al sito Redmond:
    
        Remove-CsExternalAccessPolicy -Identity "site:Redmond"

## Per rimuovere tutti i criteri di accesso esterno applicati all'ambito "per utente"

  - Questo comando rimuove tutti i criteri di accesso esterno configurati nell'ambito "per utente":
    
        Get-CsExternalAccessPolicy -Filter "tag:*" | Remove-CsExternalAccessPolicy

## Per rimuovere tutti i criteri di accesso esterno dove l'accesso esterno dell'utente è disattivato

  - Questo comando elimina tutti i criteri di accesso esterno dove l'accesso esterno dell'utente è stato disattivato:
    
        Get-CsExternalAccessPolicy | Where-Object {$_.EnableOutsideAccess -eq $False} | Remove-CsExternalAccessPolicy

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Remove-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsExternalAccessPolicy).

