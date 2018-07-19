---
title: Configurare un'applicazione SNMP
TOCTitle: Configurare un'applicazione SNMP
ms:assetid: c4b4a736-3b2e-45b9-a965-19d22161ad57
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412972(v=OCS.15)
ms:contentKeyID: 49301893
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare un'applicazione SNMP

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Lync Server 2013 include un'interfaccia di servizio Web standard che può essere utilizzata per connettere il servizio Informazioni percorso alle applicazioni SNMP (Simple Network Management Protocol) che associano indirizzi MAC a informazioni su porte e commutatori.

Se è installata un'applicazione SNMP e il servizio Informazioni percorso non riesce a trovare una corrispondenza nel database delle posizioni, il servizio Informazioni percorso inoltrerà automaticamente una query all'applicazione tramite l'indirizzo MAC fornito dal client. Il servizio Informazioni percorso utilizzerà quindi le informazioni su porta e commutatore restituite dall'applicazione SNMP per rieseguire la query nel database delle posizioni.

Per informazioni dettagliate, vedere [Set-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsWebServiceConfiguration).


> [!NOTE]
> Gli indirizzi MAC non sono disponibili nei computer in cui è in esecuzione Windows 8.



## Per configurare l'URL dell'applicazione SNMP

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet seguente per configurare l'URL per l'applicazione SNMP.
    
        Set-CsWebServiceConfiguration -MACResolverUrl "<SNMP application url>"

