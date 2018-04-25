---
title: Crittografia per Lync Server 2013
TOCTitle: Crittografia per Lync Server 2013
ms:assetid: d18c74a6-385b-407b-98eb-0d525fa38fea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481135(v=OCS.15)
ms:contentKeyID: 59679244
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Crittografia per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Lync Server 2013 utilizza TLS e MTLS per crittografare i messaggi istantanei. MTLS è necessario per tutto il traffico tra server, indipendentemente dal fatto che il traffico sia circoscritto a una rete interna oppure attraversi il perimetro della rete interna. TLS è facoltativo ma fortemente consigliato tra Mediation Server e il gateway multimediale. Se TLS viene configurato per questo collegamento, è necessario anche MTLS. Il gateway deve pertanto essere configurato con un certificato di una CA ritenuta attendibile da Mediation Server.

I requisiti per questo traffico tra client dipendono dal fatto che il traffico attraversi o meno il firewall aziendale interno. Per il traffico esclusivamente interno è possibile utilizzare TLS, che esegue la crittografia del messaggio istantaneo, oppure TCP, che non la esegue.

Nella seguente tabella vengono riassunti i requisiti di protocollo per ogni tipo di traffico.

### Protezione del traffico

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di traffico</th>
<th>Protetto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tra server</p></td>
<td><p>MTLS</p></td>
</tr>
<tr class="even">
<td><p>Da client a server</p></td>
<td><p>TLS</p></td>
</tr>
<tr class="odd">
<td><p>Presenza e messaggistica istantanea</p></td>
<td><p>TLS (se configurato per TLS)</p></td>
</tr>
<tr class="even">
<td><p>Condivisione di contenuti multimediali desktop, audio e video</p></td>
<td><p>SRTP</p></td>
</tr>
<tr class="odd">
<td><p>Condivisione desktop (segnalazione)</p></td>
<td><p>TLS</p></td>
</tr>
<tr class="even">
<td><p>Conferenze Web</p></td>
<td><p>TLS</p></td>
</tr>
<tr class="odd">
<td><p>Download di contenuti delle riunioni, download della rubrica, espansione del gruppo di distribuzione</p></td>
<td><p>HTTPS</p></td>
</tr>
</tbody>
</table>


## Crittografia multimediale

Il traffico multimediale viene crittografato tramite RTP sicuro (SRTP), un profilo RTP (Real-Time Transport Protocol) che garantisce al traffico RTP riservatezza, autenticazione e protezione da attacchi di tipo replay. SRTP utilizza una chiave di sessione generata dal servizio MRAS (Media Relay Authentication Service) quando l'autenticazione di una richiesta del server (per conto dei partecipanti multimediali) viene confermata. La chiave di sessione viene protetta dal nome utente e dalla password negoziati forniti a MRAS dai Front End Server e inviati ai partecipanti tramite il canale SIP protetto da TLS. La decrittografia della chiave di sessione protetta con il nome utente e la password utilizzati da MRAS, e forniti in modo sicuro tramite il certificato TLS dei partecipanti e il canale SIP protetto, consente ai partecipanti di decrittografare il flusso SRTP. Inoltre, anche il flusso multimediale in entrambe le direzioni tra Mediation Server e il relativo hop successivo interno viene decrittografato tramite SRTP. Il flusso multimediale in entrambe le direzioni tra Mediation Server e i gateway multimediali non viene crittografato. Mediation Server può supportare la crittografia verso il gateway multimediale, ma il gateway deve supportare MTLS e l'archiviazione di un certificato.


> [!NOTE]
> Audio/Video (A/V) è supportato con la nuova versione di Windows Live Messenger. Se si implementa la federazione A/V con Windows Live Messenger, è necessario modificare anche il livello di crittografia di Lync Server. Per impostazione predefinita, il livello di crittografia è impostato su Richiesto. È necessario modificare questa impostazione in Supportato utilizzando Lync Server Management Shell. Per ulteriori informazioni, vedere <A href="lync-server-2013-deploying-external-user-access.md">Distribuzione dell'accesso degli utenti esterni in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



Il traffico multimediale audio e video non è crittografato tra Microsoft Lync 2013 e i client di Windows Live.

## FIPS

Lync Server 2013 e Microsoft Exchange Server 2013 funzionano con il supporto per gli algoritmi FIPS (Federal Information Processing Standard) 140-2 se i sistemi operativi Windows Server sono configurati per l'utilizzo degli algoritmi FIPS 140-2 per la crittografia del sistema. Per implementare il supporto per FIPS, è necessario configurare ogni server che esegue Lync Server 2013 per il supporto. Per informazioni dettagliate sull'utilizzo di algoritmi conformi a FIPS e su come implementare il supporto per FIPS, vedere l'articolo 811833 della Microsoft Knowledge Base, Effetti dell'impostazione di sicurezza "Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma" in Windows XP e nelle versioni successive di Windows, all'indirizzo [http://go.microsoft.com/fwlink/p/?linkid=3052\&kbid=811833](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=811833). Per informazioni dettagliate sul supporto per FIPS 140-2 e le limitazioni in Exchange 2010, vedere Exchange 2010 SP1 e supporto per algoritmi conformi a FIPS all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=205335](http://go.microsoft.com/fwlink/p/?linkid=205335).

