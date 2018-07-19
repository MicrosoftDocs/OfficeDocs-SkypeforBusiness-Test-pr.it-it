---
title: Visualizzare le informazioni relative ai telefoni di area comune
TOCTitle: Visualizzare le informazioni relative ai telefoni di area comune
ms:assetid: e652240c-6a3f-4be7-a083-32f24c08e655
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994081(v=OCS.15)
ms:contentKeyID: 52062462
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni relative ai telefoni di area comune

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Per visualizzare informazioni sui telefoni di area comune configurati per l'utilizzo nell'organizzazione, utilizzare il cmdlet **Get-CsCommonAreaPhone**. Se non si specificano parametri, questo cmdlet restituisce informazioni su tutti i telefoni di area comune. I parametri facoltativi offrono modi diversi per filtrare le informazioni. Ad esempio, è possibile restituire tutti i telefoni di area comune con oggetti contatto in un'unità organizzativa specificata oppure tutti gli oggetti contatto presenti in un edificio specificato. Per informazioni dettagliate sui parametri **Get-CsCommonAreaPhone**, vedere [Get-CsCommonAreaPhone](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCommonAreaPhone).

Eseguire **Get-CsCommonAreaPhone** da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


## Visualizzazione di informazioni su tutti i telefoni di area comune

  - Per visualizzare informazioni su tutti i telefoni di area comune, digitare il comando seguente in Lync Server Management Shell, quindi premere INVIO:
    
        Get-CsCommonAreaPhone
    
    Verranno visualizzate informazioni analoghe alle seguenti:
    
        Identity           : CN=Building 14 Lobby,OU=Redmond,
                             DC=litwareinc,DC=com
        RegistrarPool      : atl-cs-001.litwareinc.com
        Enabled            : True
        SipAddress         : sip:4714e34b-9781-421d-b07a-
                             52056b5b4a56@litwareinc.com
        ClientPolicy       :
        PinPolicy          :
        VoicePolicy        :
        MobilityPolicy     :
        GroupChatPolicy    :
        ConferencingPolicy :
        LineURI            : tel:+14255550712
        DisplayNumber      : 1-425-555-0712
        DisplayName        : Building 14 Lobby
        Description        :
        ExUmEnabled        : False

Per informazioni dettagliate, vedere l'argomento della guida relativo al cmdlet [Get-CsCommonAreaPhone](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCommonAreaPhone).

