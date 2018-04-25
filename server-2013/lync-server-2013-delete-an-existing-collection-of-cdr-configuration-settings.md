---
title: Eliminare una raccolta esistente di impostazioni di configurazione di registrazione dettagli chiamata
TOCTitle: Eliminare una raccolta esistente di impostazioni di configurazione di registrazione dettagli chiamata
ms:assetid: 8ebf5da8-c0fc-498c-8d85-527d3be8479a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688128(v=OCS.15)
ms:contentKeyID: 49887649
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta esistente di impostazioni di configurazione di registrazione dettagli chiamata

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle sessioni di messaggistica istantanea peer-to-peer, delle chiamate telefoniche VoIP (Voice over Internet Protocol) e delle conferenze telefoniche. Questi dati sull'utilizzo includono informazioni sui chiamanti, sugli utenti chiamati, sulla data della chiamata e sulla durata della conversazione.

Quando si installa Microsoft Lync Server 2013, viene automaticamente creata una singola raccolta globale di importazioni di Registrazione dettagli chiamata. Gli amministratori hanno inoltre la possibilità di creare raccolte di impostazioni personalizzate applicate ai singoli siti. Le impostazioni configurate nell'ambito del sito hanno precedenza su quelle configurate nell'ambito globale. Se si eliminano le impostazioni con ambito a livello di sito, la Registrazione dettagli chiamata viene gestita nel sito in base alle impostazioni globali.

Tenere presente che è anche possibile "eliminare" le impostazioni globali. Tuttavia, le impostazioni globali non vengono effettivamente rimosse. Invece, tutte le proprietà nella raccolta vengono reimpostate sui valori predefiniti. Ad esempio, per impostazione predefinita la rimozione è abilitata in una raccolta delle impostazioni di configurazione di Registrazione dettagli chiamata. Supponiamo di modificare la raccolta globale in modo da disabilitare la rimozione. Se successivamente si eliminano le impostazioni globali, tutte le proprietà verranno reimpostate sui valori predefiniti. In questo caso, ciò significa che l'eliminazione verrà riabilitata.

È possibile rimuovere le impostazioni di Registrazione dettagli chiamata mediante il Pannello di controllo di Lync Server oppure il cmdlet [Remove-CsCdrConfiguration](remove-cscdrconfiguration.md).

## Per rimuovere le impostazioni di configurazione di Registrazione dettagli chiamata mediante il Pannello di controllo di Lync Server

1.  Nel Pannello di controllo di Lync Server fare clic su **Monitoraggio e archiviazione**.

2.  Nella scheda **Registrazione dettagli chiamata** selezionare la raccolta (o le raccolte) delle impostazioni di Registrazione dettagli chiamata da rimuovere. Per selezionare più raccolte, fare clic sulla prima raccolta, tenere premuto il tasto CTRL e fare clic sulle raccolte aggiuntive.

3.  Fare clic su **Modifica** e quindi scegliere **Elimina**.

4.  Nella finestra di dialogo Pannello di controllo di Lync Server fare clic su **OK**.

## Per rimuovere le impostazioni di configurazione di Registrazione dettagli chiamata mediante i cmdlet della Lync Server Management Shell

È possibile eliminare le impostazioni di configurazione di Registrazione dettagli chiamata mediante Windows PowerShell e il cmdlet **Remove-CsCdrConfiguration**. Questo cmdlet può essere eseguito dalla Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere una raccolta specificata delle impostazioni di configurazione di Registrazione dettagli chiamata

  - Questo comando rimuove le impostazioni di configurazione di Registrazione dettagli chiamata applicate al sito Redmond:
    
        Remove-CsCdrConfiguration -Identity "site:Redmond"

## Per rimuovere tutte le impostazioni di configurazione di Registrazione dettagli chiamata applicate all'ambito del sito

  - Questo comando rimuove tutte le impostazioni di configurazione di Registrazione dettagli chiamata applicate all'ambito del sito:
    
        Get-CsCdrConfiguration -Filter "site:*" | Remove-CsCdrConfiguration

## Per rimuovere tutte le impostazioni di configurazione della Registrazione dettagli chiamata che disabilitano la registrazione dei dettagli:

  - Questo comando rimuove tutte le impostazioni di configurazione della Registrazione dettagli chiamata per cui la registrazione dei dettagli è stata disabilitata:
    
        Get-CsCdrConfiguration | Where-Object {$_.EnableCDR -eq $False} | Remove-CsCdrConfiguration

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Remove-CsCdrConfiguration](remove-cscdrconfiguration.md).

