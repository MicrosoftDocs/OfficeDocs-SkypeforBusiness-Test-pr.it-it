---
title: Spostare più utenti nel pool pilota
TOCTitle: Spostare più utenti nel pool pilota
ms:assetid: 90d0590c-922c-4933-b778-9dd850b59310
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205096(v=OCS.15)
ms:contentKeyID: 49301324
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare più utenti nel pool pilota

 

_**Ultima modifica dell'argomento:** 2012-10-02_

È possibile spostare più utenti dal pool Lync Server 2010 al pool pilota Lync Server 2013 mediante il Pannello di controllo di Lync Server 2013 o la Lync Server 2013 Management Shell.

## Per spostare più utenti tramite il Pannello di controllo di Lync Server 2013

1.  Aprire il **pannello di controllo di Lync Server**

2.  Fare clic su **Utenti** , fare clic su Cerca e quindi su **Trova** .

3.  Selezionare due utente da spostare nel pool Lync Server 2013. In questo esempio spostiamo gli utenti Chen Yang e Claus Hansen.
    
    ![Spostamento di utenti nel pool di registrazione specifico](images/JJ205096.70d510e1-8e6b-40a5-a80b-27cbc63fc337(OCS.15).jpg "Spostamento di utenti nel pool di registrazione specifico")  

4.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione** .

5.  Nell'elenco a discesa selezionare il pool Lync Server 2013.

6.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione** . Fare clic su OK.
    
    ![Finestra di dialogo per lo spostamento di utenti nel pool di registrazione di destinazione](images/JJ205401.8a375003-dc00-4541-b578-4d88f2010601(OCS.15).png "Finestra di dialogo per lo spostamento di utenti nel pool di registrazione di destinazione")  

7.  Verificare che la colonna **Pool di registrazione** per gli utenti contenga ora il pool Lync Server 2013 indicante che gli utenti sono stati correttamente spostati.

## Per spostare più utenti mediante la Lync Server 2013 Management Shell

1.  Aprire Lync Server 2013 Management Shell.

2.  Alla riga di comando digitare quando segue e sostituire **User1** e **User2** con i nomi degli utenti specifici da spostare e sostituire **pool\_FQDN** con il nome del pool di destinazione. In questo esempio spostiamo gli utenti Hao Chen e Katie Jordan.
    
        Get-CsUser -Filter {DisplayName -eq "User1" -or DisplayName - eq "User2"} | Move-CsUser -Target "pool_FQDN"
    
    ![Esempio di cmdlet Get-CsUser di PowerShell](images/JJ205096.767ff9fc-755d-4a80-a710-5b1367aecbe0(OCS.15).jpg "Esempio di cmdlet Get-CsUser di PowerShell")  

3.  Alla riga di comando digitare quanto segue
    
        Get-CsUser -Identity "User1"

4.  L'identità del **pool di registrazione** deve ora puntare al pool specificato come **pool\_FQDN** nel passaggio precedente. La presenza di questa identità conferma che l'utente è stato correttamente spostato. Ripetere il passaggio per verificare che **User2** sia stato spostato.
    
    ![Output del cmdlet Get-UsUser-Identity di PowerShell](images/JJ205096.8ff04c67-37a0-4156-bfbc-28f9f7b137c8(OCS.15).jpg "Output del cmdlet Get-UsUser-Identity di PowerShell")  

## Per spostare tutti gli utenti contemporaneamente mediante la Lync Server 2013 Management Shell

In questo esempio, tutti gli utenti sono stati restituiti al pool Lync Server 2010 (pool01.contoso.net). Usando la Lync Server 2013 Management Shell, tutti gli utenti verranno spostati contemporaneamente al pool Lync Server 2013 (pool02.contoso.net).

1.  Aprire **Lync Server 2013 Management Shell**.

2.  Nella riga di comando digitare quanto segue:
    
        Get-CsUser -OnLyncServer | Move-CsUser -Target "pool_FQDN"
    
    ![Cmdlet di PowerShell e risultati in Management Shell](images/JJ205096.1e57ccb1-9378-4dc7-82b7-dcaa63a285c6(OCS.15).png "Cmdlet di PowerShell e risultati in Management Shell")  

3.  Eseguire quindi **Get-CsUser** per uno degli utenti pilota.
    
        Get-CsUser -Identity "Hao Chen"

4.  L'identità del **pool di registrazione** per ogni utente punta ora al pool specificato come “pool\_FQDN” nel passaggio precedente. La presenza di questa identità conferma che l'utente è stato spostato.

5.  Inoltre, è possibile visualizzare l'elenco di utenti nel Pannello di controllo di Lync Server 2013 e verificare che il valore del pool di registrazione punti ora al pool Lync Server 2013.
    
    ![Elenco utenti nel Pannello di controllo di Lync Server 2013](images/JJ205096.3f2e87a7-ec59-43c5-82cb-e770108bfb04(OCS.15).jpg "Elenco utenti nel Pannello di controllo di Lync Server 2013")

