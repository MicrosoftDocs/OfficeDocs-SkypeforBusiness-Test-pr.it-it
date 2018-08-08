---
title: "Lync Server 2013: Pianifica il ripristino di emergenza dei Response Group"
TOCTitle: Pianificazione per il ripristino di emergenza dei Response Group
ms:assetid: 14e0f5dc-77cd-42cd-a9c9-4d0da38fb1cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204699(v=OCS.15)
ms:contentKeyID: 49299771
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione per il ripristino di emergenza dei Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono illustrati alcuni modi per preparare i Response Group per ripristini di emergenza e fornita una panoramica del processo di ripristino di emergenza.

## Preparazione del ripristino di emergenza di Response Group

Durante la preparazione e l'esecuzione delle procedure di ripristino di emergenza, tenere presente quanto segue.


> [!NOTE]
> Per le procedure di ripristino di emergenza illustrate in questo documento, in un ambiente di coesistenza sono supportati solo i Response Group di Lync Server 2013.



  - Pianificare il ripristino di emergenza durante la pianificazione delle capacità. Per le capacità del ripristino di emergenza, ogni pool appartenente a una coppia deve essere in grado di gestire i carichi di lavoro di tutti i Response Group di entrambi i pool. Per informazioni dettagliate sulla pianificazione delle capacità di Response Group, vedere [Pianificazione della capacità per Response Group in Lync Server 2013](lync-server-2013-capacity-planning-for-response-group.md).

  - Eseguire regolarmente copie di backup di tutte le configurazioni dei Response Group in tutti i pool Front End in cui è stata distribuita l' applicazione Response Group utilizzando la procedura di esportazione illustrata in questo documento. Per informazioni dettagliate, vedere [Procedure per il ripristino di emergenza dei Response Group in Lync Server 2013](lync-server-2013-response-group-disaster-recovery-procedures.md). Conservare le copie di backup in una posizione sicura.

  - Conservare una copia di backup separata di tutti i file audio originali utilizzati per l' applicazione Response Group, compresi eventuali registrazioni o file di musica di attesa. Conservare le copie di backup in una posizione sicura.

  - Per il ripristino di emergenza in Lync Server 2013, è necessario che tutte le impostazioni Response Group dispongano di un nome univoco in tutta la distribuzione. Questo requisito si applica a flussi di lavoro, code, gruppi di agenti, set di festività e orario di ufficio. È opportuno verificare che questo requisito sia soddisfatto quando i pool principale e di backup sono ancora attivi e prima di avviare una procedura di failover. Se vengono rilevati conflitti di nome durante l'importazione dei dati dei Response Group al pool di backup, l'importazione non riesce. Per completare l'importazione e la procedura di failover, è necessario risolvere i conflitti di nome rinominando l'oggetto Response Group nel pool di backup o utilizzando il cmdlet **Import-CsRgsConfiguration** con il parametro –ResolveNameConflicts affinché risolva automaticamente il conflitto aggiungendo un numero di identificazione univoco all'oggetto Response Group.

  - In generale, è consigliabile eseguire backup giornalieri, ma in presenza di un volume elevato di modifiche è possibile pianificare backup più frequenti. La quantità di informazioni che è possibile perdere in caso di emergenza varia in base alla frequenza dei backup, oltre che alla frequenza e al volume di modifiche.

  - È possibile importare i Response Group in un pool di backup prima di un'operazione di failover o di una situazione di emergenza. L'importazione anticipata dei Response Group riduce i tempi di inattività perché il Lync Server, Response Group Service può essere ripristinato nel pool di backup non appena le chiamate sono instradate al pool di backup.
    

    > [!NOTE]
    > L' applicazione Response Group non può raggiungere gli agenti ospitati in un pool inattivo fino al completamento del failover. Durante questo tempo, l' applicazione Response Group elabora le chiamate come se tali agenti non fossero disponibili.



## Processo di ripristino di emergenza dei Response Group

In caso di emergenza, è possibile ripristinare i Response Group utilizzando uno dei seguenti metodi di ripristino:

  - Eseguire il failover su un pool di backup e quindi il failback sul pool originale.

  - Eseguire il failover su un pool di backup, creare un nuovo pool con un nome di dominio completo (FQDN) differente, quindi importare i Response Group nel nuovo pool.

Durante la fase di failover del ripristino di emergenza, i Response Group risiedono sia nel pool principale (non disponibile) che in quello di backup. Tali Response Group hanno lo stesso nome e lo stesso proprietario (il pool principale), ma padri diversi.

Quando si esegue il ripristino creando un nuovo pool con un FQDN diverso, è necessario assegnare il nuovo pool come proprietario dei Response Group al momento dell'importazione. La proprietà dei Response Group rimane nel pool originale se non viene esplicitamente riassegnata dall'utente utilizzando il parametro –OverwriteOwner con il cmdlet **Import-CsRgsConfiguration**.


> [!NOTE]
> Il parametro –OverwriteOwner deve inoltre essere utilizzato se è stato ricostruito il pool durante il ripristino (ovvero, il database Response Group è vuoto), anche se non si utilizza lo stesso FQDN. Non è necessario utilizzare il parametro –OverwriteOwner se non si ricostruisce il pool, ma è possibile utilizzarlo ogniqualvolta si reimportano i Response Group nel pool principale.



È possibile definire un unico set di impostazioni di configurazione di Response Group a livello di applicazione per pool. Le impostazioni includono la configurazione di musica di attesa predefinita, il file audio di musica di attesa predefinita, il periodo di tolleranza di richiamata agente e la configurazione del contesto di chiamata. Per visualizzare queste impostazioni di configurazione, eseguire il cmdlet **Get-CsRgsConfiguration**. Per informazioni dettagliate sul cmdlet **Get-CsRgsConfiguration**, vedere [Get-CsRgsConfiguration](https://docs.microsoft.com/powershell/module/skype/Get-CsRgsConfiguration).

È possibile trasferire queste impostazioni a livello di applicazione da un pool a un altro utilizzando il cmdlet **Import-CsRgsConfiguration** con parametro –ReplaceExistingSettings. L'operazione tuttavia sostituisce le impostazioni nel pool di destinazione.

> [!IMPORTANT]  
> Il vincolo sul trasferimento di impostazioni a un altro pool è valido solo per le impostazioni a livello di applicazione e per il file audio della musica di attesa predefinita. Non si applica a gruppi di agenti, code, flussi di lavoro, orario di ufficio e set di festività.

Se non si desidera sostituire le impostazioni a livello di applicazione nel pool di backup in caso di emergenza e il pool principale non può essere ripristinato, le impostazioni a livello di applicazione nel pool principale saranno perse. Se durante il ripristino è necessario creare un nuovo pool in sostituzione del pool principale con lo stesso FQDN o un FQDN diverso, non è possibile ripristinare le impostazioni a livello di applicazione originali. In questo caso, è necessario configurare il nuovo pool con queste impostazioni e includere il file audio di musica di attesa.

Se in caso di emergenza si decide di trasferire le impostazioni a livello di applicazione dal pool principale a quello di backup utilizzando il cmdlet **Import-CsRgsConfiguration**, è possibile trasferire le impostazioni dal pool di backup al nuovo pool durante il ripristino nello stesso modo in cui le si è trasferite dal pool principale a quello di backup.

Nella tabella seguente viene fornita una panoramica dei passaggi del processo di ripristino dei Response Group.

Per informazioni dettagliate sull'esecuzione di questi passaggi, vedere [Procedure per il ripristino di emergenza dei Response Group in Lync Server 2013](lync-server-2013-response-group-disaster-recovery-procedures.md).

### Procedura di ripristino di emergenza dei Response Group

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Gruppi e ruoli obbligatori</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prima dell'interruzione</p></td>
<td><p>In base alla routine, eseguire il cmdlet <strong>Export-CsRgsConfiguration</strong> per creare backup di tutte le configurazioni di Response Group contenute nei pool Front End in cui l' applicazione Response Group è distribuita.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="even">
<td><p>Durante l'interruzione</p></td>
<td><p>Eseguire il cmdlet <strong>Import-CsRgsConfiguration</strong> per importare la configurazione del Lync Server, Response Group Service di cui è stato eseguito il backup dal pool principale al pool di backup.</p>


> [!NOTE]
> Utilizzare il parametro –ReplaceExistingSettings se si desidera sostituire le impostazioni di Response Group a livello di applicazione presenti nel pool di backup con quelle del pool principale. Se le impostazioni a livello di applicazione del pool principale non vengono trasferite al pool di backup e il pool principale non può essere ripristinato, le impostazioni del pool principale andranno perse.

</td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="odd">
<td><p>Dopo l'importazione</p></td>
<td><p>Eseguire i cmdlet Response Group con il parametro –ShowAll, se si desidera visualizzare tutti i Response Group, o con il parametro –Owner, se si desidera visualizzare solo i Response Group importati, per verificare che tutte le configurazioni dei Response Group siano state importate nel pool di backup.</p>


> [!IMPORTANT]  
> Senza il parametro –ShowAll o –Owner, i Response Group importati nel pool di backup non saranno elencati nei risultati restituiti dai cmdlet.


<p>Eseguire i seguenti cmdlet:</p><ul><li><p><strong>Get-CsRgsWorkflow</strong></p></li><li><p><strong>Get-CsRgsQueue</strong></p></li><li><p><strong>Get-CsRgsAgentGroup</strong></p></li><li><p><strong>Get-CsRgsHoursOfBusiness</strong></p></li><li><p><strong>Get-CsRgsHolidaySet</strong></p></li></ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="even">
<td><p>Dopo il failover</p></td>
<td><ul><li><p>Effettuare una chiamata di prova a un Response Group importato nel pool di backup e verificare che sia gestita correttamente.</p></li><li><p>Tutti gli agenti formali devono effettuare di nuovo l'accesso ai propri gruppi formali nel pool di backup.</p></li><li><p>Gestire le modifiche di configurazione:</p>
<p>I Response Group contenuti nel pool di backup possono essere modificati come al solito durante l'interruzione, a prescindere se siano importati o di proprietà nel pool di backup.</p>


> [!IMPORTANT]  
> Utilizzare Lync Server Management Shell per gestire i Response Group importati nel pool di backup. Non è possibile utilizzare Pannello di controllo di Lync Server per gestire questi Response Group mentre si trovano nel pool di backup.

</li></ul></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Dopo il ripristino e prima del failback</p></td>
<td><p>Eseguire il cmdlet <strong>Export-CsRgsConfiguration</strong> specificando il parametro -Source come pool di backup e il parametro –Owner come pool principale per esportare i Response Group di proprietà del pool principale dal pool di backup.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="even">
<td><p>Dopo il failback</p></td>
<td><ul><li><p>Eseguire il cmdlet <strong>Import-CsRgsConfiguration</strong> per importare di nuovo i Response Group nel pool principale.</p>


> [!NOTE]
> Se il pool principale non è ripristinabile e in sostituzione viene distribuito un nuovo pool, utilizzare il parametro –ReplaceExistingSettings per trasferire le impostazione a livello di applicazione dal pool di backup al nuovo pool. In caso contrario, il nuovo pool utilizzerà le impostazioni predefinite.


</li><li><p>Eseguire i cmdlet riportati di seguito con il parametro –ShowAll, se si desidera visualizzare tutti i Response Group, o il parametro –Owner, se si desidera visualizzare solo i Response Group importati, per verificare che tutte le configurazioni dei Response Group siano state reimportate correttamente nel pool principale:</p><ul><li><p><strong>Get-CsRgsWorkflow</strong></p></li><li><p><strong>Get-CsRgsQueue</strong></p></li><li><p><strong>Get-CsRgsAgentGroup</strong></p></li><li><p><strong>Get-CsRgsHoursOfBusiness</strong></p></li><li><p><strong>Get-CsRgsHolidaySet</strong></p></li></ul></li><li><p>Effettuare una chiamata di prova a un Response Group reimportato nel pool principale e verificare che sia gestita correttamente.</p></li><li><p>Facoltativamente, eseguire il cmdlet <strong>Export-CsRgsConfiguration</strong> nel pool di backup con il parametro –RemoveExportedConfiguration per rimuovere i Response Group di proprietà del pool principale dal pool di backup.</p></li></ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
</tbody>
</table>

