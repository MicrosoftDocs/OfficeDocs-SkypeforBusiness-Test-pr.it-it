---
title: 'Lync Server 2013: Installare i sistemi operativi e il software prerequisito nei server'
TOCTitle: Installare i sistemi operativi e il software prerequisito nei server
ms:assetid: 055991e0-5aeb-43fc-a7ba-d4b02316d73b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398103(v=OCS.15)
ms:contentKeyID: 49299546
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare i sistemi operativi e il software prerequisito nei server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-24_

Dopo aver impostato l'infrastruttura hardware e di sistema, è necessario installare i sistemi operativi Windows e gli aggiornamenti appropriati, oltre a tutti gli altri componenti software prerequisiti in ogni server da distribuire. Sono inclusi i singoli ruoli del server di Lync Server 2013 e gli eventuali server di infrastruttura aggiuntivi o server basati su SQL Server necessari per la distribuzione.


> [!NOTE]
> In questa sezione viene descritta l'installazione dei sistemi operativi e del software prerequisito per i server interni. Se si stanno distribuendo server perimetrali a supporto dell'accesso di utenti esterni, sarà inoltre necessario installare i sistemi operativi e il software prerequisito per tali server, inclusi i server perimetrali e i server proxy inversi. Per informazioni dettagliate sulla preparazione dei server per il supporto dell'accesso di utenti esterni, vedere <A href="lync-server-2013-preparing-for-installation-of-servers-in-the-perimeter-network.md">Preparazione dell'installazione dei server nella rete perimetrale per Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Installare i sistemi operativi Windows nei server

In ogni server da distribuire installare il sistema operativo Windows appropriato come segue:

  - **Server che eseguono Lync Server 2013**   Per informazioni dettagliate sui requisiti dei sistemi operativi per i server che eseguono Lync Server 2013, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa alla supportabilità.

  - **Server di database**    Per informazioni dettagliate sui requisiti dei sistemi operativi per i server di database, inclusi il database back-end, il database di archiviazione e il database di monitoraggio, vedere la documentazione di SQL Server. Per SQL Server 2012, vedere la documentazione online di SQL Server 2012 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=218015\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=218015%26clcid=0x410).


> [!NOTE]
> Se si sta installando Lync Server 2013 in Windows Server&nbsp;2008&nbsp;R2 con SP1, è innanzitutto necessario installare l'aggiornamento descritto nell'articolo 2646886 della Microsoft Knowledge Base, "FIX: Quando un modulo chiama il metodo InsertEntityBody in IIS 7.5 si verifica un danneggiamento dell'heap", all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=3052&amp;clcid=0x410</A>.<BR>È inoltre necessario modificare il Registro di sistema come descritto nell'articolo della Knowledge Base, <A href="http://go.microsoft.com/fwlink/p/?linkid=506893">Gli ID evento 32402 e 61045 vengono registrati nei server Front End di Lync Server 2013 installati in Windows Server 2012 R2</A>.



## Installare Windows Update nei server

Installare gli aggiornamenti seguenti da Windows Update in ogni server:

  - **Aggiornamento di Windows per i server che eseguono Lync Server 2013**   Per informazioni dettagliate sugli aggiornamenti da Windows Update necessari per i server che eseguono Lync Server 2013, vedere [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md) nella documentazione relativa alla pianificazione.

  - **Server di database**   Per informazioni dettagliate sugli aggiornamenti da Windows Update necessari per i server di database, inclusi il database back-end, il database di archiviazione e il database di monitoraggio, vedere la documentazione di SQL Server 2012. Per SQL Server 2012, vedere la documentazione online di SQL Server 2012 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=218015\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=218015%26clcid=0x410).

## Installare altro software prerequisito nei server

Lync Server 2013 richiede l'installazione nei server del software aggiuntivo seguente:

  - **Software prerequisito per i server che eseguono Lync Server 2013**   Gli ulteriori componenti software prerequisiti per i server che eseguono Lync Server 2013 dipendono dal ruolo del server da distribuire. Per informazioni dettagliate sui requisiti software specifici per ogni server, vedere [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md) nella documentazione relativa alla pianificazione.

  - **Windows Identity Foundation**    Lync Server 2013 richiede l'installazione di Windows Identity Foundation per il supporto degli scenari di autenticazione server-server. Per verificare che sia già installato nel computer, accedere al Pannello di controllo, fare clic su **Programmi e funzionalità** , **Visualizza aggiornamenti installati** e cercare in **Microsoft Windows** . Per informazioni dettagliate sull'installazione di Windows Identity Foundation, vedere [http://go.microsoft.com/fwlink/?linkid=204657\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=204657%26clcid=0x410).

  - **Microsoft .NET Framework 4.5**   Per Lync Server 2013 è richiesta l'edizione a 64 bit di Microsoft .NET Framework 4.5.

  - **Software prerequisito per i server di database**   Per informazioni dettagliate sugli aggiornamenti da Windows Update necessari per i server di database, inclusi il database back-end, il database di archiviazione e il database di monitoraggio, vedere la documentazione di SQL Server 2012 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=218015\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=218015%26clcid=0x410).
    

    > [!NOTE]
    > Lync Server 2013 installa automaticamente Microsoft SQL Server 2012 Express in ogni server Standard Edition e in ogni server che esegue Lync Server 2013 in cui sia presente l'archivio di configurazione locale.



  - **Runtime formato Windows Media**   In tutti i Front End Server e i server Standard Edition in cui verrà distribuita la funzionalità per le conferenze deve essere installato Runtime formato Windows Media. Runtime formato Windows Media è necessario per l'esecuzione di file Windows Media Audio (con estensione wma) riprodotti dalle applicazioni Parcheggio di chiamata, Annuncio e Response Group per gli annunci e la musica.
    

    > [!NOTE]
    > Per Windows Server 2012 e Windows Server 2012 R2, Runtime formato Windows Media viene installato con Microsoft Media Foundation.

    

    > [!NOTE]
    > Per Windows Server&nbsp;2008 e Windows Server&nbsp;2008&nbsp;R2, Runtime formato Windows Media viene installato come parte di Windows Desktop Experience. È consigliabile installare Windows Desktop Experience prima di installare Lync Server 2013. Se Lync Server 2013 non trova questo software nel server, verrà richiesto di installarlo e sarà quindi necessario riavviare il server per completare l'installazione.


