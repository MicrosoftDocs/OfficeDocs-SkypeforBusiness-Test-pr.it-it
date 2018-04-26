---
title: Abilitazione di QoS per dispositivi non basati su Windows
TOCTitle: Abilitazione di QoS per dispositivi non basati su Windows
ms:assetid: 26f793df-aef8-4028-9e3b-6c2c37ea61b9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204750(v=OCS.15)
ms:contentKeyID: 49299984
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione di QoS per dispositivi non basati su Windows

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Quando si installa Microsoft Lync Server 2013, Qualità del servizio (QoS) non risulterà abilitato per i dispositivi usati nell'organizzazione che dispongono di un sistema operativo diverso da Windows. È possibile verificarlo eseguendo il comando seguente da Lync Server 2013 Management Shell:

    Get-CsMediaConfiguration

Supponendo che non siano state apportate modifiche alle impostazioni di configurazione dei supporti, dovrebbero essere visualizzate informazioni simili alle seguenti:

    Identity                          : Global
    EnableQoS                         : False
    EncryptionLevel                   : RequireEncryption
    EnableSiren                       : False
    MaxVideoRateAllowed               : VGA600K
    EnableG722StereoCodec             : True
    EnableH264Codec                   : True
    EnableAdaptiveBandwidthEstimation : True

Se la proprietà EnableQoS è impostata su False (come nell'output precedente), Qualità del servizio non è abilitato per i computer e i dispositivi che usano un sistema operativo diverso da Windows. Per impostazione predefinita, QoS è abilitato per i dispositivi Lync Phone Edition. È tuttavia possibile disabilitarlo per Lync Phone Edition.

Per abilitare Qualità del servizio nell'ambito globale, eseguire il comando seguente da Lync Server Management Shell:

    Set-CsMediaConfiguration -EnableQoS $True

Il comando precedente abilita QoS nell'ambito globale, tuttavia è importante osservare che le impostazioni di configurazione dei supporti possono essere applicate anche nell'ambito del sito. Se si desidera abilitare Qualità del servizio per un sito, è necessario includere l'Identità delle impostazioni di configurazione quando si chiama Set-CsMediaConfiguration. Questo comando, ad esempio, abilita QoS per il sito di Redmond:

    Set-CsMediaConfiguration -Identity site:Redmond -EnableQoS $True


> [!NOTE]
> Non è sempre necessario abilitare QoS nell'ambito del sito. Le impostazioni assegnate all'ambito del sito hanno la precedenza su quelle assegnate all'ambito globale. Si supponga che QoS sia abilitato nell'ambito globale ma che sia disabilitato nell'ambito del sito (per il sito di Redmond.) In questo caso, Qualità del servizio verrà disabilitato per il sito di Redmond, in quanto le impostazioni del sito sono prioritarie. Per abilitare QoS per il sito di Redmond, sarà necessario usare le impostazioni di configurazione dei supporti applicate a tale sito.



Se si desidera abilitare QoS contemporaneamente per le impostazioni di configurazione di tutti i supporti (indipendentemente dall'ambito), eseguire questo comando da Lync Server Management Shell:

    Get-CsMediaConfiguration | Set-CsMediaConfiguration -EnableQoS $True

È possibile disabilitare QoS per i dispositivi che usano un sistema operativo diverso da Windows impostando il valore della proprietà EnableQoS su False, ad esempio:

    Set-CsMediaConfiguration -Identity site:Redmond -EnableQoS $False

Questo consente di implementare QoS su alcune parti della rete, ad esempio nel sito di Redmond, e lasciarlo disabilitato su altre parti.

QoS può essere abilitato e disabilitato solo usando Lync Server Management Shell. Queste opzioni non sono disponibili nel Pannello di controllo di Lync Server.

