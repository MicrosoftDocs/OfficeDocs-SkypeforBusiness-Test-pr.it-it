---
title: Modificare le impostazioni della qualità percepita dagli utenti
TOCTitle: Modificare le impostazioni della qualità percepita dagli utenti
ms:assetid: a6b41de2-1466-4240-8a70-14ce6f0f3ddc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182563(v=OCS.15)
ms:contentKeyID: 49301579
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare le impostazioni della qualità percepita dagli utenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Per impostazione predefinita, i dati relativi alla QoE (Quality of Experience) vengono eliminati dopo 60 giorni. È possibile utilizzare le impostazioni nella pagina **Dati QoE** per conservare i dati per un periodo superiore o inferiore. Se si disabilita la funzionalità QoE, verranno eliminati anche i dati acquisiti prima dell'abilitazione di questa funzionalità.


> [!NOTE]
> È consigliabile configurare la registrazione dettagli chiamata (CDR, Call Detail Recording) e QoE in modo che mantengano i dati per lo stesso numero di giorni. Ogni chiamata inclusa nei rapporti Dettagli chiamata, disponibili dalla home page dei rapporti di monitoraggio, include informazioni di registrazione dettagli chiamata e QoE. Se il periodo che precede l'eliminazione è diverso, alcune chiamate potrebbero includere solo dati di registrazione dettagli chiamata e altre solo dati QoE.



Nella procedura seguente viene descritto come configurare le impostazioni per l'eliminazione dei dati QoE.

## Per specificare il periodo di mantenimento dei dati QoE tramite il Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Monitoraggio e archiviazione** e quindi su **Dati QoE**.

4.  Nella pagina **Dati QoE** fare clic sul sito appropriato nella tabella, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  Per abilitare l'eliminazione, selezionare **Abilita eliminazione dei dati QoE**.

6.  In **Mantieni dati QoE per durata massima (giorni)** selezionare il numero massimo di giorni per cui mantenere i dati QoE.

7.  Fare clic su **Commit**.

## Per specificare il mantenimento dei dati QoE tramite i cmdlet di Windows PowerShell

È possibile creare le impostazioni di mantenimento dei dati QoE utilizzando Windows PowerShell e il cmdlet **Set-CsQoEConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per specificare il mantenimento dei dati QoE per una posizione specifica

  - Questo comando consente di abilitare l'eliminazione dei dati QoE per il sito Redmond e di configurare il sito per mantenere i dati QoE per 20 giorni.
    
        Set-CsQoeConfiguration -Identity "site:Redmond" -EnablePurging -KeepQoEDataForDays 20

## Per specificare il mantenimento dei dati QoE per più posizioni

  - Questo comando consente di configurare il mantenimento dei dati QoE per tutte le impostazioni di configurazione QoE in uso in un'organizzazione.
    
        Get-CsQoEConfiguration | Set-CsQoEConfiguration-EnablePurging -KeepQoEDataForDays 20 

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsQoEConfiguration](set-csqoeconfiguration.md).

## Vedere anche

#### Ulteriori risorse

[Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md)

