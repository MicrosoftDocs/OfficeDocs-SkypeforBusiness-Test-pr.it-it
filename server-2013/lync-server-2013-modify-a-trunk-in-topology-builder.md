---
title: Modificare un trunk in Generatore di topologie in Lync Server 2013
TOCTitle: Modificare un trunk in Generatore di topologie in Lync Server 2013
ms:assetid: 81055a82-c6f8-47b2-9779-223b1d842f36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688110(v=OCS.15)
ms:contentKeyID: 49887629
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare un trunk in Generatore di topologie in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Seguire questi passaggi per modificare l'indirizzo IP multimediale alternativo e il BypassID alternativo di un trunk.

## Per modificare l'indirizzo IP multimediale alternativo di un trunk

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsPstnGateway e modificare il campo AlternateBypassId in Lync Server Management Shell.
    
        Set-CsPstnGateway -Identity "PstnGateway:<peer FQDN> -RepresentativeMediaIP <IP address>

## Per modificare il BypassID alternativo di un trunk

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsPstnGateway e modificare il campo AlternateBypassId in Lync Server Management Shell.
    
        Set-CsPstnGateway -Identity "PstnGateway:<peer FQDN> -AlternateBypassID <identifier>

