---
title: "Lync Server 2013: Preparazione dell'ambiente per VDI"
TOCTitle: Preparazione dell'ambiente per VDI
ms:assetid: a3ec2e13-1a73-4b1c-a54a-8db7d4cd50f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205154(v=OCS.15)
ms:contentKeyID: 49301546
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione dell'ambiente di Lync Server 2013 per VDI

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Per preparare l'ambiente per il plug-in VDI di Lync, l'amministratore deve eseguire le operazioni seguenti:

1.  In Lync Server 2013 verificare che l'impostazione di EnableMediaRedirection sia TRUE per tutti gli utenti VDI. Per informazioni dettagliate, vedere gli argomenti della Guida per il cmdlet [New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy) e il cmdlet [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy).

2.  Nel computer del data center installare il client Lync 2013 in tutte le macchine virtuali.

3.  Nei computer locali installare il plug-in VDI di Lync.

