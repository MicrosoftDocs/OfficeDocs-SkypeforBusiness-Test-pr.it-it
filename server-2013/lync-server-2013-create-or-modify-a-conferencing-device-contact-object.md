---
title: Creare o modificare un oggetto contatto per un dispositivo per conferenze
TOCTitle: Creare o modificare un oggetto contatto per un dispositivo per conferenze
ms:assetid: 62ed64be-379c-417d-9453-511881cf5604
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994035(v=OCS.15)
ms:contentKeyID: 52062174
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un oggetto contatto per un dispositivo per conferenze

 

_**Ultima modifica dell'argomento:** 2013-10-02_

Per creare un oggetto sala conferenze è innanzitutto necessario creare un account utente di Active Directory che rappresenti il dispositivo. Utilizzare quindi il cmdlet **Enable-CsMeetingRoom** per abilitare l'account al funzionamento come dispositivo per conferenze. Se è necessario modificare le proprietà di un dispositivo per conferenze esistente, utilizzare il cmdlet **Set-CsMeetingRoom**.

Questi cmdlet possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.




## Creazione di un dispositivo per conferenze

  - Dopo aver creato l'account utente di Active Directory che rappresenta il nuovo dispositivo per conferenze, abilitarlo tramite il cmdlet **Enable-CsMeetingRoom**. Assicurarsi di includere a) l'identità del dispositivo per conferenze, b) il pool di registrazione in cui verrà ospitato l'account per la sala, e c) l'indirizzo SIP da assegnare a tale account. Ad esempio:
    
        Enable-CsMeetingRoom -Identity "Redmond Conferencing device" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:RedmondMeetingRoom@litwareinc.com"

## Modifica di un dispositivo per conferenze

  - Per modificare i valori delle proprietà di un dispositivo per conferenze esistente, utilizzare il cmdlet **Set-CsMeetingRoom**. Il comando seguente, ad esempio, aggiorna il numero di telefono (LineUri) associato a un dispositivo per conferenze:
    
        Set-CsMeetingRoom -Identity "Redmond Conferencing device" -LineUri "tel:+12065551219"

Per informazioni dettagliate, vedere gli argomenti della Guida per i cmdlet [Enable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Enable-CsMeetingRoom) e [Set-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMeetingRoom).

