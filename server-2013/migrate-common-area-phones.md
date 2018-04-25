---
title: Eseguire la migrazione dei telefoni delle aree comuni
TOCTitle: Eseguire la migrazione dei telefoni delle aree comuni
ms:assetid: 31bd26fc-861b-45c6-8221-18df16e575de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688015(v=OCS.15)
ms:contentKeyID: 49887507
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione dei telefoni delle aree comuni

 

_**Ultima modifica dell'argomento:** 2012-09-29_

I telefoni delle aree comuni sono telefoni IP che molto spesso risiedono in un'area di lavoro condivisa o area comune, ad esempio una sala di attesa, una cucina o un reparto produzione. Non è necessario che tali telefoni siano connessi a un computer per fornire le funzionalità UC di Lync Server. Dopo aver eseguito la migrazione di una distribuzione di Lync Server 2010 a Lync Server 2013, è anche necessario eseguire la migrazione degli oggetti contatto associati al telefono dell'area comune legacy. Usando Lync Server Management Shell si procederà innanzitutto al recupero di tutti gli oggetti contatto associati ai telefoni delle aree comuni di Lync Server 2010 e quindi allo spostamento di tali oggetti nel pool di Lync Server 2013.

**Migrare i telefoni delle aree comuni**

1.  Dal Front End Server di Lync Server 2013 aprire Lync Server Management Shell.

2.  Dalla riga di comando digitare quanto segue:
    
        Get-CsCommonAreaPhone -Filter {RegistrarPool -eq "pool01.contoso.net"} | Move-CsCommonAreaPhone -Target pool02.contoso.net

3.  Per verificare che tutti gli oggetti contatto siano stati spostati nel pool di Lync Server 2013, da Lync Server Management Shell digitare quanto segue:
    
        Get-CsCommonAreaPhone -Filter {RegistrarPool -eq "pool02.contoso.net"}
    
    Verificare che tutti gli oggetti contatto siano ora associati al pool di Lync Server 2013.

