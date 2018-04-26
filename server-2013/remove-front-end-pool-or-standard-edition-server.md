---
title: Rimuovere pool Front End o server Standard Edition
TOCTitle: Rimuovere pool Front End o server Standard Edition
ms:assetid: 83c39a36-49a1-4ac6-9cc5-b0e441b1fdec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688115(v=OCS.15)
ms:contentKeyID: 49887633
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere pool Front End o server Standard Edition

 

_**Ultima modifica dell'argomento:** 2012-10-04_

In questo argomento vengono fornire informazioni dettagliate per la rimozione di un pool Front End o un server Standard Edition Front End Server. Quando si rimuove un pool Front End, come parte del processo di rimozione viene rimosso ogni Front End Server appartenente al pool. Quando si rimuove un server Standard Edition Front End Server, è necessario rimuovere la definizione dell'archivio SQL da Generatore di topologie.

## Per rimuovere un pool di Font End Server

1.  Aprire il Generatore di topologie.

2.  Passare al nodo Lync Server 2010.

3.  Espandere **Pool Enterprise Edition Front End** , espandere pool Front End, fare clic con il pulsante destro del mouse sul pool Front End che si desidera rimuovere e quindi scegliere **Elimina** .

4.  Pubblicare la topologia, controllare lo stato di replica e quindi eseguire la Distribuzione guidata di Lync Server secondo le esigenze.

## Per rimuovere un server Standard Edition Front End Server

1.  Aprire il Generatore di topologie.

2.  Passare al nodo Lync Server 2010.

3.  Espandere **Standard Edition Front End Server** , fare clic con il pulsante destro del mouse sul server Front End Server che si desidera rimuovere e quindi scegliere **Elimina** .

4.  Espandere **Archivi SQL** , fare clic con il pulsante destro del mouse sul database di SQL Server associato a Standard Edition Front End Server e quindi scegliere **Elimina** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>È necessario rimuovere la definizione dei database di SQL Server collocati da Standard Edition Front End Server.</td>
    </tr>
    </tbody>
    </table>


5.  Pubblicare la topologia, controllare lo stato di replica e quindi eseguire la Distribuzione guidata di Lync Server secondo le esigenze.

