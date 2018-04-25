---
title: Eseguire la migrazione dei dispositivi analogici
TOCTitle: Eseguire la migrazione dei dispositivi analogici
ms:assetid: ad072916-87ed-4d44-8289-aab87da86250
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721846(v=OCS.15)
ms:contentKeyID: 49887700
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione dei dispositivi analogici

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Lync Server offre il supporto per i dispositivi analogici. Nello specifico, i dispositivi analogici supportati sono telefoni audio analogici e apparecchi fax analogici. È possibile configurare i gateway qualificati per supportare l'utilizzo di dispositivi analogici nell'ambiente Lync Server. Dopo aver eseguito la migrazione da Lync Server 2010 a Lync Server 2013, è inoltre necessario eseguire la migrazione degli oggetti contatto associati ai dispositivi analogici. Utilizzare Lync Server Management Shell per recuperare tutti gli oggetti contatto associati ai dispositivi analogici di Lync Server 2010 e quindi spostare tali oggetti nel pool di Lync Server 2013.

## Per eseguire la migrazione dei dispositivi analogici

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Nella riga di comando digitare il comando seguente:
    
        Get-CsAnalogDevice -Filter {RegistrarPool -eq "pool01.contoso.net"} | Move-CsAnalogDevice -Target pool02.contoso.net

3.  Verificare che tutti gli oggetti contatto siano stati spostati nel pool di Lync Server 2013. A tale scopo, nella riga di comando digitare quanto segue:
    
        Get-CsAnalogDevice -Filter {RegistrarPool -eq "pool02.contoso.net"}

4.  Verificare che tutti gli oggetti contatto ora siano associati al pool di Lync Server 2013.

