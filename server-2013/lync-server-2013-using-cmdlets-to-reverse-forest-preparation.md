---
title: 'Lync Server 2013: Utilizzo dei cmdlet per annullare la preparazione della foresta'
TOCTitle: Utilizzo dei cmdlet per annullare la preparazione della foresta
ms:assetid: f48c7eb3-ccb0-48e6-ac79-ab7c7062b9d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413024(v=OCS.15)
ms:contentKeyID: 49302464
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo dei cmdlet per annullare la preparazione della foresta per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-06-19_

Utilizzare il cmdlet **Disable-CsAdForest** per annullare il passaggio di preparazione della foresta.

> [!CAUTION]
> Se si esegue il cmdlet <strong>Disable-CsAdForest</strong> in un ambiente in cui è anche distribuita una versione precedente di Lync Server, verranno eliminate anche le impostazioni globali per la versione precedente.

## Per utilizzare cmdlet per annullare la preparazione della foresta

1.  Accedere a un computer che fa parte di un dominio come membro del gruppo Domain Admins nel dominio radice della foresta.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Disable-CsAdForest [-Force] [-GroupDomain <FQDN of the domain in which universal groups were created>]
    
    Ad esempio:
    
        Disable-CsAdForest -Force -GroupDomain contoso.net
    
    Il parametro Force specifica se forzare l'esecuzione dell'attività. Se questo parametro non è presente, il comando non verrà eseguito anche se un dominio nella foresta è ancora preparato per Lync Server 2013. Se viene specificato il parametro Force, l'azione continuerà indipendentemente dallo stato degli altri domini nella foresta.
    
    Se non si specifica il parametro GroupDomain, il valore predefinito è il dominio locale.

## Vedere anche

#### Attività

[Esecuzione della preparazione della foresta per Lync Server 2013](lync-server-2013-running-forest-preparation.md)  

#### Ulteriori risorse

[Preparazione della foresta per Lync Server 2013](lync-server-2013-preparing-the-forest.md)

