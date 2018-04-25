---
title: Spostare più utenti nel pool pilota
TOCTitle: Spostare più utenti nel pool pilota
ms:assetid: 9492797f-2a26-4773-8ad2-97cb53fa68fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688143(v=OCS.15)
ms:contentKeyID: 49887663
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare più utenti nel pool pilota

 

_**Ultima modifica dell'argomento:** 2012-10-02_

È possibile spostare più utenti dal pool Office Communications Server 2007 R2 al pool pilota Lync Server 2013 mediante il Pannello di controllo di Lync Server 2013 o la Lync Server 2013 Management Shell.

## Per spostare più utenti tramite il Pannello di controllo di Lync Server 2013

1.  Aprire il **pannello di controllo di Lync Server**

2.  Nella scheda **Ricerca utenti** fare clic sul pulsante **Cerca**.

3.  Fare quindi clic su **Aggiungi filtro**.

4.  Creare un filtro in cui l' **utente di Office Communications Server** sia uguale a **True**.

5.  Fare clic su **Trova** per cercare utenti Office Communications Server 2007 R2 legacy.

6.  Selezionare due utente da spostare nel pool Lync Server 2013. In questo esempio spostiamo gli utenti Chen Yang e Claus Hansen.
    
    ![Elenco utenti visualizzato durante la ricerca degli utenti OCS](images/JJ688143.76beb4fa-72e0-41ef-b96e-3553e96645c0(OCS.15).jpg "Elenco utenti visualizzato durante la ricerca degli utenti OCS")  

7.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione** .

8.  Nell'elenco a discesa selezionare il pool Lync Server 2013.

9.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione** . Fare clic su OK.
    
    ![Finestra di dialogo per lo spostamento di utenti nel pool di registrazione di destinazione](images/JJ205401.8a375003-dc00-4541-b578-4d88f2010601(OCS.15).png "Finestra di dialogo per lo spostamento di utenti nel pool di registrazione di destinazione")  

10. Verificare che la colonna **Pool di registrazione** per gli utenti contenga ora il pool Lync Server 2013 indicante che gli utenti sono stati correttamente spostati.

## Per spostare più utenti mediante la Lync Server 2013 Management Shell

1.  Aprire Lync Server 2013 Management Shell.

2.  Alla riga di comando digitare quando segue e sostituire **User1** e **User2** con i nomi degli utenti specifici da spostare e sostituire **pool\_FQDN** con il nome del pool di destinazione. In questo esempio spostiamo gli utenti Hao Chen e Katie Jordan.
    
        Get-CsUser -Filter {DisplayName -eq "User1" -or DisplayName - eq "User2"} | Move-CsLegacyUser -Target "pool_FQDN"
    
    ![Cmdlet di esempio per spostare un utente legacy](images/JJ688143.57cfc28e-3df5-459f-83ef-8b0edf182a25(OCS.15).jpg "Cmdlet di esempio per spostare un utente legacy")  

3.  Alla riga di comando digitare quanto segue
    
        Get-CsUser -Identity "User1"

4.  L'identità del **pool di registrazione** deve ora puntare al pool specificato come **pool\_FQDN** nel passaggio precedente. La presenza di questa identità conferma che l'utente è stato correttamente spostato. Ripetere il passaggio per verificare che **User2** sia stato spostato.
    
    ![Output del cmdlet Get-UsUser-Identity di PowerShell](images/JJ205096.8ff04c67-37a0-4156-bfbc-28f9f7b137c8(OCS.15).jpg "Output del cmdlet Get-UsUser-Identity di PowerShell")  

## Per spostare tutti gli utenti contemporaneamente mediante la Lync Server 2013 Management Shell

In questo esempio, tutti gli utenti sono stati restituiti al pool Office Communications Server 2007 R2 (pool01.contoso.net). Usando la Lync Server 2013 Management Shell, tutti gli utenti verranno spostati contemporaneamente al pool Lync Server 2013 (pool02.contoso.net).

1.  Aprire **Lync Server 2013 Management Shell**.

2.  Nella riga di comando digitare quanto segue:
    
        Get-CsUser -OnOfficeCommunicationServer | Move-CsLegacyUser -Target "pool_FQDN"
    
    ![Cmdlet di esempio per spostare tutti gli utenti legacy di un pool](images/JJ688143.e6a2d578-296e-476c-bd45-d757917ea853(OCS.15).jpg "Cmdlet di esempio per spostare tutti gli utenti legacy di un pool")  

3.  Eseguire quindi **Get-CsUser** per uno degli utenti pilota.
    
        Get-CsUser -Identity "Hao Chen"

4.  L'identità del **pool di registrazione** per ogni utente punta ora al pool specificato come “pool\_FQDN” nel passaggio precedente. La presenza di questa identità conferma che l'utente è stato spostato.

5.  Inoltre, è possibile visualizzare l'elenco di utenti nel Pannello di controllo di Lync Server 2013 e verificare che il valore del pool di registrazione punti ora al pool Lync Server 2013.
    
    ![Elenco utenti nel Pannello di controllo di Lync Server 2013](images/JJ205096.3f2e87a7-ec59-43c5-82cb-e770108bfb04(OCS.15).jpg "Elenco utenti nel Pannello di controllo di Lync Server 2013")

