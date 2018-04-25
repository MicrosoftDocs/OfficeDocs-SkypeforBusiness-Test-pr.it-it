---
title: Infrastruttura a chiave pubblica per Lync Server 2013
TOCTitle: Infrastruttura a chiave pubblica per Lync Server 2013
ms:assetid: 737c8a25-23e9-4494-ab76-5a7b729b44ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481131(v=OCS.15)
ms:contentKeyID: 59679241
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Infrastruttura a chiave pubblica per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-13_

Microsoft Lync Server 2013 si basa sui certificati per l'autenticazione server e per stabilire una catena di attendibilità tra i client e i server e tra diversi ruoli server. L'infrastruttura a chiave pubblica (PKI) di Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 e Windows Server 2003 fornisce l'infrastruttura per stabilire e convalidare questa catena di attendibilità.

I certificati sono ID digitali: identificano un server in base al nome e ne specificano le proprietà. Per assicurare che le informazioni in un certificato siano valide, il certificato deve essere emesso da una CA ritenuta attendibile dai client o da altri server che si connettono al server. Se il server si connette solo ad altri client e server in una rete privata, la CA può essere una CA globale (enterprise). Se il server interagisce con entità esterne alla rete privata, potrebbe essere necessaria una CA pubblica.

Anche se le informazioni nel certificato sono valide, è necessario verificare che il server che presenta tale certificato sia realmente quello rappresentato dal certificato. Questa operazione può essere eseguita con l'infrastruttura a chiave pubblica di Windows.

Ogni certificato è collegato a una chiave pubblica. Il server specificato nel certificato include una chiave privata corrispondente nota solo al server stesso. Un client o un server che stabilisce una connessione utilizza la chiave pubblica per crittografare delle informazioni casuali e le invia al server. Se il server decrittografa le informazioni e le restituisce come testo normale, l'entità che stabilisce la connessione può essere certa che il server includa la chiave privata del certificato e che quindi sia il server specificato nel certificato.


> [!NOTE]
> Non tutte le CA pubbliche soddisfano i requisiti dei certificati di Lync Server 2013. È consigliabile fare riferimento all'elenco dei fornitori di CA pubbliche certificate per i propri certificati pubblici. Per informazioni dettagliate, vedere Partner di certificato per le comunicazioni unificate <A href="http://go.microsoft.com/fwlink/p/?linkid=140898">http://go.microsoft.com/fwlink/p/?LinkId=140898</A>.



## Punti di distribuzione CRL

Lync Server 2013 richiede che tutti i certificati del server contengano uno o più punti di distribuzione Elenco di revoche di certificati (CRL). I punti di distribuzione CRL (CDP) sono posizioni da cui è possibile scaricare i CRL per verificare che il certificato non sia stato revocato dal momento dell'emissione e che si trovi ancora all'interno del periodo di validità. Un punto di distribuzione CRL è indicato nelle proprietà del certificato sotto forma di URL e in genere si tratta di un HTTP sicuro.

## Utilizzo chiavi avanzato

Lync Server 2013 richiede che tutti i certificati del server supportino Utilizzo chiavi avanzato (EKU) per l'autenticazione del server. La configurazione del campo EKU per l'autenticazione del server implica che il certificato sia valido e che possa essere utilizzato per l'autenticazione dei server. Questo EKU è essenziale per MTLS. È possibile immettere più di una voce nel campo EKU, per consentire l'utilizzo del certificato per più scopi.


> [!NOTE]
> L'utilizzo chiavi avanzato di autenticazione client, in genere necessario per le connessioni MTLS da Live Communications Server 2003 e Live Communications Server 2005, non è più richiesto. Tuttavia, è necessario che l'EKU si trovi nei server perimetrali che si connettono ad AOL attraverso la connettività per la messaggistica istantanea pubblica.


