---
title: New-CsSipProxyUseDefaultCert
TOCTitle: New-CsSipProxyUseDefaultCert
ms:assetid: 387cf221-2607-4c46-abc3-f8db263a934f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425858(v=OCS.15)
ms:contentKeyID: 49300220
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyUseDefaultCert

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un riferimento oggetto al certificato predefinito utilizzato da Lync Server. Questo riferimento oggetto può essere utilizzato per configurare una route statica per l'utilizzo di TLS (Transport Layer Security) come protocollo di trasporto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyUseDefaultCert

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 creano un nuovo oggetto trasporto proxy SIP che utilizza TLS come trasporto. Poiché TLS richiede un certificato (da utilizzare per l'autenticazione), il primo comando dell'esempio utilizza il cmdlet **New-CsSipProxyUseDefaultCert** per configurare un nuovo oggetto SipProxy.UseDefaultCert. Questo oggetto, archiviato in una variabile denominata $cert, indica a Lync Server di utilizzare il certificato predefinito per il trasporto TLS. Dopo la creazione dell'oggetto UseDefaultCert, è possibile chiamare il cmdlet **New-CsSipProxyTLS** per creare un nuovo oggetto SipProxy.TLS, che utilizza il certificato predefinito e punta ad atl-proxy-001.litwareinc.com come nome di dominio completo (FQDN) del server dell'hop successivo.

Subito dopo essere stato creato, l'oggetto TLS (e il protocollo TLS) può essere aggiunto a un oggetto Transport, creato chiamando il cmdlet **New-CsSipProxyTransport**.

    $cert = New-CsSipProxyUseDefaultCert
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com
    
    $transport = New-CsSipProxyTransport -TransportChoice $tls -Port 7500

## Descrizione dettagliata

Quando si invia un messaggio SIP, il messaggio potrebbe dover attraversare molteplici subnet e reti prima di essere recapitato; il percorso seguito dal messaggio è spesso definito route. Nelle reti esistono due tipi di route: dinamiche e statiche. Con il routing dinamico, i server utilizzano algoritmi per determinare la posizione successiva (vale a dire l'hop successivo) a cui dovrebbe essere inoltrato un messaggio. Con il routing statico, i percorsi seguiti dai messaggi sono determinati anticipatamente dagli amministratori di sistema. Quando riceve un messaggio, il server controlla l'indirizzo del messaggio e inoltra il messaggio stesso al server dell'hop successivo configurato anticipatamente da un amministratore. Se la configurazione è corretta, le route statiche aiutano a garantire un recapito tempestivo e accurato dei messaggi, applicando un sovraccarico minimo sui server. Lo svantaggio delle route statiche è dovuto al fatto che i messaggi non vengono reinstradati in modo dinamico se si verifica un errore di rete.

Lync Server consente di impostare le route statiche per i server proxy. Se si decide di utilizzare TLS (il protocollo di trasporto consigliato), è necessario specificare anche il certificato da utilizzare per l'autenticazione. È possibile ottenere un certificato specifico per l'utilizzo nella route statica oppure configurare TLS in modo da utilizzare il certificato Lync Server predefinito. Se si decide di utilizzare il certificato predefinito, è possibile creare un riferimento oggetto a tale certificato eseguendo **New-CsSipProxyUseDefaultCert**. Il riferimento oggetto al certificato può quindi essere utilizzato dal cmdlet **New-CsSipProxyTLS** per configurare TLS come protocollo di trasporto.

Non è necessario utilizzare il cmdlet **New-CsSipProxcyUseDefaultCert** se si utilizza il cmdlet **New-CsStaticRoute** per creare la route statica.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsSipProxyUseDefaultCert** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyUseDefaultCert"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce unicamente parametri comuni di Windows PowerShell.</p>
<p></p></td>
<td><p></p></td>
<td> </td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyUseDefaultCert** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipProxyUseDefaultCert** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.UseDefaultCert.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyTLS](new-cssipproxytls.md)

