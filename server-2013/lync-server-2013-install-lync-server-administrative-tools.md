---
title: 'Lync Server 2013: Installare gli strumenti di amministrazione di Lync Server'
TOCTitle: Installare gli strumenti di amministrazione di Lync Server
ms:assetid: 842b85e4-2eeb-464f-b1c1-ceb8cc04f8d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398665(v=OCS.15)
ms:contentKeyID: 49301181
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare gli strumenti di amministrazione di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In questo argomento viene descritto come installare gli strumenti di amministrazione necessari per distribuire e gestire Lync Server 2013. Gli strumenti di amministrazione vengono installati per impostazione predefinita in ogni server che esegue Lync Server 2013. È inoltre possibile installare gli strumenti di amministrazione in altri computer, ad esempio console di amministrazione dedicate. È consigliabile installare gli strumenti di amministrazione in un computer nello stesso dominio o foresta della distribuzione di Lync Server 2013 che si sta creando, perché in questo modo si garantisce che i passaggi di preparazione di Servizi di dominio Active Directory siano già completati. Questo consente l'utilizzo, in un secondo momento, degli strumenti di amministrazione nel computer per pubblicare la topologia.

Prima di installare o utilizzare gli strumenti di amministrazione di Lync Server 2013, analizzare i requisiti relativi a infrastruttura, sistema operativo e diritti di amministratore. Per informazioni dettagliate sui requisiti dell'infrastruttura, vedere [Requisiti dell'infrastruttura degli Strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-infrastructure-requirements.md). Per informazioni dettagliate sui requisiti di sistema operativo e software per l'installazione degli strumenti di amministrazione di Lync Server 2013, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md), [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md) e [Requisiti e supporto per i server aggiuntivi in Lync Server 2013](lync-server-2013-additional-server-support-and-requirements.md). Per informazioni dettagliate sulle autorizzazioni e sui diritti utente necessari per installare gli strumenti, vedere [Autorizzazioni e diritti di amministratore necessari per l'installazione e l'amministrazione di Lync Server 2013](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md).

> [!IMPORTANT]  
> Se l'organizzazione richiede che Internet Information Services (IIS) e tutti i servizi Web si trovino in un'unità diversa dall'unità di sistema, è possibile modificare il percorso di installazione per i file di Lync Server nella finestra di dialogo del programma di installazione. Se si installano i file di installazione, incluso OCSCore.msi, in questo percorso, anche gli altri file di Lync Server 2013 verranno distribuiti in questa unità.

## Per installare gli strumenti di amministrazione di Lync Server 2013

1.  Eseguire l'accesso come amministratore locale (requisito minimo) al computer in cui si desidera installare gli strumenti di amministrazione. Se si è connessi come utente standard al sistema operativo Windows Vista o Windows 7 e il controllo dell'account utente è abilitato, verrà richiesto di specificare nome utente e password di amministratore locale o di un account di dominio equivalente.

2.  Individuare il supporto di installazione nel computer e quindi fare doppio clic su \\Setup\\amd64\\Setup.exe.

3.  Se viene chiesto di installare Microsoft Visual C++ 2008 Distributable, fare clic su **Sì** .

4.  Nella pagina **Percorso di installazione di Microsoft Lync Server 2013**, fare clic su **OK** . Sostituire il percorso indicato con un altro percorso o un'altra unità se è necessario installare i file in una diversa posizione.
    
    > [!IMPORTANT]  
    > Se l'organizzazione richiede che Internet Information Services (IIS) e tutti i servizi Web si trovino in un'unità diversa dall'unità di sistema, è possibile modificare il percorso di installazione per i file di Lync Server 2013 nella finestra di dialogo del programma di installazione. Se si installano i file di installazione, incluso OCSCore.msi, in questo percorso, anche gli altri file di Lync Server 2013 verranno distribuiti in questa unità.

5.  Nella pagina **Contratto di licenza con l'utente finale** leggere le condizioni di licenza, fare clic su **Accetto** e quindi su **OK** . Questo passaggio è obbligatorio per poter continuare.

6.  Nella pagina **Distribuzione guidata di Microsoft Lync Server 2013** fare clic su **Installa strumenti di amministrazione**.

7.  Al termine dell'installazione fare clic su **Esci** .

## Vedere anche

#### Attività

[Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md)  

#### Concetti

[Strumenti di amministrazione di Lync Server 2013](lync-server-2013-lync-server-administrative-tools.md)

