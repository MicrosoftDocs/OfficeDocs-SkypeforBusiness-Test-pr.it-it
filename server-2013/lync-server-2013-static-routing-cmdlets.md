---
title: Cmdlet per il routing statico
TOCTitle: Cmdlet per il routing statico
ms:assetid: 71d5e0cd-8412-4383-818a-95b851a4da4b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg416492(v=OCS.15)
ms:contentKeyID: 49300949
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet per il routing statico

 

_**Ultima modifica dell'argomento:** 2012-06-20_

Con le route statiche gli amministratori possono predeterminare le route di rete utilizzate dai messaggi SIP. Quando riceve un messaggio, il server ne verifica l'indirizzo e quindi lo inoltra al server dell'hop successivo preconfigurato da un amministratore. Se configurate correttamente, le route statiche contribuiscono a garantire un recapito tempestivo e accurato dei messaggi, con un sovraccarico minimo sui server.

## Cmdlet per il routing statico

Se non diversamente indicato dal personale del supporto tecnico Microsoft, le route statiche configurate per Microsoft Lync Server 2013 devono essere create utilizzando il cmdlet [New-CsStaticRoute](new-csstaticroute.md). Dopo la creazione di una route, è possibile utilizzare i cmdlet CsStaticRoutingConfiguration per aggiungerla a un insieme di configurazioni di routing statico.

**Routing statico**

  -   
    [Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)

  -   
    [New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)

  -   
    [Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

  -   
    [Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

  -   
    [New-CsStaticRoute](new-csstaticroute.md)

  -   
    [Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)

  -   
    [New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)

  -   
    [Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

  -   
    [Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

  -   
    [New-CsSipProxyCustom](new-cssipproxycustom.md)

  -   
    [New-CsSipProxyRealm](new-cssipproxyrealm.md)

  -   
    [New-CsSipProxyTCP](new-cssipproxytcp.md)

  -   
    [New-CsSipProxyTLS](new-cssipproxytls.md)

  -   
    [New-CsSipProxyTransport](new-cssipproxytransport.md)

  -   
    [New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

  -   
    [New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

  -   
    [New-CsIssuedCertId](new-csissuedcertid.md)

## Vedere anche

#### Ulteriori risorse

[Blog di PowerShell per Lync Server](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x410)

