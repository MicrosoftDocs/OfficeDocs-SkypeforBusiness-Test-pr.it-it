---
title: Spostare un dispositivo per conferenze in un nuovo pool di registrazione
TOCTitle: Spostare un dispositivo per conferenze in un nuovo pool di registrazione
ms:assetid: 26e02ca3-e881-4f90-8bf0-b13649108100
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994025(v=OCS.15)
ms:contentKeyID: 52062122
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare un dispositivo per conferenze in un nuovo pool di registrazione

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Spostare un dispositivo per conferenze da un pool di registrazione in un altro utilizzando il cmdlet **move-csmeetingroom**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.




## Spostamento di un dispositivo per conferenze in un nuovo pool di registrazione

  - Per spostare un dispositivo per conferenze, è necessario specificare l'identità della chat room da spostare, quindi impostare il parametro di destinazione sul nome di dominio completo (FQDN) del pool di registrazione in cui verrà spostato il dispositivo. Ad esempio:
    
        move-csmeetingroom -Target "atl-cs-001.litwareinc.com" -Identity "Room 14"

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [move-csmeetingroom](https://docs.microsoft.com/en-us/powershell/module/skype/Move-CsMeetingRoom).

