---
title: 'Lync Server 2013: Supporto per il software client di Lync'
TOCTitle: Supporto per il software client di Lync
ms:assetid: a6851e38-ba9a-4f19-9aa7-d8accf4d62b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412781(v=OCS.15)
ms:contentKeyID: 49301562
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per il software client di Lync in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-07-06_

In questa sezione viene riepilogato il supporto software per Lync 2013 e il componente aggiuntivo per riunioni online per Lync 2013.


> [!NOTE]
> Il componente aggiuntivo per riunioni online per Lync 2013, che supporta la gestione di riunioni dal client di collaborazione e messaggistica di Outlook, viene installato automaticamente con Lync 2013.



### Requisiti software per Lync 2013 e il componente aggiuntivo per riunioni online per Lync 2013

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente del sistema</th>
<th>Requisito minimo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sistema operativo Windows</p></td>
<td><p>Windows 8,1</p>
<p>Windows 8</p>
<p>sistema operativo Windows 7</p>
<p>Windows Server 2008 R2 con il Service Pack più recente</p>

> [!NOTE]
> Lync 2013 e il componente aggiuntivo per riunioni online per Lync 2013 non sono supportati in Windows Vista o Windows XP (qualsias versione).


</td>
</tr>
<tr class="even">
<td><p>Installazione e aggiornamenti</p></td>
<td><p>Diritti e autorizzazioni di amministratore</p></td>
</tr>
<tr class="odd">
<td><p>Browser</p></td>
<td><p>Browser Internet Windows Internet Explorer 10</p>
<p>Browser Internet Internet Explorer 9</p>
<p>Browser Internet Internet Explorer 8</p>
<p>Browser Internet Internet Explorer 7</p>
<p>Mozilla Firefox</p>


> [!NOTE]
> Se si utilizza Lync con Microsoft Exchange Online e nell'organizzazione è stato distribuito un proxy HTTP per l'autenticazione, è necessario Internet Explorer 9 o Internet Explorer 8.


</td>
</tr>
<tr class="even">
<td><p>Integrazione di Microsoft Office</p></td>
<td><p>Per il set completo di funzionalità di integrazione:</p>
<ul>
<li><p>Client di messaggistica e collaborazione Outlook 2013</p></li>
<li><p>Client di messaggistica e collaborazione Outlook 2010</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Integrazione di Microsoft Exchange</p></td>
<td><p>Per il set completo di funzionalità di integrazione:</p>
<ul>
<li><p>Microsoft Exchange Server 2013</p></li>
<li><p>Microsoft Exchange Server 2010</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Sistemi operativi Macintosh

Lync 2013 è disponibile solo per Windows. Lync Server 2013 tuttavia supporta i client seguenti nei computer che eseguono Mac OS 10.5.8 o i sistemi operativi (basati su Intel) con il Service Pack o la versione più recente (il sistema operativo Mac OS 10.9 attualmente non è supportato). Per informazioni dettagliate sulle funzionalità supportate, vedere [Tabelle di confronto dei client per Lync Server 2013](lync-server-2013-desktop-client-comparison-tables.md).

  - Microsoft Lync per Mac 2011 (vedere la guida alla distribuzione di Lync per Mac 2011 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268786\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268786%26clcid=0x410))

  - Microsoft Communicator per Mac 2011 (vedere la guida alla distribuzione di Communicator per Mac 2011 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268787\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268787%26clcid=0x410))

## Browser Lync Web App

Lync Web App supporta combinazioni specifiche di sistemi operativi e browser. Per informazioni dettagliate, vedere [Piattaforme supportate da Lync Web App per Lync Server 2013](lync-server-2013-lync-web-app-supported-platforms.md) nella documentazione relativa alla pianificazione.

## Supporto di Microsoft Office

I client Lync Server 2013 supportano l'integrazione con diverse versioni di Microsoft Office, come riepilogato in questa sezione.

  - Le funzionalità di integrazione di Lync 2013 sono supportate in Outlook 2013 e Microsoft Outlook 2010.

  - Le funzionalità di integrazione di Lync 2013 sono supportate in Microsoft Exchange Server 2013 e Microsoft Exchange Server 2010.

  - Il componente aggiuntivo per riunioni online per Lync 2013 è supportato con Office 2013 e Microsoft Office 2010.

## Utilizzo dei profili obbligatori

Se gli utenti prevedono di utilizzare le funzionalità per conferenze di Lync 2013, è sconsigliabile l'utilizzo dei profili obbligatori di Servizi di dominio Active Directory per eseguire l'accesso al client Lync 2013. Poiché i profili obbligatori sono profili utente di sola lettura, le chiavi dell'infrastruttura a chiave pubblica (PKI) necessarie per le funzionalità per conferenze di Lync 2013 non possono essere salvate nel profilo. Per informazioni dettagliate, vedere l'articolo 2552221 della Microsoft Knowledge Base sugli errori della funzionalità per le conferenze di Lync 2010 quando l'utente esegue l'accesso con un profilo utente obbligatorio all'indirizzo [http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x410).

## Vedere anche

#### Concetti

[Supporto per l'hardware client di Lync in Lync Server 2013](lync-server-2013-lync-client-hardware-support.md)  
[Requisiti video del client Lync per Lync Server 2013](lync-server-2013-lync-client-video-requirements.md)  
[Client supportati dalle distribuzioni precedenti in Lync Server 2013](lync-server-2013-supported-clients-from-previous-deployments.md)

