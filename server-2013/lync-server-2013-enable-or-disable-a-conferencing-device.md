---
title: Abilitare o disabilitare un dispositivo per conferenze
TOCTitle: Abilitare o disabilitare un dispositivo per conferenze
ms:assetid: d5140e38-d015-4706-9bde-cf2fa748c36b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994070(v=OCS.15)
ms:contentKeyID: 52062445
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare un dispositivo per conferenze

 

_**Ultima modifica dell'argomento:** 2013-02-20_

È possibile abilitare e disabilitare un dispositivo per conferenze utilizzando il cmdlet **Enable-CsMeetingRoom** e il cmdlet **Disable-CsMeetingRoom**. Questi cmdlet possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.




## Abilitazione di un dispositivo per conferenze

  - Per abilitare un dispositivo per conferenze, utilizzare il cmdlet **Enable-CsMeetingRoom**. Quando si abilita un dispositivo per conferenze, è necessario includere a) l'identità del dispositivo per conferenze, b) il pool di registrazione in cui risiederà l'account della sala e c) l'indirizzo SIP da assegnare a tale account.
    
        Enable-CsMeetingRoom -Identity "Redmond Conferencing device" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:RedmondMeetingRoom@litwareinc.com"

## Disabilitazione di un dispositivo per conferenze

  - Per disabilitare un dispositivo per conferenze, utilizzare il cmdlet **Disable-CsMeetingRoom**. Assicurarsi di specificare l'identità del dispositivo per conferenze da disabilitare:
    
        Disable-CsMeetingRoom -Identity "sip:RedmondMeetingRoom@litwareinc.com"

Per informazioni dettagliate, vedere gli argomenti della Guida per i cmdlet [Enable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Enable-CsMeetingRoom) e [Disable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Disable-CsMeetingRoom).

