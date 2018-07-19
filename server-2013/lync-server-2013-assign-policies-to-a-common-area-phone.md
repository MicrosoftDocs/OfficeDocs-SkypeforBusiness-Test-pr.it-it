---
title: Assegnare criteri a un telefono di area comune
TOCTitle: Assegnare criteri a un telefono di area comune
ms:assetid: f0554fd1-b237-49b3-9eb4-26f4b91f5604
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994082(v=OCS.15)
ms:contentKeyID: 52062465
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri a un telefono di area comune

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Dopo la creazione del criterio per i telefoni di area comune (per informazioni dettagliate, vedere [Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)), sarà possibile assegnare il criterio al telefono di area comune utilizzando Windows PowerShell e il cmdlet appropriato **Grant-Cs**. Questi cmdlet possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).


## Assegnazione di un criterio a un singolo telefono di area comune

  - Il comando seguente consente di assegnare il criterio vocale per utente RedmondVoice al telefono di area comune con identità "Building 14 Lobby".
    
        Grant-CsVoicePolicy -Identity "Building 14 Lobby" -PolicyName "RedmondVoicePolicy"

## Assegnare un criterio a più telefoni di area comune

  - In questo esempio il criterio per utente RedmondVoice viene assegnato a tutti i telefoni di area comune configurati per l'utilizzo nell'organizzazione.
    
        Get-CsCommonAreaPhone | Grant-CsVoicePolicy  -PolicyName "RedmondVoicePolicy"

Per informazioni dettagliate, vedere l'argomento della Guida per [Grant-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsVoicePolicy).

## Vedere anche

#### Ulteriori risorse

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)

