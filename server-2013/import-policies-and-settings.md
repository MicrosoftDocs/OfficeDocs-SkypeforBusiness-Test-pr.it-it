---
title: Importare criteri e impostazioni
TOCTitle: Importare criteri e impostazioni
ms:assetid: b25decee-2ee5-4836-b370-454411d39252
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205178(v=OCS.15)
ms:contentKeyID: 49301703
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Importare criteri e impostazioni

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Dopo aver unito le informazioni della topologia di Office Communications Server 2007 R2 al pool pilota di Lync Server 2013, è necessario eseguire un cmdlet di Lync Server 2013 Management Shell per eseguire la migrazione delle impostazioni di configurazione e dei criteri di Office Communications Server 2007 R2 nel pool pilota di Lync Server 2013.

Il cmdlet **Import-CsLegacyConfiguration** importa in Lync Server 2013 criteri, route vocali, dial plan, URL di Communicator Web Access e numeri di accesso esterno.

## Per eseguire la migrazione di criteri e impostazioni

1.  Nel Front End Server di Lync Server 2013 avviare Lync Server Management Shell.

2.  Nella riga di comando digitare quanto segue:
    
        Import-CsLegacyConfiguration
    
    Dopo l'importazione dei criteri, utilizzare la procedura riportata di seguito per visualizzare nel Pannello di controllo di Lync Server i criteri importati.

## Per visualizzare i criteri importati

1.  Aprire il Pannello di controllo di Lync Server 2013.

2.  Fare clic su **Routing vocale** e visualizzare i criteri importati.

3.  Fare clic su **Servizio di conferenza** e visualizzare i criteri importati.

4.  Fare clic su **Federazione e accesso esterno** e visualizzare i criteri importati.

5.  Fare clic su **Monitoraggio e archiviazione** e visualizzare i criteri importati.

