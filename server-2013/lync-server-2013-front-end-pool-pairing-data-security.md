---
title: "Lync Server 2013: sicurezza dei dati per l'abbinamento dei pool Front End"
TOCTitle: Sicurezza dei dati per l'abbinamento dei pool Front End
ms:assetid: edb852b8-ea86-4948-b756-60fe6ee876d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721930(v=OCS.15)
ms:contentKeyID: 49887813
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sicurezza dei dati per l'abbinamento dei pool Front End in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-10-07_

Il Servizio di backup è un meccanismo di replica dei dati introdotto in Lync Server 2013 che trasferisce dati utente e contenuti delle conferenze tra due pool Front End abbinati in modo continuo tra due data center per consentire eventuali ripristini di emergenza. I dati utente contengono gli URI SIP nonché gli elenchi contatti e le impostazioni. Il contenuto delle conferenze include i caricamenti di Microsoft PowerPoint 2010 e le lavagne utilizzate. Dal pool di origine, i dati utente e i contenuti delle conferenze vengono esportati dall'archiviazione locale, compressi e trasferiti nel pool di destinazione, dove vengono decompressi e importati nell'archiviazione locale. Il Servizio di backup presume che i collegamenti di comunicazione tra i due data center si trovino all'interno di una rete aziendale protetta da Internet. I dati trasferiti tra i due data center non vengono crittografati, né è previsto l'incapsulamento nativo all'interno di un protocollo di sicurezza, quale HTTPS. Pertanto resta possibile un attacco man-in-the-middle compiuto da personale interno alla rete aziendale.

## Valutazione dei rischi per la sicurezza

Le aziende che distribuiscono Lync Server 2013 su più data center e utilizzano la caratteristica di ripristino di emergenza devono assicurarsi che il traffico tra i data center sia protetto dalla Intranet aziendale. Le aziende che intendono cautelarsi dal rischio di un attacco interno, devono proteggere i collegamenti di comunicazione tra i data center.

In genere, si suppone che i data center di un'azienda siano protetti nella Intranet aziendale. Molti altri tipi di dati aziendali riservati vengono trasferiti tra questi data center. L'infrastruttura IT dell'azienda è esposta a seri pericoli se i collegamenti tra data center non sono protetti.

Sebbene in un'azienda esista il pericolo di attacchi man-in-the-middle, è relativamente contenuto se paragonato al rischio di esporre il traffico in Internet. In particolare, i dati utente esposti dal Servizio di backup (ad esempio gli URI SIP) sono generalmente disponibili a tutti gli utenti dell'azienda con altri mezzi, quali la Rubrica globale di Exchange o altri software di directory. Quando viene utilizzato il Servizio backup per copiare dati tra due pool abbinati, è pertanto necessario concentrarsi sulla protezione della WAN tra i due data center.

## Contenere i rischi per la sicurezza

Esistono molti modi per migliorare la protezione del traffico del Servizio di backup, a partire dalla limitazione dell'accesso ai data center alla protezione del trasporto WAN tra i due data center. Nella maggior parte dei casi, le aziende che distribuiscono Lync Server 2013 dispongono già dell'infrastruttura di sicurezza necessaria. Alle aziende che invece cercano indicazioni, Microsoft propone un esempio di come creare un'infrastruttura IT sicura. Tuttavia, ciò non significa che esista una sola soluzione, né che questa sia preferibile per Lync Server. È necessario che i clienti aziendali scelgano la soluzione più adatta alle proprie esigenze specifiche, anche in base ai propri requisiti e alla propria infrastruttura di sicurezza IT. La soluzione di esempio Microsoft utilizza IPSec e Criteri di gruppo per l'isolamento del server e del dominio. Per informazioni dettagliate, vedere [http://go.microsoft.com/fwlink/p/?LinkId=268544](http://go.microsoft.com/fwlink/p/?linkid=268544). Per domande e commenti, contattare secwish@microsoft.com.

Un'altra soluzione possibile prevede l'utilizzo di IPSec per proteggere i dati inviati dal Servizio di backup stesso. Se si sceglie questo metodo, è necessario configurare le regole IPSec per il protocollo SMB per i seguenti server, in cui il pool A e il pool B sono due pool Front End abbinati.

  - Il servizio SMB (TCP/445) da ogni Front End Server del pool A all'archivio file utilizzato dal pool B.

  - Il servizio SMB (TCP/445) da ogni Front End Server del pool B all'archivio file utilizzato dal pool A.


> [!WARNING]
> IPsec non sostituisce la protezione a livello dell'applicazione, come SSL/TLS. Uno dei vantaggi offerti da IPsec è che consente di proteggere il traffico di rete delle applicazioni esistenti senza modificarle. Le aziende che desiderano solamente proteggere il trasporto tra i due data center possono chiedere ai propri fornitori di hardware di rete quali sono i dispositivi disponibili per proteggere le connessioni WAN.


