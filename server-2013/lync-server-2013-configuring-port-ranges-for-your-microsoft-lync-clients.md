---
title: Configurazione degli intervalli di porte per i client Microsoft Lync
TOCTitle: Configurazione degli intervalli di porte per i client Microsoft Lync
ms:assetid: 287d5cea-7ada-461c-9b4a-9da2af315e71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204760(v=OCS.15)
ms:contentKeyID: 49300000
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione degli intervalli di porte per i client Microsoft Lync

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per impostazione predefinita, le applicazioni client Lync possono usare qualsiasi porta compresa nell'intervallo di porte da 1024 a 65535 quando vengono usate in una sessione di comunicazione. Questo accade perché non vengono abilitati automaticamente intervalli di porte specifici per i client. Per poter usare Qualità del servizio (QoS), tuttavia, è necessario riassegnare i diversi tipi di traffico (audio, video, multimediale, condivisione applicazioni e trasferimento file) a una serie di intervalli di porte univoci. A tale scopo è possibile usare il cmdlet Set-CsConferencingConfiguration.

Per determinare quali intervalli di porte sono attualmente in uso per le sessioni di comunicazione è possibile eseguire questo comando da Microsoft Lync Server 2013 Management Shell:

    Get-CsConferencingConfiguration

Supponendo che non siano state apportate modifiche alle impostazioni delle conferenze in seguito all'installazione di Lync Server 2013, dovrebbero essere restituite informazioni che includono questi valori di proprietà:

    ClientMediaPortRangeEnabled : False
    ClientAudioPort             : 5350
    ClientAudioPortRange        : 40
    ClientVideoPort             : 5350
    ClientVideoPortRange        : 40
    ClientAppSharingPort        : 5350
    ClientAppSharingPortRange   : 40
    ClientFileTransferPort      : 5350
    ClientTransferPortRange     : 40

Se si osserva attentamente l'output precedente, si noteranno due aspetti importanti. Innanzitutto, la proprietà ClientMediaPortRangeEnabled è impostata su False:

    ClientMediaPortRangeEnabled : False

Si tratta di un'impostazione determinante. Infatti, quando questa proprietà è impostata su False, i client di Lync usano una qualsiasi porta disponibile compresa nell'intervallo da 1024 a 65535 quando vengono coinvolti in una sessione di comunicazione, indipendentemente dalle altre impostazioni relative alle porte, ad esempio ClientMediaPort o ClientVideoPort. Se si desidera limitare l'uso a un set di porte specificato (operazione utile se si intende implementare Qualità del servizio), è prima necessario abilitare gli intervalli di porte multimediali dei client. A tale scopo è possibile usare questo comando di Windows PowerShell:

    Set-CsConferencingConfiguration -ClientMediaPortRangeEnabled $True

Il comando precedente abilita gli intervalli di porte multimediali dei client per la raccolta globale delle impostazioni di configurazione delle conferenze. Tali impostazioni, tuttavia, possono essere applicate anche all'ambito del sito e/o all'ambito del servizio (solo per il servizio Conferencing Server). Per abilitare gli intervalli di porte multimediali dei client per un determinato sito o server, specificare l'identità del sito o del server quando si chiama Set-CsConferencingConfiguration:

    Set-CsConferencingConfiguration -Identity "site:Redmond" -ClientMediaPortRangeEnabled $True

In alternativa, è possibile usare questo comando per abilitare contemporaneamente gli intervalli di porte per tutte le impostazioni di configurazione delle conferenze:

    Get-CsConferencingConfiguration | Set-CsConferencingConfiguration  -ClientMediaPortRangeEnabled $True

Il secondo aspetto importante da osservare è l'output di esempio. Questo mostra che, per impostazione predefinita, gli intervalli di porte multimediali impostati per ogni tipo di traffico di rete sono identici:

    ClientAudioPort             : 5350
    ClientVideoPort             : 5350
    ClientAppSharingPort        : 5350
    ClientFileTransferPort      : 5350

Per implementare QoS, è necessario che ciascuno di questi intervalli di porte sia univoco. È ad esempio possibile configurare gli intervalli di porte in questo modo:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di traffico client</th>
<th>Inizio intervallo porte</th>
<th>Intervallo porte</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Audio</p></td>
<td><p>50020</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>Video</p></td>
<td><p>58000</p></td>
<td><p>20</p></td>
</tr>
<tr class="odd">
<td><p>Condivisione applicazioni</p></td>
<td><p>42000</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>Trasferimento file</p></td>
<td><p>42020</p></td>
<td><p>20</p></td>
</tr>
</tbody>
</table>


Nella tabella precedente gli intervalli di porte dei client rappresentano un subset degli intervalli di porte configurati per i server. Sui server, ad esempio, la condivisione applicazioni è configurata in modo da usare le porte da 40803 a 49151, mentre sui computer client la condivisione applicazioni è configurata in modo da usare le porte da 42000 a 42019. Questo consente, ancora una volta, di semplificare l'amministrazione di Qualità del servizio, in quanto non è necessario che le porte dei client rappresentino un subset delle porte usate sul server. Sui computer client è ad esempio possibile configurare la condivisione applicazioni in modo da usare le porte da 10000 a 10019. È tuttavia consigliabile impostare gli intervalli di porte dei client come subset degli intervalli di porte dei server.

Si sarà inoltre notato che sono state riservate 8348 porte per la condivisione applicazioni sui server e che solo 20 porte sono state messe da parte per la condivisione applicazioni sui client. Anche questa regola è consigliata, sebbene non sia categorica. In genere, è possibile considerare che ogni porta disponibile rappresenti una singola sessione di comunicazione: la disponibilità di 100 porte in un intervallo di porte, indica che il computer in questione può partecipare a non più di 100 sessioni di comunicazione in un dato momento. Poiché è probabile che i server verranno coinvolti in un numero di conversazioni di gran lunga superiore a quelle dei client, è ragionevole aprire molte più porte sui server che non sui client. La scelta di riservare 20 porte per la condivisione applicazioni su un client significa che un utente può partecipare contemporaneamente a 20 sessioni di condivisione applicazioni sul dispositivo specificato. Questa configurazione dovrebbe soddisfare la maggior parte degli utenti.

Per assegnare gli intervalli di porte precedenti alla raccolta globale delle impostazioni di configurazione delle conferenze, è possibile usare questo comando di Lync Server Management Shell:

    Set-CsConferencingConfiguration -Identity global -ClientAudioPort 50020 -ClientAudioPortRange 20 -ClientVideoPort 58000 -ClientVideoPortRange 20 -ClientAppSharingPort 42000 -ClientAppSharingPortRange 20 - ClientFileTransferPort 42020 -ClientFileTransferPortRange 20

In alternativa, usare il comando per assegnare questi stessi intervalli di porte per tutte le impostazioni di configurazione delle conferenze:

    Get-CsConferencingConfiguration | Set-CsConferencingConfiguration -ClientAudioPort 50020 -ClientAudioPortRange 20 -ClientVideoPort 58000 -ClientVideoPortRange 20 -ClientAppSharingPort 42000 -ClientAppSharingPortRange 20 - ClientFileTransferPort 42020 -ClientFileTransferPortRange 20

Per rendere effettive le modifiche apportate, è necessario che i singoli utenti si disconnettano da Lync e quindi si riconnettano.


> [!NOTE]
> È anche possibile abilitare gli intervalli di porte multimediali dei client e quindi assegnarli con un singolo comando. Ad esempio:<BR><CODE>Set-CsConferencingConfiguration -ClientMediaPortRangeEnabled $True -ClientAudioPort 50020 -ClientAudioPortRange 20 -ClientVideoPort 58000 -ClientVideoPortRange 20 -ClientAppSharingPort 42000 -ClientAppSharingPortRange 20 -ClientFileTransferPort 42020 -ClientFileTransferPortRange 20</CODE>


