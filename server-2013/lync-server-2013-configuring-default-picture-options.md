---
title: Configurazione delle opzioni immagine predefinite
TOCTitle: Configurazione delle opzioni immagine predefinite
ms:assetid: b1c986f0-6400-447a-9e36-78c1c3a4f793
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn205074(v=OCS.15)
ms:contentKeyID: 53901534
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle opzioni immagine predefinite

 

_**Ultima modifica dell'argomento:** 2013-03-22_

Per impostazione predefinita, le immagini degli utenti vengono visualizzate automaticamente. Gli utenti che desiderano nascondere la propria immagine possono selezionare l'opzione **Nascondi immagine** nel client Lync, tuttavia questa impostazione viene ignorata da alcune altre applicazioni di Office.

Se la possibilità che l'immagine venga visualizzata anche se l'utente ha scelto altrimenti rappresenta un problema, è possibile modificare le opzioni di visualizzazione delle immagini di Lync a livello globale per un sito o un servizio, in modo che le immagini degli utenti non vengano visualizzate per impostazione predefinita. Usare il cmdlet di Lync Server Management Shell seguente per fare in modo che le immagini non vengano visualizzate a meno che l'utente non selezioni esplicitamente l'opzione **Mostra immagine** nel client:

    Set-CsPrivacyConfiguration -DisplayPublishedPhotoDefault $False

Per ulteriori informazioni su questo cmdlet, vedere l'argomento [Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md) nella documentazione relativa a Lync Server Management Shell.

