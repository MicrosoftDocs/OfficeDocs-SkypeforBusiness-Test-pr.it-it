---
title: Visualizzare le informazioni sulle impostazioni di configurazione di Lync Phone Edition
TOCTitle: Visualizzare le informazioni sulle impostazioni di configurazione di Lync Phone Edition
ms:assetid: 15f94478-651f-4063-9918-6a059f98df16
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687976(v=OCS.15)
ms:contentKeyID: 49887455
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sulle impostazioni di configurazione di Lync Phone Edition

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile visualizzare le informazioni di configurazione relative ai dispositivi che eseguono Lync Phone Edition. Le informazioni sono organizzate in raccolte. Quando si installa Lync Server, si ottiene una raccolta di impostazioni di Lync Phone Edition valide per tutti i dispositivi che eseguono Lync Phone Edition nella distribuzione. È anche possibile creare nuove raccolte di impostazioni per uno specifico sito. Le impostazioni del sito hanno la precedenza sulle impostazioni globali. In ogni raccolta di impostazioni sono disponibili nome, ambito (globale o sito), impostazione per la sicurezza SIP, livello di registrazione, livello di qualità vocale del servizio (QoS), impostazione per il blocco telefono e dettagli sul blocco telefono, ovvero la lunghezza minima del PIN di sblocco e l'intervallo di tempo prima che il telefono si blocchi.

## Per visualizzare le informazioni sulla configurazione dei dispositivi che eseguono Lync Phone Edition

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Client**, quindi sul pulsante di spostamento **Configurazione dispositivo**.

4.  Nella pagina **Configurazione dispositivo** fare clic sulla raccolta di impostazioni di cui si desidera visualizzare le informazioni. Il nome, l'ambito, l'impostazione di sicurezza SIP, il livello di qualità vocale e l'impostazione di blocco telefono sono elencate nella pagina principale. Per visualizzare il livello di registrazione e i dettagli del blocco telefono, fare clic sul menu **Modifica**, quindi su **Mostra dettagli**.

## Per visualizzare le informazioni sulla configurazione Lync Phone Edition tramite i cmdlet Lync Server Management Shell

Le impostazioni di configurazione di Lync Phone Edition possono essere inoltre visualizzate utilizzando Lync Server Management Shell e il cmdlet **Get-CsUCPhoneConfiguration**. È possibile eseguire il cmdlet da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare le informazioni di configurazione di Lync Phone Edition

  - Per visualizzare le informazioni su tutte le impostazioni di configurazione Lync Phone Edition, digitare il seguente comando nella Lync Server Management Shell e premere INVIO:
    
        Get-CsUCPhoneConfiguration
    
    Verranno restituite informazioni simili alle seguenti
    
        Identity             : Global
        CalendarPollInterval : 00:03:00
        EnforcePhoneLock     : True
        PhoneLockTimeout     : 00:10:00
        MinPhonePinLength    : 6
        SIPSecurityMode      : High
        VoiceDiffServTag     : 40
        Voice8021p           : 0
        LoggingLevel         : Off

Per informazioni dettagliate vedere [Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md).

## Vedere anche

#### Attività

[Creare o modificare una raccolta di impostazioni di configurazione di Lync Phone Edition](lync-server-2013-create-or-modify-a-collection-of-lync-phone-edition-configuration-settings.md)  
[Eliminare una raccolta esistente di impostazioni di configurazione di Lync Phone Edition](lync-server-2013-delete-an-existing-collection-of-lync-phone-edition-configuration-settings.md)  
[Configurare le impostazioni di sicurezza per Lync Phone Edition](lync-server-2013-configure-security-settings-for-lync-phone-edition.md)  
[Applicare il blocco del telefono](lync-server-2013-enforce-phone-locking.md)

