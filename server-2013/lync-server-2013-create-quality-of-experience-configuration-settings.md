---
title: Creare le impostazioni di configurazione per la qualità percepita dagli utenti
TOCTitle: Creare le impostazioni di configurazione per la qualità percepita dagli utenti
ms:assetid: 64f05569-07c7-4f76-a96b-ea4125a510d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521006(v=OCS.15)
ms:contentKeyID: 49300791
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare le impostazioni di configurazione per la qualità percepita dagli utenti

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Le metriche QoE (Quality of Experience) registrano la qualità delle chiamate audio e video effettuate nell'organizzazione, includendo informazioni quali il numero di pacchetti di rete persi, i rumori di fondo e la quantità di "instabilità" (differenze nel ritardo dei pacchetti). Queste metriche vengono archiviate in un database separatamente rispetto ad altri dati, ad esempio i dati di registrazione dettagli chiamata (CDR, Call Detail Record), in modo che sia possibile abilitare e disabilitare il servizio QoE in maniera indipendente rispetto ad altre registrazioni di dati.

Quando si installa Microsoft Lync Server 2013, viene creata automaticamente una singola raccolta globale di impostazioni di configurazione QoE. Gli amministratori hanno inoltre la possibilità di creare impostazioni personalizzato con ambito sito. Ogni volta che vengono utilizzate tali impostazioni con ambito sito, queste avranno la precedenza rispetto alle impostazioni globali. Se si creano impostazioni con ambito sito per il sito Redmond, ad esempio, per gestire i criteri QoE nel sito di Redmond verranno utilizzate tali impostazioni, anziché quelle globali.

Le impostazioni di configurazione QoE possono essere create tramite il Pannello di controllo di Lync Server o il cmdlet [New-CsQoEConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsQoEConfiguration). Se si utilizza il Pannello di controllo di Lync Server per creare le nuove impostazioni, saranno disponibili le opzioni seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione dell'interfaccia utente</th>
<th>Parametro di PowerShell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome</p></td>
<td><p>Identità</p></td>
<td><p>Identificatore univoco delle impostazioni da creare. Le impostazioni di configurazione QoE possono essere create solo in ambito di sito.</p></td>
</tr>
<tr class="even">
<td><p>Abilita monitoraggio dei dati QoE</p></td>
<td><p>EnableQoE</p></td>
<td><p>Indica se i record QoE verranno raccolti e salvati nel database di monitoraggio.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita eliminazione dei dati QoE</p></td>
<td><p>EnablePurging</p></td>
<td><p>Indica se i record verranno cancellati dopo la scadenza specificata nella proprietà <strong>Mantieni dati QoE per durata massima (giorni)</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Mantieni dati QoE per durata massima (giorni)</p></td>
<td><p>KeepQoEDataForDays</p></td>
<td><p>Il numero di giorni in cui i dati QoE verranno archiviati prima di essere eliminati dal database. Questo valore viene ignorato se l'eliminazione è disabilitata.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Il nuovo cmdlet New-CsQoEConfiguration include ulteriori opzioni non disponibili in Pannello di controllo di Lync Server. Per ulteriori informazioni, vedere l'argomento della Guida relativo a <A href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsQoEConfiguration">New-CsQoEConfiguration</A>.



## Per creare le impostazioni di configurazione QoE tramite il Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Monitoraggio e archiviazione** e quindi su **Dati QoE**.

4.  Nella pagina **Dati QoE** fare clic su **Nuovo**.

5.  In **Seleziona un sito** fare clic sul sito a cui si desidera applicare i criteri e quindi fare clic su **OK**.

6.  In **Crea nuova impostazione QoE** eseguire le operazioni seguenti:
    
      - Selezionare **Abilita monitoraggio dei dati QoE** per attivare il monitoraggio.
    
      - Selezionare **Abilita eliminazione dei dati QoE** per attivare l'eliminazione.
    
      - In **Mantieni dati QoE per durata massima (giorni)** selezionare il numero massimo di giorni per il mantenimento dei record QoE.

7.  Fare clic su **Commit**.

## Per creare le impostazioni di configurazione QoE tramite i cmdlet di Windows PowerShell

È inoltre possibile creare le impostazioni di configurazione QoE tramite Windows PowerShell e il cmdlet New-CsQoEConfiguration. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per creare una nuova raccolta di impostazioni di configurazione QoE

  - Questo comando crea una nuova raccolta di impostazioni di configurazione QoE per il sito Redmond:
    
        New-CsQoEConfiguration -Identity "site:Redmond"

## Per creare una nuova raccolta di impostazioni di configurazione QoE in cui il monitoraggio QoE è disabilitato

  - Dal momento che nel comando precedente non sono stati specificati parametri, oltre al parametro Identity obbligatorio, la nuova raccolta di impostazioni di configurazione utilizzerà i valori predefiniti per ogni proprietà. Per creare impostazioni che utilizzano valori di proprietà diversi, includere semplicemente il parametro e il valore di parametro appropriato. Per creare una raccolta di impostazioni di configurazione QoE che consenta la disabilitazione della registrazione QoE per impostazione predefinita, utilizzare un comando come il seguente:
    
        New-CsQoEConfiguration -Identity "site:Redmond" -EnableQoE $False

## Per specificare più valori di proprietà durante la creazione di una nuova raccolta di impostazioni di configurazione QoE

  - È possibile specificare più valori di proprietà includendo più parametri. Questo comando, ad esempio, configura le nuove impostazioni per mantenere i dati QoE per 30 giorni ed eliminare i dati obsoleti alle 3.00:
    
        New-CsQoEConfiguration -Identity "site:Redmond" -KeepQoEDataForDays 30 -PurgeHourOfDay 3

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [New-CsQoEConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsQoEConfiguration).

