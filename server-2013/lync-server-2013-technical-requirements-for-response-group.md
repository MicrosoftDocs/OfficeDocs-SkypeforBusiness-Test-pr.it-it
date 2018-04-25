---
title: 'Lync Server 2013: Requisiti tecnici per i Response Group'
TOCTitle: Requisiti tecnici per i Response Group
ms:assetid: 477488bd-124f-437b-9327-732a0d7271ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204863(v=OCS.15)
ms:contentKeyID: 49300397
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per i Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti i requisiti tecnici per l' applicazione Response Group:

  - Requisiti hardware

  - Requisiti software

  - Requisiti delle porte

  - Requisiti dei file audio

  - Requisiti dello strumento di configurazione Response Group

## Requisiti hardware

L' applicazione Response Group ha gli stessi requisiti hardware dei Front End Server. Per informazioni dettagliate sui requisiti hardware, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa al supporto.

## Requisiti software

L' applicazione Response Group ha gli stessi requisiti del sistema operativo e gli stessi prerequisiti software dei Front End Server. Per informazioni dettagliate sui requisiti software, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa al supporto.

Se si utilizzano file Windows Media Audio (con estensione wma) per gli annunci e la musica di Response Group, in tutti i Front End Server o i server Standard Edition che eseguono l' applicazione Response Group deve essere installato il Runtime formato Windows Media nel caso dei server con Windows Server 2008 R2 o Microsoft Media Foundation nel caso dei server con Windows Server 2012 o Windows Server 2012 R2. Per Windows Server 2008 R2, il Runtime formato Windows Media viene installato come parte dell'esperienza desktop di Windows.

Per ulteriori dettagli sui requisiti audio, vedere "Requisiti dei file audio" più avanti in questa sezione.

## Requisiti delle porte

L' applicazione Response Group utilizza le porte seguenti:

  - **Porta 5071**   Utilizzata per le richieste di attesa SIP

  - **Porta 8404**   Utilizzata per le comunicazioni tra i server
    

    > [!NOTE]
    > Questa porta viene utilizzata per il servizio di ricerca corrispondenze ed è necessaria quando si distribuisce l' applicazione Response Group in un pool con più Front End Server.




> [!NOTE]
> Queste porte sono impostazioni predefinite ed è possibile modificarle utilizzando il cmdlet <STRONG>Set-CsApplicationServer</STRONG>. Per informazioni dettagliate sul cmdlet, vedere la documentazione di Lync Server Management Shell.



## Requisiti dei file audio

L' applicazione Response Group supporta i formati file wave (.wav) e audio Windows Media (.wma) per i messaggi di Response Group, la musica di attesa o le domande IVR (Interactive Voice Response ).

Il formato dei file Windows Media Audio richiede l'installazione del Runtime formato Windows Media nei Front End Server che eseguono Windows Server 2008 R2 e Windows Server 2008. Per ulteriori dettagli, vedere i "Requisiti software" presi già in esame in questa sezione.

## Formati di file wave supportati

Tutti i file wave devono soddisfare i requisiti seguenti:

  - File a 8 bit o a 16 bit

  - LPCM (Linear Pulse Code Modulation), formato A-Law o mu-Law

  - Mono o stereo

  - Massimo 4 MB

Per ottenere prestazioni ottimali con i file wave, è consigliabile utilizzare un file wave mono a 16 bit e 16 kHz.

## Formati di file Windows Media Audio supportati

Se si utilizza un file Windows Media Audio, è consigliabile utilizzare velocità in bit basse e verificare le prestazioni del sistema sotto carico.

Per convertire un file nel formato Windows Media Audio, è possibile utilizzare Microsoft Expression Encoder 4. Per scaricare Expression Encoder 4, vedere [http://go.microsoft.com/fwlink/?linkid=202843\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=202843%26clcid=0x410).

## Requisiti dello strumento di configurazione Response Group

Lo Strumento di configurazione di Response Group supporta le combinazioni di sistemi operativi e Web browser descritte nella tabella seguente.


> [!NOTE]
> Sono supportate sia le versioni a 32 bit che a 64 bit dei sistemi operativi. Sono supportate solo le versioni a 32 bit di Internet Explorer.



### Sistemi operativi e Web browser supportati

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema operativo</th>
<th>Web browser</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista con Service Pack (SP) 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p></td>
</tr>
<tr class="even">
<td><p>Windows 7</p>
<p>Windows 7 con Service Pack 1</p></td>
<td><p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 con Service Pack 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p></td>
</tr>
<tr class="even">
<td><p></p>
<p></p>
<p></p>
<p>Windows Server 2008 R2</p>
<p>Windows Server 2008 R2 con Service Pack 1</p></td>
<td><p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p></td>
</tr>
</tbody>
</table>


## Console degli agenti di Response Group

La console degli agenti supporta le combinazioni di sistemi operativi e Web browser descritte nella tabella seguente.


> [!NOTE]
> Sono supportate sia le versioni a 32 bit che a 64 bit dei sistemi operativi. Sono supportate solo le versioni a 32 bit di Internet Explorer.



### Sistemi operativi e Web browser supportati

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema operativo</th>
<th>Web browser</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista con Service Pack (SP) 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p></td>
</tr>
<tr class="even">
<td><p>Windows 7</p>
<p>Windows 7 con Service Pack 1</p></td>
<td><p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p>
<p>Firefox 10.0</p>
<p>Chrome 18.0</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 con Service Pack 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p>
<p>Windows Server 2008 R2 con Service Pack 1</p></td>
<td><p>Internet Explorer 8 (modalità nativa)</p>
<p>Internet Explorer 9 (modalità nativa)</p>
<p>Firefox 10.0</p>
<p>Chrome 18.0</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td></td>
</tr>
</tbody>
</table>

