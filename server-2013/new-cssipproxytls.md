---
title: New-CsSipProxyTLS
TOCTitle: New-CsSipProxyTLS
ms:assetid: 7e04f7bb-c33f-49b4-9306-082b14d2a854
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398629(v=OCS.15)
ms:contentKeyID: 49301114
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyTLS

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo oggetto SipProxy.TLS, che può essere quindi utilizzato per configurare una route statica che utilizza TLS (Transport Layer Security) come proprio protocollo di trasporto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyTLS -Certificate <ITLSTLSChoice> -Fqdn <String>

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 crea un nuovo oggetto trasporto proxy SIP che utilizza TLS come trasporto. Poiché TLS richiede un certificato da utilizzare per scopi di autenticazione, il primo comando nell'esempio utilizza il cmdlet **New-CsSipProxyUseDefaultCert** per configurare un nuovo oggetto SipProxy.UseDefaultCert. Questo oggetto, archiviato in una variabile denominata $cert, indica a Lync Server di utilizzare il certificato predefinito per il trasporto TLS. Dopo essere stato creato, l'oggetto UseDefaultCert può essere chiamato dal cmdlet **New-CsSipProxyTLS** per creare un nuovo oggetto SipProxy.TLS, che utilizza il certificato predefinito e punta ad atl-proxy-001.litwareinc.com come nome di dominio completo per il server dell'hop successivo.

Subito dopo la creazione dell'oggetto TLS, tale oggetto e il protocollo TLS possono essere aggiunti a un oggetto Transport, creato chiamando il cmdlet **New-CsSipProxyTransport**.

    $cert = New-CsSipProxyUseDefaultCert
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com
    
    $transport = New-CsSipProxyTransport -TransportChoice $tls -Port 7500

## Descrizione dettagliata

Quando si invia un messaggio SIP a qualcuno, quel messaggio potrebbe dover attraversare più subnet e reti prima di essere consegnato; il percorso effettuato dal messaggio viene spesso chiamato "route". Nelle reti, esistono due tipi di route: dinamiche e statiche. Con le route dinamiche, i server utilizzano algoritmi per stabilire la prossima destinazione (prossimo hop) dove inoltrare il messaggio. Con le route statiche, il percorso del messaggio viene stabilito a priori dagli amministratori di sistema. Quando un messaggio viene ricevuto da un server, questo controlla l'indirizzo del messaggio e lo inoltra al prossimo server che è stato preconfigurato da un amministratore. Se configurate correttamente le route statiche aiutano ad assicurare una tempestiva ed accurata consegna del messaggio senza sovraccarico sul server. Lo svantaggio delle route statiche è rappresentato dal fatto che i messaggi non vengono dinamicamente reinstradati nel caso di un errore di rete.

Lync Server consente di impostare route statiche per i server proxy. Queste route sono costituite da due elementi principali: le impostazioni di configurazione proxy e le route proxy SIP. A loro volta, le route proxy SIP dispongono di numerose proprietà. Ad esempio, ogni route deve avere Transport, una proprietà che definisce il protocollo di rete utilizzato per trasmettere messaggi nella route.

Lync Server consente di specificare TCP (Transmission Control Protocol) o TLS (Transport Layer Security) come protocollo di trasporto. Se si decide di utilizzare TLS come protocollo, è necessario innanzitutto creare un oggetto TLS utilizzando il cmdlet **New-CsSipProxyTLS**. È quindi possibile utilizzare tale oggetto per specificare il protocollo per l'oggetto Transport creato dal cmdlet **New-CsSipProxyTransport**.

Si noti che si deve anche specificare un certificato (da utilizzare per scopi di autenticazione) se si sceglie di utilizzare TLS come protocollo di trasporto.

Non è necessario il cmdlet **New-CsSipProxyTLS** se per creare la nuova route statica si utilizza il cmdlet **New-CsStaticRoute**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsSipProxyTLS** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyTLS"}

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
<td><p><em>Certificate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ITLSTLSChoice</p></td>
<td><p>Certificato da utilizzare per autenticazione TLS.</p></td>
</tr>
<tr class="even">
<td><p><em>Fqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome completo di dominio (FQDN) del server hop successivo. Ad esempio: -Fqdn atl-proxy-001.litwareinc.com.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyTLS** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipProxyTLS** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.TLS.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyTCP](new-cssipproxytcp.md)  
[New-CsSipProxyTransport](new-cssipproxytransport.md)  
[New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

