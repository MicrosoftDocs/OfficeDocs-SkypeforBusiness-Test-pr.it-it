---
title: New-CsSipProxyTCP
TOCTitle: New-CsSipProxyTCP
ms:assetid: 27600a10-cc00-4be0-ab47-0bb06e65e4cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425745(v=OCS.15)
ms:contentKeyID: 49299985
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyTCP

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo oggetto SipProxy.TCP che può essere utilizzato per configurare una route statica per l'utilizzo di TCP (Transmission Control Protocol) come protocollo di trasporto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyTCP -IPAddress <String>

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 creano un nuovo oggetto trasporto proxy SIP che utilizza TCP come protocollo di trasporto. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsSipProxyTCP** per creare un nuovo oggetto SipProxy.TCP che punta al server dell'hop successivo con l'indirizzo IP 192.168.1.100. Questo oggetto TCP è archiviato nella variabile denominata $tcp.

Dopo che è stato creato l'oggetto SipProxy.TCP, il cmdlet **New-CsSipProxyTransport** consente di creare un oggetto trasporto TCP.

    $tcp = New-CsSipProxyTCP -IPAddress 192.168.1.100
    
    $transport = New-CsSipProxyTransport -TransportChoice $tcp -Port 7500

## Descrizione dettagliata

Quando si invia un messaggio SIP, il messaggio potrebbe dover attraversare molteplici subnet e reti prima di essere recapitato; il percorso seguito dal messaggio è spesso definito route. Nelle reti esistono due tipi di route: dinamiche e statiche. Con il routing dinamico, i server utilizzano algoritmi per determinare la posizione successiva (vale a dire l'hop successivo) a cui dovrebbe essere inoltrato un messaggio. Con il routing statico, i percorsi seguiti dai messaggi sono determinati anticipatamente dagli amministratori di sistema. Quando riceve un messaggio, il server controlla l'indirizzo del messaggio e inoltra il messaggio stesso al server dell'hop successivo configurato anticipatamente da un amministratore. Se la configurazione è corretta, le route statiche aiutano a garantire un recapito tempestivo e accurato dei messaggi, applicando un sovraccarico minimo sui server. Lo svantaggio delle route statiche è dovuto al fatto che i messaggi non vengono reinstradati in modo dinamico se si verifica un errore di rete.

Lync Server consente di impostare le route statiche per i server proxy. Queste route sono costituite da due elementi principali: impostazioni di configurazione dei server proxy (create utilizzando il cmdlet **New-CsProxyConfiguration**) e route proxy SIP. A loro volta, le route proxy SIP dispongono di diverse proprietà. Ogni route ad esempio deve disporre di una proprietà Transport che definisce il protocollo di rete utilizzato per la trasmissione dei messaggi lungo la route.

Lync Server consente di specificare TCP (Transmission Control Protocol) o TLS (Transport Layer Security) come protocollo di trasporto. Se si decide di utilizzare TCP come protocollo, è necessario innanzitutto creare un oggetto TCP utilizzando il cmdlet **New-CsSipProxyTCP**. È quindi possibile utilizzare tale oggetto per specificare il protocollo per l'oggetto Transport creato dal cmdlet **New-CsSipProxyTransport**.

Non è necessario utilizzare il cmdlet **New-CsSipProxyTCP** se si utilizza il cmdlet **New-CsStaticRoute** per creare la route statica.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsSipProxyTCP** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyTCP"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>IPAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo IP del router dell'hop successivo. Ad esempio: -IPAddress 192.168.0.240.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyTCP** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipProxyTCP** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.TCP.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyTLS](new-cssipproxytls.md)  
[New-CsSipProxyTransport](new-cssipproxytransport.md)

