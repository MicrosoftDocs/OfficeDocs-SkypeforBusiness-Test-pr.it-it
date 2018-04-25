---
title: Convalidare gli indirizzi
TOCTitle: Convalidare gli indirizzi
ms:assetid: aae557c9-e6f5-4d23-8af1-1d4cd7968c54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412808(v=OCS.15)
ms:contentKeyID: 49301631
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Convalidare gli indirizzi

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Prima di pubblicare il database delle posizioni, è necessario convalidare le nuove posizioni in base allo stradario generale gestito dal provider dei servizi di emergenza del trunk SIP o della rete PSTN (Public Switched Telephone Network) .

Per informazioni dettagliate sui provider dei servizi di emergenza del trunk SIP, vedere [Scelta di un provider di servizi di emergenza per Lync Server 2013](lync-server-2013-choosing-an-e9-1-1-service-provider.md).

Per informazioni dettagliate sulla convalida degli indirizzi, vedere la documentazione di Lync Server Management Shell relativa ai cmdlet seguenti:

  - **Get-CsLisServiceProvider**

  - **Set-CsLisServiceProvider**

  - **Remove-CsLisServiceProvider**

  - **Get-CsLisCivicAddress**

  - **Test-CsLisCivicAddress**

## Per convalidare gli indirizzi presenti nel database delle posizioni

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire i seguenti cmdlet per configurare la connessione del provider dei servizi di emergenza.
    
        $pwd = Read-Host -AsSecureString <password>
        Set-CsLisServiceProvider -ServiceProviderName Provider1 -ValidationServiceUrl <URL provided by provider> -CertFileName <location of certificate provided by provider> -Password $pwd

3.  Per convalidare gli indirizzi nel database delle posizioni, eseguire il cmdlet seguente.
    
        Get-CsLisCivicAddress | Test-CsLisCivicAddress -UpdateValidationStatus
    
    Per convalidare indirizzi singoli, è inoltre possibile utilizzare il cmdlet **Test-CsLisCivicAddress**.

