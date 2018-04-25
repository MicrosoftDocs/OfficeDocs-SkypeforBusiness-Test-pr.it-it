---
title: Modificare le impostazioni per i file di log di aggiornamento dei dispositivi
TOCTitle: Modificare le impostazioni per i file di log di aggiornamento dei dispositivi
ms:assetid: 9b57f126-1853-43b3-bbd4-06401e6498bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182554(v=OCS.15)
ms:contentKeyID: 49301459
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare le impostazioni per i file di log di aggiornamento dei dispositivi

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile modificare le impostazioni per la modalità di registrazione delle informazioni sull'aggiornamento dei dispositivi nell'organizzazione tramite il Pannello di controllo di Lync Server o Lync Server Management Shell. Nella tabella seguente sono indicate le impostazioni modificabili e gli strumenti che possono essere utilizzati per modificarle.

Le impostazioni di registrazione possono essere modificate e applicate a livello globale o di sito.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Per modificare</th>
<th>Utilizzare</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Le dimensioni massime (in byte) per un file di log</p></td>
<td><p>Pannello di controllo di Lync Server</p>
<p>-oppure-</p>
<p>Lync Server Management Shell</p></td>
</tr>
<tr class="even">
<td><p>La quantità massima di informazioni (in byte) che può essere memorizzata nella cache</p></td>
<td><p>Pannello di controllo di Lync Server</p>
<p>-oppure-</p>
<p>Lync Server Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>La frequenza (in minuti) di scrittura nel log delle informazioni memorizzate nella cache</p></td>
<td><p>Pannello di controllo di Lync Server</p>
<p>-oppure-</p>
<p>Lync Server Management Shell</p></td>
</tr>
<tr class="even">
<td><p>Il periodo di tempo (in giorni) di conservazione dei file di log</p></td>
<td><p>Pannello di controllo di Lync Server</p>
<p>-oppure-</p>
<p>Lync Server Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>Quando (ora del giorno) controllare la presenza di file scaduti da eliminare</p></td>
<td><p>Lync Server Management Shell</p></td>
</tr>
<tr class="even">
<td><p>Quali estensioni dei file di log consentire</p></td>
<td><p>Lync Server Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>Quali tipi di file di log mantenere</p></td>
<td><p>Lync Server Management Shell</p></td>
</tr>
</tbody>
</table>


## Per modificare le impostazioni di registrazione tramite il Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi su **Configurazione log dispositivo**.

3.  Nella pagina **Configurazione log dispositivo** fare doppio clic sulla configurazione che si desidera modificare.

4.  Nella finestra di dialogo **Modifica impostazione log** modificare qualsiasi impostazione tra le seguenti:
    
      - **Dimensioni massime file (byte)**   Specifica le dimensioni massime che un file di log può raggiungere prima di essere eliminato. Il valore predefinito è 1.024.000 byte (1 MB).
    
      - **Dimensioni massime cache (byte)**   Specifica il numero massimo di informazioni (in byte) che la cache del file di log può contenere prima che sia necessario svuotarla e scrivere i dati in un file di log. Il valore predefinito è 512.000 byte (0,5 MB).
    
      - **Minuti per lo scaricamento della cache (1-60)**   Indica la frequenza con cui le informazioni archiviate nella cache del file di log vengono scritte nel file di log effettivo. Dopo la registrazione dei dati, la cache verrà eliminata. Il valore predefinito è 5 minuti.
    
      - **Giorni per la conservazione dei file di log (1-365)**   Specifica il numero di giorni per cui conservare i file di log prima di eliminarli. Il valore predefinito è 10 giorni.

5.  Fare clic su **Commit**.

## Modifica delle impostazioni di registrazione tramite cmdlet di Windows PowerShell

Le impostazioni dei file di log di aggiornamento dei dispositivi possono essere modificate tramite Windows PowerShell e il cmdlet **Set-CsDeviceUpdateConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



Gli esempi seguenti mostrano un paio di modi in cui è possibile utilizzare **Set-CsDeviceUpdateConfiguration** per modificare le impostazioni.

## Per modificare le dimensioni massime del file di log e l'intervallo di pulizia del log

  - Il comando seguente consente di modificare le impostazioni del log di aggiornamento dei dispositivi applicate al sito Redmond. In questo esempio, le dimensioni massime del file di log vengono impostate su 204800 e l'intervallo di pulizia del log viene impostato su 14 giorni.
    
        Set-CsDeviceUpdateConfiguration -Identity "site:Redmond" -MaxLogFileSize 204800 -LogCleanUpInterval 14.00:00:00

## Per modificare l'ora del giorno per la pulizia del log

  - Questo comando consente di impostare l'ora per la pulizia del log per il sito Redmond sulle 3.00.
    
        Set-CsDeviceUpdateConfiguration -Identity "site:Redmond" -LogCleanupTimeOfDay 03:00

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md).

