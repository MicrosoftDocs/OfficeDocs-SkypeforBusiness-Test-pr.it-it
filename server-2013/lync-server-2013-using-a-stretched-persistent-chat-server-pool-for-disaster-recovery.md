---
title: "Lync Server 2013: Utilizza pool server Chat persist. esteso per ripr. emerg."
TOCTitle: Utilizzo di un pool di server Chat persistente esteso per il ripristino di emergenza
ms:assetid: 74c5287e-d70d-490a-9adc-ab419917ddd9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205007(v=OCS.15)
ms:contentKeyID: 49300990
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di un pool di server Chat persistente esteso per il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

La soluzione di ripristino di emergenza per server Chat persistente si basa su un pool di server Chat persistente esteso, analogamente alla resilienza di siti metropolitani in Lync Server 2010, con la differenza che non è necessaria una VLAN estesa. Estendendo il pool di server Chat persistente, si configura un pool nella topologia a livello logico, ma i server sono collocati fisicamente in due data center separati. Configurare allo stesso modo il mirroring SQL Server per il database, e distribuire database e mirror nello stesso data center. È inoltre necessario configurare un database di backup nel data center secondario (con un mirror facoltativo per l'elevata disponibilità durante il ripristino di emergenza); questo sarà lo stesso database utilizzato per il failover durante il ripristino di emergenza.

Per informazioni dettagliate su come configurare il mirroring SQL Server per l'elevata disponibilità, vedere [Mirroring di SQL Server in Lync Server 2013](lync-server-2013-sql-server-mirroring.md). Per informazioni dettagliate sul failover per il ripristino di emergenza, vedere [Configurazione del log shipping di SQL Server in Lync Server 2013 per il database primario del server chat persistente](lync-server-2013-setting-up-sql-server-log-shipping-for-the-persistent-chat-server-primary-database.md) e [Configurazione del log shipping di SQL Server tra il mirror primario e il database secondario di log shipping in Lync Server 2013](lync-server-2013-setting-up-sql-server-log-shipping-between-the-primary-mirror-and-the-log-shipping-secondary-database.md).

