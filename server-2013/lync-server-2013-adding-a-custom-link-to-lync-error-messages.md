---
title: 'Lync Server 2013: Aggiunta di un collegamento personalizzato ai messaggi di errore di Lync'
TOCTitle: Aggiunta di un collegamento personalizzato ai messaggi di errore di Lync
ms:assetid: de756088-fcc3-4e47-bde8-4fa4cc852fd1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398979(v=OCS.15)
ms:contentKeyID: 52062453
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiunta di un collegamento personalizzato ai messaggi di errore di Lync in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Per personalizzare i messaggi di errore di Lync 2013, è possibile aggiungere un collegamento alle informazioni interne per la risoluzione dei problemi o dell'help desk. A tale scopo, usare il cmdlet **New-CSClientPolicy** o **Set-CSClientPolicy** Lync Server Management Shell con il parametro CustomLinkInErrorMessages. Il testo del collegamento personalizzato è "Fare clic qui per ottenere supporto dall'amministratore" e non può essere modificato.

Con il comando seguente, ad esempio, il collegamento personalizzato viene visualizzato nell'area a piè di pagina di ogni messaggio di errore di Lync 2013 e la destinazione del collegamento viene impostata su http://contoso.com/help/LyncHelpDesk.aspx:

    New-CsClientPolicy -Identity LyncErrorLink -CustomLinkInErrorMessages "http://contoso/help/LyncHelpDesk.aspx"

Usare **Grant-CSClientPolicy** per assegnare questo nuovo criterio agli utenti. Per informazioni dettagliate, vedere **New-CSClientPolicy** e **Grant-CSClientPolicy** nella documentazione relativa a Lync Server Management Shell.

