---
title: Eliminare un intervallo di numeri per la risposta alle chiamate di gruppo
TOCTitle: Eliminare un intervallo di numeri per la risposta alle chiamate di gruppo
ms:assetid: 521891f3-7a5d-45de-92dc-d57025453159
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945629(v=OCS.15)
ms:contentKeyID: 52062151
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un intervallo di numeri per la risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Utilizzare la procedura seguente per eliminare un intervallo di numeri per la risposta alle chiamate di gruppo.

## Per eliminare un intervallo di numeri per la risposta alle chiamate di gruppo

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare:
    
        Remove-CsCallParkOrbit -Identity "<group number range name>" 
    
    Ad esempio:
    
        Remove-CsCallParkOrbit -Identity "Redmond call pickup"
    

    > [!NOTE]
    > Per informazioni dettagliate su ulteriori opzioni, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit">Remove-CsCallParkOrbit</A>.



## Vedere anche

#### Attività

[Creare o modificare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)  

#### Ulteriori risorse

[Remove-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit)  
[Get-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCallParkOrbit)

