---
title: Abilitare o disabilitare l'hotdesking
TOCTitle: Abilitare o disabilitare l'hotdesking
ms:assetid: 93a7fed6-f61a-4b41-9336-a8320afa87cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994057(v=OCS.15)
ms:contentKeyID: 52062231
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare l'hotdesking

 

_**Ultima modifica dell'argomento:** 2013-02-20_

È possibile configurare i telefoni delle aree comuni come *telefoni di tipo Hot Desk*. Con i telefoni di tipo Hot Desk gli utenti possono accedere al proprio account utente e, dopo l'accesso, utilizzare le funzionalità di Lync Server e le impostazioni del profilo utente personale. L'hotdesking viene gestito tramite criteri client. Per abilitare o disabilitare l'hotdesking, è necessario modificare i criteri client utilizzati dai telefoni delle aree comuni. Per informazioni dettagliate su come determinare i criteri di conferenza assegnati ai telefoni delle aree comuni, vedere [Visualizzare le informazioni relative ai telefoni di area comune](lync-server-2013-view-common-area-phone-information.md).

Per abilitare o disabilitare l'hotdesking in un telefono, si utilizza il parametro EnableHotdesking del cmdlet **New-CSClientPolicy** o del cmdlet **Set-CSClientPolicy**, come indicato di seguito. Eseguire questi cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).


## Abilitazione dell'hotdesking

  - Per abilitare l'hotdesking per un telefono delle aree comuni, è necessario modificare i criteri client assegnati a tale telefono (o raccolta di telefoni).
    
    Dopo aver identificato i criteri che devono essere modificati, il passaggio successivo consiste nell'utilizzare il cmdlet **Set-CsClientPolicy** per impostare il parametro EnableHotdesking su True. Ad esempio:
    
        Set-CsClientPolicy -Identity "CommonAreaPhonePolicy" - EnableHotdesking $True

  - In alternativa, è possibile utilizzare il cmdlet **New-CsClientPolicy** per creare nuovi criteri client per l'abilitazione dell'hotdesking. Ad esempio:
    
        New-CsClientPolicy -Identity "NewCommonAreaPhonePolicy" - EnableHotdesking $True

> [!IMPORTANT]  
> Dopo aver creato questi criteri, è necessario assegnarli ai telefoni delle aree comuni appropriati. Per informazioni dettagliate, vedere <a href="lync-server-2013-assign-policies-to-a-common-area-phone.md">Assegnare criteri a un telefono di area comune</a>.

## Disabilitazione dell'hotdesking

  - Per disabilitare l'hotdesking per un telefono delle aree comuni, reimpostare il parametro EnableHotdesking del **Set-CsClientPolicy** sul valore predefinito False. Ad esempio:
    
        Set-CsClientPolicy -Identity "CommonAreaPhonePolicy" - EnableHotdesking $False

Per informazioni dettagliate, vedere gli argomenti della Guida per i cmdlet [New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy) e [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy).

