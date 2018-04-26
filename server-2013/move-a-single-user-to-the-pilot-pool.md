---
title: Spostare un singolo utente nel pool pilota
TOCTitle: Spostare un singolo utente nel pool pilota
ms:assetid: e9de81a8-40dd-4446-81e7-a2b810eaea50
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205401(v=OCS.15)
ms:contentKeyID: 49302327
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare un singolo utente nel pool pilota

 

_**Ultima modifica dell'argomento:** 2012-09-26_

È possibile spostare un utente dal pool di Lync Server 2010 al pool pilota di Lync Server 2013 utilizzando il Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell. Nell'esempio seguente, nella colonna Pool di registrazione, **pool01.contoso.net** è il pool di Lync Server 2010 e tutti i sei utenti sono connessi a questo pool. Utilizzare le procedure seguenti per spostare un utente nel pool di Lync Server 2013 tramite Pannello di controllo di Lync Server 2013 e Lync Server Management Shell.

## Per spostare un utente tramite il Pannello di controllo di Lync Server 2013

**Elenco di utenti nel Pannello di controllo di Lync Server 2013**

![Pannello di controllo di Lync Server - Finestra di dialogo Spostare un utente](images/JJ721870.a2bce284-0392-4db3-9bb2-9f12699738e7(OCS.15).jpg "Pannello di controllo di Lync Server - Finestra di dialogo Spostare un utente")

1.  Eseguire l'accesso al Front End Server con un account membro del gruppo RTCUniversalServerAdmins oppure membro del ruolo amministrativo CsAdministrator o CsUserAdministrator.

2.  Aprire il **pannello di controllo di Lync Server**.

3.  Fare clic su **Utenti**, fare clic su Cerca e quindi su **Trova**.

4.  Selezionare un utente che si desidera spostare nel pool Lync Server 2013. In questo esempio, verrà spostato l'utente Sara Davis.

5.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione**.

6.  Nell'elenco a discesa selezionare il pool Lync Server 2013.

7.  Fare clic su **Azione** e quindi su **Sposta utenti selezionati nel pool**. Fare clic su **OK**.
    
    ![Finestra di dialogo per lo spostamento di utenti nel pool di registrazione di destinazione](images/JJ205401.8a375003-dc00-4541-b578-4d88f2010601(OCS.15).png "Finestra di dialogo per lo spostamento di utenti nel pool di registrazione di destinazione")  

8.  Verificare che la colonna **Pool di registrazione** per l'utente contenga ora il pool di Lync Server 2013, a indicare che l'utente è stato spostato correttamente.

## Per spostare un utente tramite Lync Server 2013 Management Shell

1.  Aprire Lync Server Management Shell.

2.  Nella riga di comando digitare quanto segue:
    
        Move-CsUser -Identity "David Pelton" -Target "pool02.contoso.net"

3.  Nella riga di comando digitare quanto segue:
    
        Get-CsUser -Identity "David Pelton"

4.  L'identità di **RegistrarPool** ora punta al pool di Lync Server 2013. La presenza di questa identità conferma che l'utente è stato spostato.
    
    ![Output del cmdlet Get-CsUser con filtro Identity](images/JJ205401.bc5d4672-8068-4475-b882-dbd305c801a9(OCS.15).jpg "Output del cmdlet Get-CsUser con filtro Identity")  
    

    > [!NOTE]
    > Per informazioni dettagliate sul cmdlet <STRONG>Get-CsUser</STRONG> , eseguire <STRONG>Get-Help Get-CsUser –Detailed</STRONG>


