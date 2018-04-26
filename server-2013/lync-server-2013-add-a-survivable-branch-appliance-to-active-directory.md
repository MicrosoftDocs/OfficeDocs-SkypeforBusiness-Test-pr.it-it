---
title: 'Lync Server 2013: Aggiungere un Survivable Branch Appliance ad Active Directory'
TOCTitle: Aggiungere un Survivable Branch Appliance ad Active Directory
ms:assetid: 3e63507c-d60b-40ec-8bbe-586b1d707c3e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425906(v=OCS.15)
ms:contentKeyID: 49300298
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere un Survivable Branch Appliance ad Active Directory in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-23_

Se si intende distribuire una Survivable Branch Appliance, sarà necessario aggiungere la Survivable Branch Appliance a Servizi di dominio Active Directory. Eseguire questa procedura nel sito centrale.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Eseguire questa procedura solo se si desidera distribuire un Survivable Branch Appliance. Non eseguirla invece se si distribuisce un Survivable Branch Server.</td>
</tr>
</tbody>
</table>


## Per aggiungere un Survivable Branch Appliance a Servizi di dominio Active Directory

1.  Eseguire l'accesso a un server membro come membro del gruppo Enterprise Admins.

2.  Fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **Utenti e computer di Active Directory** .

3.  Scegliere **Nuovo** dal menu **Azioni** e quindi fare clic su **Computer** .

4.  Nella finestra di dialogo **Nuovo computer** digitare un nome per l'oggetto computer Survivable Branch Appliance, ad esempio BranchOffice1, e quindi fare clic su **Cambia** .

5.  Nella finestra di dialogo **Seleziona utente o gruppo** aggiungere il gruppo RTCUniversalSBATechnicians e quindi fare clic su **OK** .
    

    > [!NOTE]
    > Un membro del gruppo RTCUniversalSBATechnicians nel sito di succursale aggiungerà successivamente questo dispositivo al dominio.



6.  Fare clic su **OK** per salvare l'oggetto computer Survivable Branch Appliance.

7.  Fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **ADSI Edit** .

8.  In **ADSI Edit** fare clic con il pulsante destro del mouse sull'oggetto computer creato nei passaggi precedenti e quindi scegliere **Properties** .

9.  Nell'elenco degli attributi fare clic su **servicePrincipalName** e quindi su **Edit** .

10. Nel campo **Value to add** digitare HOST/\<FQDN SBA\> dove \<FQDN SBA\> è il nome di dominio completo (FQDN) del Survivable Branch Appliance. Digitare ad esempio **HOST/BranchOffice1.contoso.com** .

11. Fare clic su **OK** per salvare l'impostazione dell'attributo **servicePrincipalName** e quindi su **OK** per salvare le proprietà dell'oggetto computer.

12. In **Utenti e computer di Active Directory** fare clic con il pulsante destro del mouse su **Utenti** , scegliere **Nuovo** e quindi fare clic su **Utente** .

13. Immettere le informazioni nella procedura guidata per la creazione di un account utente di dominio per un tecnico Survivable Branch Appliance.

14. In **Utenti e computer di Active Directory** fare clic su **Utenti** , fare clic con il pulsante destro del mouse sull'oggetto utente e quindi scegliere **Aggiungi a un gruppo** .

15. In **Immettere i nomi degli oggetti da selezionare** digitare **RTCUniversalSBATechnicians** e quindi fare clic su **OK** .

16. Ripetere i passaggi 12-15 per ogni tecnico del sito di succursale.

**Passaggio successivo**: [Aggiungere siti di succursale alla topologia in Lync Server 2013](lync-server-2013-add-branch-sites-to-your-topology.md)

