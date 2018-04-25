---
title: 'Lync Server 2013: Controllo di ammissione di chiamata con un PBX o un gateway PSTN di terze parti'
TOCTitle: Controllo di ammissione di chiamata con un PBX o un gateway PSTN di terze parti
ms:assetid: 95dc4ceb-bcad-48ee-86ec-af911727f853
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398762(v=OCS.15)
ms:contentKeyID: 49301373
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Controllo di ammissione di chiamata in Lync Server 2013 con un PBX o un gateway PSTN di terze parti

 

_**Ultima modifica dell'argomento:** 2012-10-20_

In questo argomento vengono forniti esempi sulla modalità di distribuzione del servizio Controllo di ammissione di chiamata nel collegamento tra l'interfaccia del gateway del Mediation Server e un gateway PSTN o PBX di terze parti.

## Caso 1: Controllo di ammissione di chiamata tra il Mediation Server e un gateway PSTN

Controllo di ammissione di chiamata può essere distribuito sul collegamento WAN tra l'interfaccia del gateway del Mediation Server e un gateway PSTN o PBX di terze parti.

**Caso 1: Controllo di ammissione di chiamata tra il Mediation Server e un gateway PSTN**

![Caso 1: controllo di ammissione di chiamata tra il Mediation Server e un gateway PSTN](images/Gg398762.4bebf9ee-2732-4ea6-bbe5-0269b2903d8c(OCS.15).jpg "Caso 1: controllo di ammissione di chiamata tra il Mediation Server e un gateway PSTN")

In questo esempio il servizio Controllo di ammissione di chiamata è applicato tra il Mediation Server e un gateway PSTN. Se un client Lync nel Sito di rete 1 effettua una chiamata PSTN attraverso il gateway PSTN nel Sito di rete 2, gli elementi multimediali passano attraverso il collegamento WAN. Per ogni sessione PSTN vengono pertanto eseguiti due controlli di ammissione di chiamata:

  - Tra l'applicazione client Lync e il Mediation Server

  - Tra il Mediation Server e il gateway PSTN

Ciò è valido sia per le chiamate PSTN in arrivo a un client nel Sito di rete 1 che per le chiamate PSTN in uscita che hanno origine da un'applicazione client nel Sito di rete 1.


> [!NOTE]
> Verificare che la subnet IP alla quale il gateway PSTN appartiene sia configurata e associata a Sito di rete 2.<BR>Verificare che la subnet IP alla quale appartengono entrambe le interfacce del Mediation Server sia configurata e associata con Sito di rete 1.<BR>Per informazioni dettagliate, vedere <A href="lync-server-2013-associate-a-subnet-with-a-network-site.md">Associare una subnet a un sito di rete in Lync Server 2013</A>.



## Caso 2: Controllo di ammissione di chiamata tra il Mediation Server e un PBX di terze parti con punto di terminazione multimediale

Questa configurazione è simile a quella del Caso 1. In entrambi i casi il Mediation Server conosce il dispositivo che termina il flusso multimediale al capo opposto del collegamento WAN e l'indirizzo IP del gateway PSTN o PBX con punto di terminazione multimediale (MTP) è configurato nel Mediation Server come hop successivo.

**Caso 2: Controllo di ammissione di chiamata tra il Mediation Server e un PBX di terze parti con MTP**

![Caso 2: controllo di ammissione di chiamata tra il Mediation Server e un PBX con MTP](images/Gg398762.1c0b5263-c053-4cca-842f-85dd670760c8(OCS.15).jpg "Caso 2: controllo di ammissione di chiamata tra il Mediation Server e un PBX con MTP")

In questo esempio il servizio Controllo di ammissione di chiamata è applicato tra il Mediation Server e il PBX/MTP. Se un client Lync nel Sito di rete 1 effettua una chiamata PSTN attraverso il PBX/MTP che si trova nel Sito di rete 2, gli elementi multimediali passano attraverso il collegamento WAN. Per ogni sessione PSTN vengono pertanto eseguiti due controlli di ammissione di chiamata:

  - Tra l'applicazione client Lync e il Mediation Server

  - Tra il Mediation Server e il PBX/MTP

Ciò è valido sia per le chiamate PSTN in arrivo a un client nel Sito di rete 1 che per le chiamate PSTN in uscita che hanno origine da un client nel Sito di rete 1.


> [!NOTE]
> Verificare che la subnet IP alla quale il MTP appartiene sia configurata e associata a Sito di rete 2.<BR>Verificare che la subnet IP alla quale appartengono entrambe le interfacce del Mediation Server sia configurata e associata con Sito di rete 1.<BR>Per informazioni dettagliate, vedere <A href="lync-server-2013-associate-a-subnet-with-a-network-site.md">Associare una subnet a un sito di rete in Lync Server 2013</A>.



## Case 3: Controllo di ammissione di chiamata tra il Mediation Server e un PBX di terze parti senza punto di terminazione multimediale

Il Caso 3 è leggermente diverso dai primi due. Se il PBX di terze parti non è provvisto di MTP, nel caso di una richiesta di sessione in uscita al PBX di terze parti, il Mediation Server non sa in che punto termineranno gli elementi multimediali nei confini del PBX. In questo caso, gli elementi multimediali circolano direttamente tra il Mediation Server e il dispositivo endpoint di terze parti.

**Caso 3: Controllo di ammissione di chiamata tra il Mediation Server e un PBX di terze parti senza MTP**

![Caso 3: controllo di ammissione di chiamata tra il Mediation Server e un PBX senza MTP](images/Gg398762.f4bcf800-3a68-4037-bb3f-adb2fdf50d32(OCS.15).jpg "Caso 3: controllo di ammissione di chiamata tra il Mediation Server e un PBX senza MTP")

In questo esempio, se un utente di un client Lync presso il Sito di rete 1 effettua una chiamata a un utente attraverso il PBX, il Mediation Server sarà in grado di eseguire il controllo di ammissione di chiamata solo sulla coda del proxy (tra l'applicazione client Lync e il Mediation Server). Poiché il Mediation Server non dispone di informazioni sul dispositivo endpoint durante la richiesta della sessione, non è possibile eseguire i controlli di Controllo di ammissione di chiamata sul collegamento WAN (tra il Mediation Server e l'endpoint di terze parti) prima di stabilire la chiamata. Una volta stabilita la sessione, tuttavia, il Mediation Server facilita il calcolo della larghezza di banda utilizzata sul trunk.

Per le chiamate che hanno origine dall'endpoint di terze parti, le informazioni sull'endpoint sono disponibili al momento della richiesta della sessione ed è possibile eseguire il controllo di Controllo di ammissione di chiamata su entrambi i lati del Mediation Server.


> [!NOTE]
> Verificare che la subnet IP alla quale appartengono i dispositivi endpoint sia configurata e associata con Sito di rete 2.<BR>Verificare che la subnet IP alla quale appartengono entrambe le interfacce del Mediation Server sia configurata e associata con Sito di rete 1.<BR>Per informazioni dettagliate, vedere <A href="lync-server-2013-associate-a-subnet-with-a-network-site.md">Associare una subnet a un sito di rete in Lync Server 2013</A>.


