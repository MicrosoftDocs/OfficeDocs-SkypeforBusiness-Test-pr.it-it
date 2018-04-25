---
title: Topologie per i telefoni IP
TOCTitle: Topologie per i telefoni IP
ms:assetid: 26ebffcf-43ff-4e70-847d-0fbc90e94e57
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425740(v=OCS.15)
ms:contentKeyID: 49299975
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologie per i telefoni IP

 

_**Ultima modifica dell'argomento:** 2012-06-21_

In questa sezione viene fornita una panoramica del processo di connettività e vengono illustrate le differenze tra la modalità di connessione di un telefono IP in una rete interna e in una rete esterna.


> [!NOTE]
> Lync Server offre il supporto per i telefoni IP seguenti: il telefono di area comune Aastra 6721ip, il telefono da tavolo Aastra 6725ip, il telefono IP di area comune HP 4110, i telefoni IP da tavolo HP 4120, Polycom CX600 e Polycom CX700, il telefono IP di area comune Polycom CX500 e il telefono IP per conferenze Polycom CX3000. Tutti questi telefoni, ad eccezione del Polycom CX700, possono eseguire Lync Phone Edition.



Nel diagramma seguente vengono descritti tutti i componenti coinvolti nella connettività di un dispositivo nell'ambiente aziendale.

**Topologia interna**

![Dispositivi all'interno della rete](images/Gg425740.3d88893e-df57-46e3-855a-a1d24589030a(OCS.15).jpg "Dispositivi all'interno della rete")


> [!NOTE]
> La figura precedente è una rappresentazione logica e non una panoramica fisica. Servizi di dominio Active Directory ad esempio è presente raramente nello stesso computer in cui si trovano i componenti di Lync Server. L'archivio utente può essere contenuto nel server back-end, nel server di archiviazione o nel Monitoring Server. Lync Server Management Shell, il server Web e i servizi di aggiornamento fanno tutti parte del ruolo Front End Server.



Nel diagramma seguente viene fornita una panoramica dei componenti coinvolti quando il dispositivo si trova all'esterno della rete aziendale.

**Topologia esterna**

![Dispositivi all'esterno della rete](images/Gg425740.8ce6bb8e-b89c-4c4e-ac6d-41ac6c68f6f3(OCS.15).jpg "Dispositivi all'esterno della rete")


> [!NOTE]
> Il Servizio Web aggiornamento dispositivi offre un sito Web esterno e uno interno, ma in questo diagramma viene illustrato solo quello esterno.<BR>La posizione della funzione di registrazione e l'URL del Servizio Web aggiornamento dispositivi dell'organizzazione devono essere pubblicati in DNS se deve essere abilitato l'accesso esterno. Il server perimetrale inoltre deve essere distribuito e configurato correttamente per consentire le comunicazioni esterne dal dispositivo all'ambiente aziendale e viceversa. Questo viene omesso nel diagramma precedente perché la distribuzione di server perimetrali non è specifica della connettività di un dispositivo.


