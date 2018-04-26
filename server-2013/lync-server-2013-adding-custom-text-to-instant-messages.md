---
title: 'Lync Server 2013: Aggiunta di testo personalizzato ai messaggi istantanei'
TOCTitle: Aggiunta di testo personalizzato ai messaggi istantanei
ms:assetid: cabcc3ec-9d35-42ac-a403-e21b7d538c2c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398847(v=OCS.15)
ms:contentKeyID: 52062266
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiunta di testo personalizzato ai messaggi istantanei in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Per aggiungere una declinazione di responsabilità o un avviso all'inizio di ogni conversazione istantanea di Lync 2013, è possibile usare il cmdlet **New-CSClientPolicy** o **Set-CSClientPolicy**Lync Server Management Shell con il parametro IMWarning.

Il comando nell'esempio seguente aggiunge un promemoria di sicurezza in alto nella finestra di conversazione all'inizio di ogni nuova conversazione istantanea:

    New-CsClientPolicy -Identity IMSecurityNotice -IMWarning 
    "Remember, security is everyone's responsibility. Keep it confidential."

Usare **Grant-CSClientPolicy** per assegnare questo nuovo criterio agli utenti. Per informazioni dettagliate, vedere **New-CSClientPolicy** e **Grant-CSClientPolicy** nella documentazione relativa a Lync Server Management Shell.

