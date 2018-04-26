---
title: Aprire gli strumenti di amministrazione di Lync Server
TOCTitle: Aprire gli strumenti di amministrazione di Lync Server
ms:assetid: 8c58de94-9e0a-4368-9e14-9afcaa1142d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg195741(v=OCS.15)
ms:contentKeyID: 49301256
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aprire gli strumenti di amministrazione di Lync Server

 

_**Ultima modifica dell'argomento:** 2012-06-28_

Le procedure descritte in questo argomento consentono di aprire gli strumenti di amministrazione per distribuire e configurare la topologia di Lync Server 2013, nonché risolvere i relativi problemi.

  - Distribuzione guidata

  - Generatore di topologie

  - Pannello di controllo di Lync Server 2013

  - Lync Server 2013 Management Shell

## Distribuzione guidata

La procedura seguente consente di avviare la Distribuzione guidata localmente per aggiungere o rimuovere i file dei componenti di Lync Server 2013.

## Per avviare la Distribuzione guidata di Lync Server 2013

1.  Accedere al computer in cui è installata la Distribuzione guidata di Lync Server come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Distribuzione guidata di Lync Server**.

## Generatore di topologie

La procedura seguente consente di aprire Generatore di topologie per definire i server che si desidera distribuire nella topologia di Lync Server 2013.

## Per aprire Generatore di topologie di Lync Server 2013 per progettare la topologia

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.
    

    > [!NOTE]
    > È possibile definire una topologia utilizzando un account membro del gruppo Users locale, ma per leggere, pubblicare o abilitare una topologia, necessaria per installare Lync Server 2013 in un server, è necessario utilizzare un account membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins e con autorizzazioni di controllo completo (ovvero, lettura, scrittura e modifica) per la condivisione file da utilizzare per l'archivio file per consentire a Generatore di topologie di configurare gli elenchi di controllo di accesso discrezionale necessari oppure un account con diritti utente equivalenti.



2.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

## Pannello di controllo di Lync Server 2013

Le procedure seguenti consentono di aprire il Pannello di controllo di Lync Server 2013 per gestire la configurazione di server, utenti, client e dispositivi nell'ambiente in uso.


> [!NOTE]
> È possibile utilizzare un account utente assegnato al ruolo CsAdministrator per eseguire le attività nel Pannello di controllo di Lync Server 2013. È possibile utilizzare altri ruoli per accedere al Pannello di controllo di Lync Server 2013 per eseguire attività di amministrazione specifiche, a seconda dell'attività che è necessario eseguire. È ad esempio possibile utilizzare il ruolo CSArchivingAdministrator per amministrare l'archiviazione nel Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui ruoli, vedere <A href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</A> nella documentazione relativa alla pianificazione. Per informazioni dettagliate sui ruoli che è possibile utilizzare per eseguire un'attività specifica, vedere la documentazione relativa all'attività.



## Per aprire il Pannello di controllo di Lync Server 2013 da qualsiasi computer all'interno del firewall dell'organizzazione

1.  Da un account utente assegnato al ruolo CsAdministrator o a un altro ruolo con autorizzazioni e diritti utente appropriati per l'attività da eseguire, accedere a qualsiasi computer nella distribuzione interna con una risoluzione minima dello schermo pari a 1024 x 768.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se è stato configurato un URL (Uniform Resource Locator) semplice di amministrazione, è possibile accedere al Pannello di controllo di Lync Server 2013 da un browser Internet in esecuzione in qualsiasi computer interno al firewall dell'organizzazione. Per informazioni dettagliate sulla configurazione dell'URL semplice di amministrazione, vedere <a href="lync-server-2013-planning-for-simple-urls.md">Pianificazione degli URL semplici in Lync Server 2013</a> nella documentazione sulla pianificazione e <a href="lync-server-2013-edit-or-configure-simple-urls.md">Modificare o configurare URL semplici in Lync Server 2013</a> nella documentazione sulla distribuzione.</td>
    </tr>
    </tbody>
    </table>


2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione configurato per l'organizzazione.

## Per aprire il Pannello di controllo di Lync Server 2013 in un computer che esegue Lync Server 2013

1.  Da un account utente membro del ruolo CsAdministrator o di un altro ruolo con autorizzazioni e diritti utente appropriati per l'attività da eseguire, accedere a un computer in cui sia installato Lync Server 2013 o in cui siano almeno presenti gli strumenti di amministrazione di Lync Server 2013. Per configurare le impostazioni, la risoluzione minima dello schermo del computer deve essere pari a 1024x768.

2.  Avviare il Pannello di controllo di Lync Server 2013: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Strumenti di amministrazione**, **Microsoft Lync Server 2013** e quindi fare clic su **Pannello di controllo di Lync Server 2013**.

## Lync Server 2013 Management Shell

La procedura seguente consente di aprire la Lync Server 2013 Management Shell per amministrare server, utenti, client e dispositivi nell'ambiente utilizzando la riga di comando.


> [!NOTE]
> È possibile utilizzare un account utente assegnato al ruolo CsAdministrator per eseguire le attività in Lync Server 2013 Management Shell. È possibile accedere utilizzando altri ruoli per eseguire attività di amministrazione specifiche, a seconda dell'attività che è necessario eseguire. È ad esempio possibile utilizzare CSArchivingAdministrator per eseguire cmdlet correlati all'amministrazione dell'archiviazione. Per informazioni dettagliate sui ruoli, vedere <A href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</A> nella documentazione relativa alla pianificazione. Per informazioni dettagliate sui ruoli che è possibile utilizzare per eseguire un cmdlet specifico, vedere la documentazione relativa al cmdlet.<BR>È inoltre possibile eseguire alcuni cmdlet utilizzando un account utente nel gruppo RTCUniversalServerAdmins, RTCUniversalUserAdmins o RTCUniversalReadOnlyAdmins, a seconda del cmdlet.



## Per aprire la Lync Server 2013 Management Shell.

  - Se si apre una finestra di Windows PowerShell anziché Lync Server 2013 Management Shell, per impostazione predefinita non è possibile eseguire i cmdlet di Lync Server 2013. Per eseguire i cmdlet di Lync Server 2013 da Windows PowerShell, digitare il comando seguente al prompt dei comandi di Windows PowerShell:
    
    `Import-Module Lync`

  - Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

## Vedere anche

#### Attività

[Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md)  

#### Concetti

[Strumenti di amministrazione di Lync Server 2013](lync-server-2013-lync-server-administrative-tools.md)

