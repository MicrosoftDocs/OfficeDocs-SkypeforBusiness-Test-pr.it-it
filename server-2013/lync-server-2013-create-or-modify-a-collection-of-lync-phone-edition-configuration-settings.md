---
title: Creare o modificare una raccolta di impostazioni di configurazione di Lync Phone Edition
TOCTitle: Creare o modificare una raccolta di impostazioni di configurazione di Lync Phone Edition
ms:assetid: 6cf714af-8f57-4a71-89ad-0a776302b2ba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688086(v=OCS.15)
ms:contentKeyID: 49887598
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una raccolta di impostazioni di configurazione di Lync Phone Edition

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Quando si installa Lync Server, si ottiene l'intera raccolta di impostazioni di Lync Phone Edition, che si applicano a tutti i dispositivi che eseguono Lync Phone Edition nella distribuzione. È possibile modificare queste impostazioni in qualunque momento. È inoltre possibile configurare una nuova raccolta di impostazioni da applicare a dispositivi in un sito specifico. Queste hanno la precedenza sulla impostazioni globali.

Le impostazioni di configurazione consistono nel nome della raccolta, l'ambito (globale o sito), l'impostazione di sicurezza SIP, il livello di registrazione, il livello della qualità del servizio (QoS) vocale, l'impostazione di blocco del telefono e i dettagli di blocco del telefono, ovvero: a) la lunghezza del PIN e b) la durata dell'inattività del telefono prima del blocco.

## Come creare una raccolta di impostazioni di configurazione di Lync Phone Edition o modificare le impostazioni di una raccolta esistente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione dispositivo**.

4.  Nella pagina **Configurazione dispositivo** effettuare una delle seguenti operazioni:
    
      - Per creare una nuova raccolta di impostazioni di configurazione di Lync Phone Edition, fare clic su **Nuovo**, selezionare un sito, fare clic su **OK**, rivedere le impostazioni predefinite e, se lo si desidera, apportare eventuali modifiche.
    
      - Per modificare le impostazioni di una raccolta esistente, fare clic sulla raccolta, selezionare il menu **Modifica**, fare clic su **Mostra dettagli** e apportare le modifiche.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per tornare a utilizzare le impostazioni predefinite di una raccolta globale, fare clic sulla stessa, quindi sul menu <strong>Modifica</strong> e su <strong>Elimina</strong>, quindi fare clic su <strong>OK</strong>. La raccolta globale non viene eliminata, ma le impostazioni vengono ripristinate ai valori predefiniti.</td>
        </tr>
        </tbody>
        </table>


5.  Fare clic su **Commit**.

## Le nuove impostazioni di configurazione di Lync Phone Edition vengono create tramite il cmdlet Lync Server Management Shell.

È inoltre possibile creare impostazioni di configurazione di Lync Phone Edition (solo a livello di sito) tramite i cmdlet Lync Server Management Shell e **New-CsUCPhoneConfiguration**, eseguibili da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Come creare nuove impostazioni di configurazione di Lync Phone Edition che utilizzano i valori predefiniti

  - Con questo comando viene creata una nuova raccolta di impostazioni del telefono UC per il sito Redmond.
    
        New-CsUCPhoneConfiguration -Identity "site:Redmond"
    
    Dal momento che nel comando precedente non sono specificati altri parametri (oltre al parametro Identity, che è obbligatorio), questa nuova raccolta di impostazioni di configurazione utilizzerà i valori predefiniti per tutte le proprietà.

## Come cambiare il valore di una proprietà singola durante la creazione di nuove impostazioni di configurazione di Lync Phone Edition

  - Per creare impostazioni che utilizzano diversi valori di proprietà, è sufficiente includere il parametro e il valore del parametro appropriati. Ad esempio, per creare una raccolta di impostazioni di configurazione del telefono UC che, per impostazione predefinita, richiedono il blocco del telefono, utilizzare un comando come il seguente:
    
        New-CsUCPhoneConfiguration -Identity "site:Redmond" -EnforcePhoneLock $True

## Come cambiare i valori di più proprietà durante la creazione di nuove impostazioni di configurazione di Lync Phone Edition

  - I valori di proprietà multiple possono essere modificati includendo parametri multipli. Ad esempio, questo comando impone il blocco del telefono e imposta la lunghezza minima del PIN su 8 cifre:
    
        New-CsUCPhoneConfiguration -Identity "site:Redmond" -EnforcePhoneLock $True -MinPhonePinLength 8

Per informazioni dettagliate, vedere [New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md).

## Vedere anche

#### Attività

[Eliminare una raccolta esistente di impostazioni di configurazione di Lync Phone Edition](lync-server-2013-delete-an-existing-collection-of-lync-phone-edition-configuration-settings.md)  
[Configurare le impostazioni di sicurezza per Lync Phone Edition](lync-server-2013-configure-security-settings-for-lync-phone-edition.md)  
[Applicare il blocco del telefono](lync-server-2013-enforce-phone-locking.md)

