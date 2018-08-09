---
title: "Lync Server 2013: Config. impostaz. di Registraz. dettagli chiam. e Qualità dell'esperienza"
TOCTitle: "Lync Server 2013: Config. impostaz. di Registraz. dettagli chiam. e Qualità dell'esperienza"
ms:assetid: 009a0499-4f8c-450d-9c72-a565a08e9f7a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204621(v=OCS.15)
ms:contentKeyID: 49299482
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle impostazioni di Registrazione dettagli chiamata e Qualità percepita dagli utenti

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Dopo l'associazione di un archivio di monitoraggio a un pool Front End, la configurazione dell'archivio di monitoraggio, quindi l'installazione e la configurazione di SQL Server Reporting Services e dei rapporti di monitoraggio, sarà possibile gestire il monitoraggio registrazioni dettagli chiamata (CDR, Call Detail Recording) e QoE (Quality of Experience) utilizzando Lync Server Management Shell. I cmdlet Lync Server Management Shell consentono di abilitare e disabilitare il monitoraggio CDR e/o QoE per un sito specifico o per l'intera distribuzione di Lync Server. Per ottenere questo risultato, è sufficiente un comando semplice come il seguente:

    Set-CsQoEConfiguration -Identity "global" -EnableQoE $False

Quando si installa Microsoft Lync Server 2013, viene installata anche una raccolta predefinita di impostazioni di configurazione globali per CDR e QoE. I valori predefiniti di alcune delle impostazioni usate più di frequente da CDR sono mostrati nella tabella seguente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Descrizione</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EnableCDR</p></td>
<td><p>Indica se la registrazione dettagli chiamata è abilitata o meno. Se è impostata su True, tutti i record CDR verranno raccolti e scritti nel database di monitoraggio.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>EnablePurging</p></td>
<td><p>Indica se i record CDR verranno eliminati periodicamente dal database. Se è impostata su True, i record verranno eliminati dopo il periodo di tempo specificato dalle proprietà KeepCallDetailForDays (per record CDR) e KeepErrorReportForDays (per errori CDR). Se False, i record verranno mantenuti indefinitamente.</p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p>KeepCallDetailForDays</p></td>
<td><p>Indica il numero di giorni per cui i record CDR verranno mantenuti nel database. Qualsiasi record che ha superato il numero di giorni specificato verrà eliminato automaticamente, ma solo se l'eliminazione è stata abilitata.</p>
<p>KeepCallDetailForDays può essere impostato su qualsiasi valore intero compreso tra 1 e 2562 giorni (circa 7 anni).</p></td>
<td><p>60 giorni</p></td>
</tr>
<tr class="even">
<td><p>KeepErrorReportForDays</p></td>
<td><p>Indica per quanti giorni i report sugli errori di registrazione dettagli chiamata verranno conservati. Gli eventuali report antecedenti al numero di giorni specificato verranno eliminati automaticamente. I report con gli errori di registrazione dettagli chiamata sono report diagnostici caricati da applicazioni client come Microsoft Lync 2013.</p>
<p>È possibile impostare questa proprietà su qualsiasi valore intero compreso tra 1 e 2562 giorni.</p></td>
<td><p>60 giorni</p></td>
</tr>
</tbody>
</table>


Analogamente, i valori predefiniti per le impostazioni QoE selezionate vengono mostrati nella tabella seguente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Descrizione</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EnableQoE</p></td>
<td><p>Indica se il monitoraggio QoE è abilitato. Se impostata su True, tutti i record QoE verranno raccolti e scritti nel database di monitoraggio.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>EnablePurging</p></td>
<td><p>Indica se i record QoE verranno eliminati periodicamente dal database. Se è impostata su True, i record verranno eliminati dopo il periodo di tempo specificato dalle proprietà KeepQoEDataForDays. Se False, i record QoE verranno mantenuti indefinitamente.</p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p>KeepQoEDataForDays</p></td>
<td><p>Indica il numero di giorni per cui i record QoE verranno mantenuti nel database. Qualsiasi record che ha superato il numero di giorni specificato verrà eliminato automaticamente, ma solo se l'eliminazione è stata abilitata.</p>
<p>KeepCallDetailForDays può essere impostato su qualsiasi valore intero compreso tra 1 e 2562 giorni.</p></td>
<td><p>60 giorni</p></td>
</tr>
</tbody>
</table>


Per modificare queste impostazioni globali, utilizzare i cmdlet Set-CsCdrConfiguration e Set-CsQoEConfiguration. Ad esempio, questo comando, eseguito entro Lync Server Management Shell, consente di disabilitare il monitoraggio CDR a livello di ambito globale. Per ottenere questo risultato, la proprietà EnableCDR viene impostata su False ($False):

    Set-CsCdrConfiguration -Identity "global" -EnableCDR $False

Si noti che la disabilitazione del monitoraggio non annulla l'associazione dell'archivio di monitoraggio dal pool Front End e non disinstallerà o influirà in alcun modo sul database di monitoraggio back-end. Quando si utilizza Lync Server Management Shell per disabilitare il monitoraggio CDR o QoE, si interrompe in effetti la raccolta e l'archiviazione di dati di monitoraggio da parte di Lync Server. Se, in questo caso, si desidera riprendere la raccolta e l'archiviazione di dati CDR, è sufficiente impostare di nuovo la proprietà EnableCDR su True ($True):

    Set-CsCdrConfiguration -Identity "global" -EnableCDR $True

Analogamente, questo comando disabilita l'eliminazione dei record QoE a livello di ambito globale:

    Set-CsQoEConfiguration -Identity "global" -EnablePurging $False

Oltre alle impostazioni globali, le impostazioni di configurazione di CDR e QoE possono essere assegnate all'ambito del sito. Ciò offre una maggiore flessibilità a livello di gestione per il monitoraggio. Ad esempio, un amministratore può abilitare il monitoraggio CDR per il sito di Redmond ma disabilitarlo per il sito di Dublino. Per creare nuove impostazioni di configurazione CDR a livello di ambito di sito, utilizzare un comando simile a questo:

    New-CsCdrConfiguration -Identity "site:Redmond" -EnableCDR $False

È necessario ricordare che le impostazioni configurate a livello di ambito di sito hanno priorità maggiore rispetto alle impostazioni configurate a livello di ambito globale. Ad esempio, si supponga che il monitoraggio CDR sia abilitato a livello di ambito globale, ma disabilitato a livello di ambito di sito (per il sito di Redmond). Le informazioni sulle registrazioni dettagli chiamata non verranno quindi archiviate per gli utenti del sito di Redmond, ma verranno archiviate per gli utenti di altri siti, ovvero utenti gestiti dalle impostazioni globali invece che dalle impostazioni de sito di Redmond.

Nuove impostazioni di configurazione QoE possono essere create a livello di ambito di sito utilizzando un comando simile a questo:

    New-CsQoEConfiguration -Identity "site:Redmond" -KeepQoEDataForDays 15

Per ulteriori informazioni, digitare i comandi seguenti da Lync Server Management Shell:

    Get-Help New-CsCdrConfiguration | more
    Get-Help Set-CsCdrConfiguration | more
    Get-Help New-CsQoEConfiguration | more
    Get-Help Set-CsQoEConfiguration | more

