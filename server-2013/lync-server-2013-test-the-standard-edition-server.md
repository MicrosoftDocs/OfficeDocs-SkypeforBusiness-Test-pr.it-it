---
title: 'Lync Server 2013: Testare il server Standard Edition'
TOCTitle: Testare il server Standard Edition
ms:assetid: b6ef67bb-9665-43e4-b8b3-eac8898eebf6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412890(v=OCS.15)
ms:contentKeyID: 49301749
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testare il server Standard Edition in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Nella procedura seguente viene illustrato come testare la distribuzione di un server Standard Edition.

## Per testare la distribuzione di un server Standard Edition

1.  Utilizzare Utenti e computer Active Directory per aggiungere l'oggetto utente di Active Directory del ruolo di amministratore per la distribuzione di Lync Server 2013 (in cui è installato il Pannello di controllo di Lync Server) al gruppo **CSAdministrator**.

2.  Se l'oggetto utente è connesso, disconnettersi e rieseguire l'accesso per registrare la nuova assegnazione al gruppo.
    

    > [!NOTE]
    > L'account utente non può essere l'amministratore locale del server che esegue Lync Server 2013 Standard Edition. Se non si aggiungono gli utenti e i gruppi appropriati al gruppo CsAdministors, verrà visualizzato un errore all'apertura del Pannello di controllo di Lync Server 2013 con il messaggio "Non autorizzato: accesso negato a causa di un errore dell'autorizzazione di controllo di accesso basato su ruoli (RBAC)".



3.  Utilizzare l'account amministrativo per accedere al computer in cui è installato il Pannello di controllo di Lync Server.

4.  Avviare il Pannello di controllo di Lync Server e specificare le credenziali, se richieste. Nel Pannello di controllo di Lync Server 2013 verranno visualizzate informazioni sulla distribuzione.

5.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi verificare che lo stato del servizio sia un'icona di computer con una freccia verde e che sia presente un segno di spunta verde accanto a ogni ruolo del server di Lync Server distribuito e portato online.

6.  Sulla barra di spostamento sinistra fare clic su **Utenti** e quindi abilitare i due utenti per Lync Server 2013.

7.  Connettere un utente a un computer appartenente al dominio e l'altro utente a un altro computer nel dominio.

8.  Installare Lync Server 2013 in ognuno dei due computer client e quindi verificare che entrambi gli utenti possano accedere a Lync Server 2013 e scambiarsi messaggi istantanei.

## Vedere anche

#### Concetti

[Distribuzione di client e dispositivi in Lync Server 2013](lync-server-2013-deploying-clients-and-devices.md)

