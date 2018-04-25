---
title: Spostare un singolo utente nel pool pilota
TOCTitle: Spostare un singolo utente nel pool pilota
ms:assetid: 80d5b365-f153-4c61-a148-f9e18ce6e027
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688109(v=OCS.15)
ms:contentKeyID: 49887627
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare un singolo utente nel pool pilota

 

_**Ultima modifica dell'argomento:** 2012-09-28_

È possibile spostare un utente dal pool di Office Communications Server 2007 R2 al pool pilota di Lync Server 2013 utilizzando il Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell. Nell'esempio di seguito, nella colonna Pool di registrazione, **\<Office Communications Server\>** rappresenta il pool di Office Communications Server 2007 R2, al quale sono connessi i sei utenti. Utilizzare le procedure seguenti per spostare un utente dal pool di Lync Server 2013 usando il Pannello di controllo di Lync Server 2013 e Lync Server Management Shell.

![Ricerca di utenti OCS nel Pannello di controllo di Lync Server](images/JJ688109.d2008fd6-868b-4f26-84cf-57bb69e073d3(OCS.15).jpg "Ricerca di utenti OCS nel Pannello di controllo di Lync Server")

## Per spostare un utente tramite il Pannello di controllo di Lync Server 2013

1.  Eseguire l'accesso al Front End Server con un account membro del gruppo RTCUniversalServerAdmins oppure membro del ruolo amministrativo CsAdministrator o CsUserAdministrator.

2.  Aprire il Pannello di controllo di Lync Server.

3.  Fare clic su **Utenti**.

4.  Nella scheda **Ricerca utenti** fare clic sul pulsante **Cerca**.

5.  Fare quindi clic su **Aggiungi filtro**.

6.  Creare un filtro in cui l' **utente di Office Communications Server** sia uguale a **True**.

7.  Fare clic su **Trova** per cercare utenti Office Communications Server 2007 R2 legacy.
    
    ![Ricerca di utenti OCS nel Pannello di controllo di Lync Server](images/JJ688109.09528349-7915-41e1-91b4-6ab5c12b1b38(OCS.15).jpg "Ricerca di utenti OCS nel Pannello di controllo di Lync Server")  

8.  Selezionare un utente che si desidera spostare nel pool Lync Server 2013. In questo esempio, verrà spostato l'utente Sara Davis.

9.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione**.

10. Nell'elenco a discesa selezionare il pool Lync Server 2013.

11. Fare clic su **Azione** e quindi su **Sposta utenti selezionati nel pool**. Fare clic su **OK**.
    
    ![Impostazione del pool di destinazione nella finestra di dialogo Sposta utenti](images/JJ688109.d7dc0759-87c5-4c23-938f-361576621504(OCS.15).jpg "Impostazione del pool di destinazione nella finestra di dialogo Sposta utenti")  

12. Verificare che la colonna **Pool di registrazione** per l'utente contenga ora il pool di Lync Server 2013, a indicare che l'utente è stato spostato correttamente.

## Per spostare un utente tramite Lync Server 2013 Management Shell

1.  Aprire Lync Server Management Shell.

2.  Nella riga di comando digitare quanto segue:
    
        Move-CsLegacyUser -Identity "David Pelton" -Target "pool02.contoso.net"

3.  Nella riga di comando digitare quanto segue:
    
        Get-CsUser -Identity "David Pelton"

4.  L'identità di **RegistrarPool** ora punta al pool di Lync Server 2013. La presenza di questa identità conferma che l'utente è stato spostato.
    
    ![Output del cmdlet Get-CsUser con filtro Identity](images/JJ205401.bc5d4672-8068-4475-b882-dbd305c801a9(OCS.15).jpg "Output del cmdlet Get-CsUser con filtro Identity")  
    

    > [!NOTE]
    > Per informazioni dettagliate sul cmdlet <STRONG>Get-CsUser</STRONG>, eseguire <STRONG>Get-Help Get-CsUser –Detailed</STRONG>


