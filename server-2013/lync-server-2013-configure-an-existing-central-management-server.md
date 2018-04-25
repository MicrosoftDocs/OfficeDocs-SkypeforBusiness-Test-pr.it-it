---
title: 'Lync Server 2013: Configurare un server di gestione centrale esistente'
TOCTitle: Configurare un server di gestione centrale esistente
ms:assetid: d715b24a-1256-4a7c-a5ef-1cee41d6b733
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205315(v=OCS.15)
ms:contentKeyID: 49302117
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare un server di gestione centrale esistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Se si riutilizza un server di gestione centrale di una distribuzione di Lync Server 2013 esistente, è necessario eseguire la procedura descritta di seguito per garantire il corretto funzionamento del Pannello di controllo di Lync Server e di Windows PowerShell.

## Per configurare un server di gestione centrale esistente

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Utilizzare il cmdlet **Update-CsAdminRole** per aggiornare i ruoli del controllo di accesso basato sui ruoli (RBAC) archiviati nel server di gestione centrale.
    

    > [!NOTE]
    > Non è previsto alcun output, a meno che non si verifichi un errore.


