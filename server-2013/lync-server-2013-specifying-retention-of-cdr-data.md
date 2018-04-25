---
title: Specificazione del periodo di mantenimento dei dati di registrazione dettagli chiamata
TOCTitle: Specificazione del periodo di mantenimento dei dati di registrazione dettagli chiamata
ms:assetid: c0fd6056-87bc-4136-902a-f1b37cd3a1ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182581(v=OCS.15)
ms:contentKeyID: 49301851
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Specificazione del periodo di mantenimento dei dati di registrazione dettagli chiamata

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Per impostazione predefinita, i dati di registrazione dettagli chiamata vengono eliminati dopo 60 giorni. È possibile utilizzare le impostazioni nella pagina **Registrazione dettagli chiamata** per mantenere i dati per un periodo maggiore o inferiore. Se si disabilita registrazione dettagli chiamata, verranno eliminati anche i dati acquisiti prima dell'abilitazione di registrazione dettagli chiamata.


> [!NOTE]
> È consigliabile configurare registrazione dettagli chiamata e QoE (Quality of Experience) in modo che mantengano i dati per lo stesso numero di giorni. Ogni chiamata inclusa nei rapporti Dettagli chiamata, disponibili dalla pagina Web dei rapporti di Monitoring Server, include informazioni di registrazione dettagli chiamata e QoE. Se la durata prima dell'eliminazione è diversa, alcune chiamate potrebbero includere solo dati di registrazione dettagli chiamata e altre solo dati QoE.



Nelle procedure seguenti viene descritto come configurare le impostazioni per l'eliminazione dei dati di registrazione dettagli chiamata.

## Per specificare il periodo di mantenimento dei dati di registrazione dettagli chiamata

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Monitoraggio e archiviazione** e quindi su **Registrazione dettagli chiamata**.

4.  Nella pagina **Registrazione dettagli chiamata** fare clic sul sito appropriato nella tabella, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  Per attivare l'eliminazione, selezionare **Abilita eliminazione registrazioni dettagli chiamata**.

6.  In **Mantieni registrazioni dettagli chiamata per durata massima (giorni)** selezionare il numero massimo di giorni per cui mantenere le registrazioni dettagli chiamata.

7.  In **Mantieni dati delle segnalazioni errori per durata massima (giorni)** selezionare il numero massimo di giorni per cui mantenere le segnalazioni degli errori.

8.  Fare clic su **Commit**.

## Per specificare il mantenimento delle registrazioni dettagli chiamata tramite i cmdlet di Lync Server Management Shell

È possibile creare le impostazioni di mantenimento delle registrazioni dettagli chiamata utilizzando Windows PowerShell e il cmdlet Set-CsCdrConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per specificare il mantenimento delle registrazioni dettagli chiamata per una posizione specifica

  - Questo comando consente di abilitare l'eliminazione dei dati delle registrazioni dettagli chiamata per il sito Redmond e di configurare il sito per mantenere sia tali dati che le segnalazioni di errore per 20 giorni.
    
        Set-CsCdrConfiguration -Identity "site:Redmond" -EnablePurging -KeepCallDetailForDays 20 -KeepErrorReportForDays 20

## Per specificare il mantenimento delle registrazioni dettagli chiamata per più posizioni

  - Questo comando consente di configurare il mantenimento delle registrazioni dettagli chiamata per tutte le impostazioni di configurazione di tali registrazioni in uso in un'organizzazione.
    
        Get-CsCdrConfiguration | Set-CsCdrConfiguration-EnablePurging -KeepCallDetailForDays 20 -KeepErrorReportForDays 20

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsCdrConfiguration](set-cscdrconfiguration.md).

## Vedere anche

#### Ulteriori risorse

[Registrazione dettagli chiamata (CDR) in Lync Server 2013](lync-server-2013-call-detail-recording-cdr.md)

