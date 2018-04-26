---
title: 'Lync Server 2013: Verificare la progettazione della topologia'
TOCTitle: Verificare la progettazione della topologia
ms:assetid: c1b61814-239e-4101-aab0-de3db1d8793c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412951(v=OCS.15)
ms:contentKeyID: 49301888
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare la progettazione della topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-02_

Generatore di topologie verifica automaticamente la topologia. Gli eventuali errori di topologia vengono identificati come errori di convalida e indicati dall'apposita icona accanto al ruolo del server. È inoltre importante verificare che la topologia rappresenti correttamente la topologia della propria distribuzione.

## Per verificare la topologia prima della pubblicazione

1.  Controllare che tutti gli URL semplici siano configurati in modo corretto.

2.  Verificare che il server basato su SQL Server sia online e disponibile per il computer in cui è installato Generatore di topologie, incluse eventuali regole del firewall necessarie.

3.  Verificare che la condivisione file sia disponibile e siano state definite le autorizzazioni appropriate.

4.  Verificare che nella topologia siano definiti i ruoli del server corretti conformi ai requisiti della distribuzione.

5.  Verificare che i server esistano in Servizi di dominio Active Directory. Ciò avviene automaticamente se i server sono stati aggiunti al dominio.

Dopo aver verificato la topologia e stabilito che non sono presenti errori di convalida, è possibile procedere con la pubblicazione della topologia. Gli eventuali errori di convalida rilevati dovranno essere risolti prima di poter pubblicare la topologia. Per informazioni dettagliate sulla pubblicazione della topologia, vedere [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md).

