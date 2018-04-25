---
title: Configurare un servizio Informazioni percorso secondario
TOCTitle: Configurare un servizio Informazioni percorso secondario
ms:assetid: 083ffbc6-7c18-4141-85f9-8825b62c3d10
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398138(v=OCS.15)
ms:contentKeyID: 49299595
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare un servizio Informazioni percorso secondario

 

_**Ultima modifica dell'argomento:** 2012-10-30_

In Lync Server 2013 è disponibile un'interfaccia di servizio Web che è possibile utilizzare per far puntare il servizio Informazioni percorso a un database SLS (Secondary Location Source). L'interfaccia di servizio Web che si connette al database SLS deve essere conforme al codice WSDL del servizio Informazioni percorso. Se sono configurati un database delle posizioni e un database SLS, il servizio Informazioni percorso innanzitutto interrogherà il database delle posizioni e, se non vengono trovate corrispondenze, invierà la richiesta della posizione dal client al database SLS. Se la posizione esiste nel database SLS, il servizio Informazioni percorso restituirà la posizione al client.

Per informazioni dettagliate, vedere nella documentazione di Lync Server Management Shell il cmdlet seguente:

  - **Set-CsWebServiceConfiguration**

## Per configurare il database SLS

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet seguente per configurare l'URL del percorso del database SLS.
    
        Set-CsWebServiceConfiguration -SecondaryLocationSourceURL "<web service url>"

