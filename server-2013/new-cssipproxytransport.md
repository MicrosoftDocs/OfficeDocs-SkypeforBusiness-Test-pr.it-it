---
title: New-CsSipProxyTransport
TOCTitle: New-CsSipProxyTransport
ms:assetid: 68587257-d666-429a-bf2d-f8a2b46f1f09
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398489(v=OCS.15)
ms:contentKeyID: 49300843
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyTransport

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Specifica il protocollo di trasmissione da utilizzare in una route statica. Lync Server consente di scegliere tra TCP (Transmission Control Protocol) o TLS (Transport Layer Security) come protocollo di trasmissione per una route. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyTransport -Port <UInt16> -TransportChoice <ITransportChoice>

## Esempi

## ESEMPIO 1

Con i comandi mostrati nell'esempio 1 viene creato un nuovo oggetto trasporto proxy SIP che utilizza TLS come protocollo di trasporto. Poiché il protocollo TLS richiede un certificato da utilizzare per l'autenticazione, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsSipProxyUseDefaultCert** per configurare un nuovo oggetto SipProxy.UseDefaultCert. Questo oggetto, archiviato in una variabile denominata $cert, indica a Lync Server di utilizzare il certificato predefinito per il trasporto TLS. Dopo aver creato l'oggetto UseDefaultCert, è possibile chiamare il cmdlet **New-CsSipProxyTLS** per creare un nuovo oggetto SipProxy.TLS, che utilizza il certificato predefinito e punta ad atl-proxy-001.litwareinc.com come nome di dominio completo (FQDN) per il server dell'hop successivo.

    $cert = New-CsSipProxyUseDefaultCert
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com
    
    $transport = New-CsSipProxyTransport -TransportChoice $tls -Port 7500

## ESEMPIO 2

Con i comandi mostrati nell'esempio 2 viene creato un nuovo oggetto trasporto proxy SIP che utilizza TCP come protocollo di trasporto. A tale scopo, nel primo comando nell'esempio viene utilizzato il cmdlet **New-CsSipProxyTCP** per creare un nuovo oggetto SipProxy.TCP che punta al server dell'hop successivo con indirizzo IP 192.168.1.100. Questo oggetto TCP è archiviato in una variabile denominata $tcp.

Una volta creato l'oggetto SipProxy.TCP, è possibile chiamare il cmdlet **New-CsSipProxyTransport** per creare un oggetto trasporto TCP.

    $tcp = New-CsSipProxyTCP -IPAddress 192.168.1.100
    
    $transport = New-CsSipProxyTransport -TransportChoice $tcp -Port 7500

## Descrizione dettagliata

Quando si invia un messaggio SIP, è possibile che il messaggio debba attraversare diverse subnet e reti prima di essere recapitato. Il percorso seguito dal messaggio è spesso definito route. Nelle reti esistono due tipi di route: dinamica e statica. Con il routing dinamico, i server utilizzano algoritmi per determinare la posizione successiva (vale a dire l'hop successivo) a cui dovrebbe essere inoltrato un messaggio. Con il routing statico, i percorsi seguiti dai messaggi sono determinati anticipatamente dagli amministratori di sistema. Quando riceve un messaggio, il server controlla l'indirizzo del messaggio e inoltra il messaggio stesso al server dell'hop successivo configurato anticipatamente da un amministratore. Se la configurazione è corretta, le route statiche aiutano a garantire un recapito tempestivo e accurato dei messaggi, applicando un sovraccarico minimo sui server. Le route statiche presentano lo svantaggio di non reinstradare in modo dinamico i messaggi in caso di errore di rete.

Lync Server consente di impostare route statiche per i server proxy. Queste route sono costituite da due elementi principali: le impostazioni di configurazione proxy e le route proxy SIP. A loro volta, le route proxy SIP dispongono di numerose proprietà. Ad esempio, ogni route deve avere Transport, una proprietà che definisce il protocollo di rete utilizzato per trasmettere messaggi nella route. È possibile specificare la proprietà Transport tramite il cmdlet **New-CsSipProxyTransport**.

Il cmdlet **New-CsSipProxyTransport** richiede due parametri obbligatori: TransportChoice e Port. Il parametro TransportChoice viene configurato utilizzando un altro cmdlet, ovvero **New-CsSipProxyTCP** per assegnare TCP come protocollo di trasporto della route oppure **New-CsSipProxyTLS** per assegnare TLS come protocollo di trasporto della route. Ogni oggetto trasporto creato tramite il cmdlet **New-CsSipProxyTransport** deve essere salvato in una variabile. Tale variabile deve quindi essere utilizzata per configurare la proprietà Transport di una route proxy SIP.

Non è necessario utilizzare il cmdlet **New-CsSipProxyTransport** se si utilizza il cmdlet **New-CsStaticRoute** per creare una route statica.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsSipProxyTransport** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyTransport"}

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
<td><p><em>Port</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta utilizzato per il routing SIP. Ad esempio: -Port 7742.</p></td>
</tr>
<tr class="even">
<td><p><em>TransportChoice</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ITransportChoice</p></td>
<td><p>Indica il protocollo di trasmissione, TCP o TLS, da utilizzare per la route statica. Per utilizzare il protocollo TCP, creare un oggetto trasporto utilizzando il cmdlet <strong>New-CsSipProxyTCP</strong>. Per utilizzare il protocollo TLS, creare un oggetto trasporto utilizzando il cmdlet <strong>New-CsSipProxyTLS</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyTransport** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipProxyTransport** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Transport.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyTCP](new-cssipproxytcp.md)  
[New-CsSipProxyTLS](new-cssipproxytls.md)

