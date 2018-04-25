---
title: "Lync Server 2013: Requisiti tecnici per l'applicazione Annuncio"
TOCTitle: Requisiti tecnici per l'applicazione Annuncio
ms:assetid: fbd8c204-3765-4b22-a0c9-a781b5126366
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205413(v=OCS.15)
ms:contentKeyID: 49302558
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per l'applicazione Annuncio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

In questa sezione vengono descritti i requisiti tecnici per l' applicazione Annuncio:

  - Requisiti hardware

  - Requisiti software

  - Requisiti delle porte

  - Requisiti dei file audio

## Requisiti hardware

L' applicazione Annuncio ha gli stessi requisiti hardware dei Front End Server. Per informazioni dettagliate sui requisiti hardware, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa al supporto.

## Requisiti software

L' applicazione Annuncio ha gli stessi requisiti del sistema operativo e gli stessi prerequisiti software dei Front End Server. Per informazioni dettagliate sui requisiti software, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa al supporto.

Tutti i server Front End Server o Standard Edition che eseguono l' applicazione Annuncio devono aver installato Runtime formato Windows Media per i server in cui è in esecuzione Windows Server 2008 R2 o Microsoft Media Foundation per i server in cui è in esecuzione Windows Server 2012 o Windows Server 2012 R2. Per Windows Server 2008 R2, Runtime formato Windows Media viene installato insieme a Windows Desktop Experience. Runtime formato Windows Media o Microsoft Media Foundation sono necessari per i file in formato WMA (Windows Media Audio) che l' applicazione Annuncio utilizza per riprodurre annunci o musica.

## Requisiti delle porte

L' applicazione Annuncio utilizza le porte seguenti:

  - **Porta 5071**   Utilizzata per le richieste di attesa SIP


> [!NOTE]
> Questa porta è l'impostazione predefinita ed è possibile modificarla utilizzando il cmdlet <STRONG>Set-CsApplicationServer</STRONG>. Per informazioni dettagliate sul cmdlet, vedere la documentazione di Lync Server Management Shell.



## Requisiti dei file audio

L' applicazione Annuncio supporta i formati di file WAV (Wave) e WMA (Windows Media Audio) per la musica e gli annunci. I requisiti dei file audio per l' applicazione Annuncio sono analoghi a quelli per l' applicazione Response Group. Per informazioni dettagliate, vedere [Requisiti tecnici per i Response Group in Lync Server 2013](lync-server-2013-technical-requirements-for-response-group.md).

