---
title: 'Lync Server 2013: Requisiti tecnici per il parcheggio di chiamata'
TOCTitle: Requisiti tecnici per il parcheggio di chiamata
ms:assetid: 38bcf302-2b72-4492-9266-f6dc31b566e1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204818(v=OCS.15)
ms:contentKeyID: 49300213
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per il parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

In questa sezione vengono descritti i requisiti tecnici seguenti per il Parcheggio di chiamata:

  - Requisiti hardware

  - Requisiti software

  - Requisiti delle porte

  - Requisiti dei file audio

## Requisiti hardware

L' applicazione Parcheggio di chiamata ha gli stessi requisiti hardware dei Front End Server. Per informazioni dettagliate sui requisiti hardware, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa al supporto.

## Requisiti software

L' applicazione Parcheggio di chiamata ha gli stessi requisiti del sistema operativo e gli stessi prerequisiti software dei Front End Server. Per informazioni dettagliate sui requisiti software, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa al supporto.

In tutti i Front End Server e i server Standard Edition in cui è distribuita l' applicazione Parcheggio di chiamata deve essere installato Runtime formato Windows Media per i server che eseguono Windows Server 2008 R2 o Microsoft Media Foundation per i server che eseguono Windows Server 2012 o Windows Server 2012 R2. Per Windows Server 2008 R2, Runtime formato Windows Media è installato come parte dell'esperienza desktop di Windows. Per i file Windows Media Audio (con estensione wma) riprodotti dal Parcheggio di chiamata per la musica in attesa sono richiesti Runtime formato Windows Media o Microsoft Media Foundation.

## Requisiti delle porte

L' applicazione Parcheggio di chiamata utilizza le porte seguenti:

  - **Porta 5075**   Usata per le richieste di attesa SIP.


> [!NOTE]
> Questa porta è un'impostazione predefinita che può essere modificata usando il cmdlet <STRONG>Set-CsApplicationServer</STRONG>. Per informazioni dettagliate su questo cmdlet, vedere la documentazione di Lync Server Management Shell.



## Requisiti dei file audio

L' applicazione Parcheggio di chiamata supporta solo file audio Windows Media (.wma) per la musica di attesa. Per personalizzare i file per la musica di attesa, è possibile usare Microsoft Expression Encoder 4. Per scaricare Expression Encoder 4, vedere "Expression Encoder 4" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202843](http://go.microsoft.com/fwlink/p/?linkid=202843). Utilizzare lo strumento per convertire il file in un formato wma. Il formato consigliato per i file della musica di attesa di Parcheggio di chiamata è Media Audio 9, 44 kHz, 16 bit, Mono, CBR, 32 kbps.


> [!NOTE]
> Il file convertito viene riprodotto nel telefono solo a 16 kHz, anche se è stato registrato a 44 kHz.


