---
title: New-CsIssuedCertId
TOCTitle: New-CsIssuedCertId
ms:assetid: 3158e26e-3fda-488b-a08d-5481e1abfc1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425814(v=OCS.15)
ms:contentKeyID: 49300097
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsIssuedCertId

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un certificato esistente a un oggetto SipProxy.TLS. A sua volta, tale oggetto può essere utilizzato per configurare una route statica in modo che utilizzi TLS (Transport Layer Security) come protocollo di trasporto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsIssuedCertId -Issuer <String> -SerialNumber <Byte[]>

## Esempi

## ESEMPIO 1

Con i comandi mostrati nell'esempio 1 viene creato un nuovo oggetto ID certificato, successivamente assegnato a un oggetto SipProxy.TLS. A sua volta, tale oggetto può essere utilizzato per configurare una route statica per l'uso del protocollo di trasporto TLS. Per eseguire queste operazioni, il primo comando nell'esempio utilizza **New-CsIssuedCertId** per creare un oggetto ID certificato per un certificato emesso da Fabrikam con numero di serie 10143418 (il numero di serie viene specificato come array di stringhe di due caratteri). L'oggetto risultante viene memorizzato in una variabile denominata $cert.

Nel secondo comando, viene utilizzato New-CsSipProxyTLS per creare un oggetto SIPProxy.TLS. Per garantire che questo oggetto utilizzi il certificato emesso da Fabrikam per l'autenticazione, come valore per il parametro Certificate viene utilizzata la variabile $cert.

    $cert = New-CsIssuedCertId -Issuer "Fabrikam" -SerialNumber 0x10,0x14,0x3A,0x1A
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com

## Descrizione dettagliata

Quando si invia un messaggio SIP (Session Initiation Protocol), il messaggio potrebbe dover attraversare molteplici subnet e reti prima di essere recapitato; il percorso seguito dal messaggio è spesso definito route. Nelle reti esistono due tipi di route: dinamiche e statiche. Con il routing dinamico, i server utilizzano algoritmi per determinare la posizione successiva (vale a dire l'hop successivo) a cui dovrebbe essere inoltrato un messaggio. Con il routing statico, i percorsi seguiti dai messaggi sono determinati anticipatamente dagli amministratori di sistema. Quando riceve un messaggio, il server controlla l'indirizzo del messaggio e inoltra il messaggio stesso al server dell'hop successivo configurato anticipatamente da un amministratore. Se la configurazione è corretta, le route statiche aiutano a garantire un recapito tempestivo e accurato dei messaggi, applicando un sovraccarico minimo sui server. Lo svantaggio del routing statico è dovuto al fatto che i messaggi non vengono reinstradati in modo dinamico se si verifica un errore di rete.

Lync Server consente di specificare TCP (Transmission Control Protocol) o TLS (Transport Layer Security) come protocollo di trasporto durante la configurazione di una route statica. Se si decide di utilizzare TLS come protocollo, è necessario innanzitutto assegnare un certificato da utilizzare per l'autenticazione. In tal caso, è possibile utilizzare il certificato predefinito configurato per Lync Server. In alternativa, è possibile assegnare certificati TLS chiamando **New-CsIssuedCertID** per creare un oggetto certificato e poi assegnando tale oggetto a un oggetto SipProxy.TLS creato tramite il cmdlet **New-CsSipProxyTLS**.

Quando si esegue **New-CsIssuedCertID** è necessario fornire al cmdlet il nome dell'emittente e il numero di serie di un certificato esistente. Tali informazioni possono essere ottenute eseguendo questo comando:

Get-CsCertificate | Select-Object Issuer, SerialNumber

I numeri di serie devono essere passati come array di byte, quindi è necessario passare il numero di serie come array di valori di due caratteri. Inoltre, ogni valore di due caratteri deve essere preceduto da 0x. Ad esempio, si supponga di avere un certificato con numero di serie 1E225D3ZF66. I dati devono essere passati utilizzando la sintassi:

\-SerialNumber 0x1E,0x22,0x5D,0x3F,0x66

Non è necessario utilizzare il cmdlet **New-CsIssuedCertId** se si crea una route statica utilizzando il cmdlet **New-CsStaticRoute**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsIssuedCertId** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsIssuedCertId"}

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
<td><p><em>Issuer</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'Autorità di certificazione che ha emesso il certificato da utilizzare nella route statica.</p></td>
</tr>
<tr class="even">
<td><p><em>SerialNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Numero di serie del certificato da utilizzare nella route statica. I numeri di serie devono essere passati come array di byte, quindi è necessario passare il numero di serie come array di valori di due caratteri, con ciascun valore di due caratteri preceduto da 0x. Ad esempio: -SerialNumber 0x01, 0x23, 0x45, 0x67, 0x89.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsIssuedCertId** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsIssuedCertId**consente di creare nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.BaseTypes.IssuedCertId.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyTLS](new-cssipproxytls.md)

