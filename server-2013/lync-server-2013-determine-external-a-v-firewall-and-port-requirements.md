---
title: 'Lync Server 2013: Determinare i requisiti di porte e firewall A/V esterni'
TOCTitle: Determinare i requisiti di porte e firewall A/V esterni
ms:assetid: 3b849dc7-175d-40d1-820d-80e6ade6d332
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425882(v=OCS.15)
ms:contentKeyID: 49300262
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La comunicazione Audio/Video (A/V) può essere complessa. La natura dei protocolli usati nella comunicazione A/V e il modo in cui client e server usano tali protocolli hanno reso necessario dedicare una sezione speciale alla spiegazione delle differenze tra le versioni client e server.

Usare la tabella di firewall A/V e porte riportata di seguito per determinare i requisiti di firewall e le porte da aprire. Rivedere quindi la terminologia relativa alla conversione NAT (Network Address Translation) perché quest'ultima può essere implementata in diversi modi. Per un esempio dettagliato delle impostazioni delle porte di firewall, vedere le architetture di riferimento in [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md).

### Utilizzo generale dei protocolli per UDP e TCP nel traffico audio/video e multimediale

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Trasporto audio/video</th>
<th>Dati di utilizzo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UDP</p></td>
<td><p>Protocollo del livello trasporto preferito per audio e video</p></td>
</tr>
<tr class="even">
<td><p>TCP</p></td>
<td><p>Protocollo del livello trasporto di fallback per audio e video</p>
<p>Protocollo del livello trasporto richiesto per la condivisione delle applicazioni in Office Communications Server 2007 R2, Lync Server 2010 e Lync Server 2013</p>
<p>Protocollo del livello trasporto richiesto per il trasferimento di file in Lync Server 2010 e Lync Server 2013</p></td>
</tr>
</tbody>
</table>


## Requisiti delle porte dei firewall A/V esterni per l'accesso degli utenti esterni

I requisiti delle porte dei firewall per le interfacce SIP esterne e interne e di conferenza sono uniformi indipendentemente dalla versione del client o del partner federativo.

Non si applicano gli stessi requisiti per l'interfaccia esterna Audio/Video Edge. Per la federazione con Office Communications Server 2007 il servizio A/V Edge richiede che le regole del firewall esterno consentano il flusso bidirezionale del traffico RTP/TCP e RTP/UDP nell'intervallo di porte compreso tra 50.000 e 59.999. Nella tabella precedente si presuppone che Lync Server 2013 sia il partner federativo primario e che sia configurato per comunicare con uno degli altri quattro tipi di partner federativi elencati.

La configurazione dell'intervallo di porte audio/video 50.000-59.999 deve tenere conto del fatto che l'intervallo includerà le porte di origine per le comunicazioni con i partner federativi. In particolare, tenere presente che una comunicazione viene avviata da un partner federativo. La comunicazione dalle porte del servizio A/V Edge nell'intervallo 50.000-59.999 si connetterà alla porta prevista TCP 443 del servizio A/V Edge del partner. Il traffico in ingresso sulla porta TCP 443 del servizio A/V Edge avrà invece una porta di origine nell'intervallo 50.000-59.999.

Firewall e criteri di amministrazione del firewall diversi potrebbero rendere necessaria la sola configurazione delle regole di destinazione oppure sia la configurazione dell'origine che della destinazione. Se i requisiti riguardano solo le porte di destinazione, i requisiti audio/video sono i seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>IP origine</th>
<th>IP destinazione</th>
<th>Porta di destinazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>UDP 3478</p></td>
</tr>
<tr class="odd">
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>UDP 3478</p></td>
</tr>
</tbody>
</table>


Se i criteri richiedono la definizione di regole del firewall sia in ingresso che in uscita, i requisiti audio/video sono i seguenti:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>IP origine</th>
<th>IP destinazione</th>
<th>Porta di origine</th>
<th>Porta di destinazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>TCP 50.000-59.999</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>UDP 3478</p></td>
<td><p>UDP 3478</p></td>
</tr>
<tr class="odd">
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia del servizio A/V Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>UDP 3478</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> Per Microsoft Office Communications Server 2007 è necessaria una configurazione leggermente diversa. L'intervallo di porte TCP e UDP 50.000-59.999 deve essere aperto sia per il traffico in ingresso che in uscita. Questo requisito è valido solo per Office Communicator 2007. Office Communications Server 2007 R2, Lync Server 2010 e Lync Server 2013 richiedono solo l'apertura dell'intervallo TCP 50.000-59.999 in uscita.

## Requisiti NAT per l'accesso degli utenti esterni

Il processo NAT è una funzione di routing, ma è possibile configurare per NAT i dispositivi più recenti come i firewall e addirittura i dispositivi di bilanciamento del carico hardware. Anziché i dispositivi su cui viene eseguito questo processo, questo argomento descrive il comportamento NAT richiesto.

Lync Server 2013  software di comunicazione non supporta il processo NAT per il traffico verso o dall'interfaccia interna perimetrale, mentre per l'interfaccia esterna perimetrale è richiesto il comportamento NAT seguente.

> [!IMPORTANT]  
> È necessario configurare il processo NAT simmetrico per il traffico in ingresso e in uscita. Il processo NAT simmetrico è la tecnologia NAT descritta in questo argomento.

In questa documentazione vengono utilizzati i termini Modifica destinazione e Modifica origine nelle tabelle e nelle figure per definire il comportamento richiesto seguente:

  - **Modifica destinazione**   Processo di modifica dell'indirizzo IP di destinazione nei pacchetti destinati per la rete in cui viene utilizzato NAT. Questo processo è noto anche come trasparenza, port forwarding, modalità NAT di destinazione o modalità Half-NAT.

  - **Modifica origine**   Processo di modifica dell'indirizzo IP di origine nei pacchetti provenienti dalla rete in cui viene utilizzato NAT. Questo processo è noto anche come proxy, SecureNAT, stateful NAT, Source NAT o modalità Full-NAT.

Indipendentemente dalla convenzione utilizzata per i nomi, il comportamento NAT necessario per l'interfaccia esterna del server perimetrale è il seguente:

  - Per il traffico proveniente da Internet e diretto verso l'interfaccia esterna perimetrale:
    
      - Cambiare l'indirizzo IP di destinazione del pacchetto in ingresso dall'indirizzo IP pubblico dell'interfaccia esterna perimetrale nell'indirizzo IP convertito dell'interfaccia esterna perimetrale.
    
      - Lasciare invariato l'indirizzo IP di origine in modo che vi sia una route di ritorno per il traffico.

  - Per il traffico proveniente dall'interfaccia esterna perimetrale e diretto verso Internet:
    
      - Cambiare l'indirizzo IP di origine del pacchetto in uscita dall'interfaccia esterna perimetrale da indirizzo IP convertito a indirizzo IP pubblico dell'interfaccia esterna perimetrale, in modo che l'indirizzo IP dell'interfaccia perimetrale interna non venga esposto e perché si tratta di un indirizzo IP non instradabile.
    
      - Lasciare invariato l'indirizzo IP di destinazione nei pacchetti in uscita.

Nella figura seguente viene mostrata la distinzione tra la modifica dell'indirizzo IP di destinazione (Modifica destinazione) per il traffico in ingresso e la modifica dell'indirizzo IP di origine (Modifica origine) per il traffico in uscita utilizzando l'interfaccia A/V Edge come esempio.

**Modifica dell'indirizzo IP di destinazione (Modifica destinazione) per il traffico in ingresso e modifica dell'indirizzo IP di origine (Modifica origine)**

![Modifica degli indirizzi IP di origine/destinazione](images/Gg425882.0fee7ec5-4cb8-4aff-9164-e7fbab73336d(OCS.15).jpg "Modifica degli indirizzi IP di origine/destinazione")

I punti principali sono i seguenti:

  - Per il traffico in ingresso nel server che esegue il servizio A/V Edge, l'indirizzo IP di origine non cambia, mentre l'indirizzo IP di destinazione cambia da 131.107.155.30 all'indirizzo IP convertito 10.45.16.10.

  - Per il traffico in uscita dal server che esegue il servizio A/V Edge verso la workstation, l'indirizzo IP di origine cambia dall'indirizzo IP pubblico del server nell'indirizzo IP pubblico del server che esegue il servizio A/V Edge. Come IP di destinazione resta l'indirizzo IP pubblico della workstation. Dopo che il pacchetto ha lasciato dal primo dispositivo NAT in uscita, la regola per il dispositivo NAT cambia l'indirizzo IP di origine del server che esegue il servizio A/V Edge dall'indirizzo IP dell'interfaccia esterna (10.45.16.10) nel rispettivo indirizzo IP pubblico (131.107.155.30).

