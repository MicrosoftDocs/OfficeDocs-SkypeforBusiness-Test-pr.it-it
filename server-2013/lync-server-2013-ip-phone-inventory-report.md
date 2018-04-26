---
title: 'Lync Server 2013: Rapporto inventario telefoni IP'
TOCTitle: Rapporto inventario telefoni IP
ms:assetid: aa7d6b31-cb09-4e68-b020-aa5dd0081c20
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615027(v=OCS.15)
ms:contentKeyID: 49301623
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto inventario telefoni IP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel Rapporto inventario telefoni IP vengono fornite informazioni sui telefoni IP attualmente in uso nell'organizzazione. In tale rapporto è incluso un elenco dettagliato dei telefoni IP effettivamente utilizzati durante il periodo specificato. Tra l'altro, il rapporto consente agli amministratori di sapere se sono ancora in uso telefoni obsoleti da sostituire e di essere avvisati se nell'organizzazione sono presenti telefoni costosi che vengono utilizzati raramente. Questo tipo di informazioni può rivelarsi prezioso quando si decide di acquistare nuovi telefoni o di ridistribuire quelli esistenti. Ad esempio, a un utente che utilizza di rado un telefono costoso può venire richiesto di scambiarlo con un utente che utilizza il proprio telefono con maggiore frequenza.

Tenere presente che questo rapporto presenta diverse limitazioni se viene utilizzato come un vero e proprio inventario. Innanzitutto elenca esclusivamente tutti i telefoni IP che hanno avuto accesso a Lync Server durante il periodo di tempo specificato, ordinati in base all'ora dell'ultimo accesso. Se pertanto un telefono non esegue l'accesso durante il periodo di tempo in questione, non viene incluso nel rapporto, così come i telefoni che hanno eseguito l'accesso prima dell'inizio di tale periodo e che restano connessi per l'intervallo di tempo specificato. Si supponga ad esempio di voler esaminare l'inventario dei telefoni per luglio 2012 e di avere diversi telefoni che hanno eseguito l'accesso a Lync Server il 30 giugno 2012 e che erano ancora connessi il 1° luglio. Tali telefoni non verranno visualizzati nel rapporto inventario per il 1° luglio.

È inoltre importante notare che il rapporto inventario può includere telefoni che non vengono più utilizzati nell'organizzazione. Si supponga ad esempio che alcuni telefoni Fabrikam abbiano eseguito l'accesso al sistema il 1° luglio 2012 e che cinque giorni dopo l'organizzazione si sia disfatta di tutti questi telefoni sostituendoli con un modello Contoso più recente. I telefoni Fabrikam verranno comunque visualizzati nel rapporto "inventario" semplicemente perché si sono connessi al sistema durante il mese di luglio.

Nel Rapporto inventario telefoni IP inoltre non vengono riportati i totali riepilogativi per i diversi tipi di telefoni. Si supponga ad esempio di disporre di 105 telefoni Polycom CX600. Nel rapporto non verrà indicato che vi sono 105 telefoni di questo tipo e verranno solo visualizzate 105 voci distinte per Polycom Cx600. L'unico modo per sapere che sono presenti 105 voci per Polycom Cx600 è quello di contare manualmente queste singole voci.


> [!WARNING]
> In alternativa, esportare i dati e utilizzare Microsoft Excel o Windows PowerShell per eseguire automaticamente il conteggio.



## Accesso al Rapporto inventario telefoni IP

È possibile accedere al Rapporto inventario telefoni IP dalla home page dei rapporti di monitoraggio. Se si fa clic sulla metrica URI utente (User URI), si accede al Rapporto attività utente per l'utente in questione. Se si fa clic sulla metrica Ultima attività (Last activity) per una chiamata peer-to-peer, si accede al Rapporto Dettagli sessione peer-to-peer. Se si fa clic su questa stessa metrica per una conferenza, si accede al Rapporto Dettagli conferenza.

## Utilizzo ottimale del Rapporto inventario telefoni IP

Se si è interessati esclusivamente alle informazioni sull'utilizzo di un determinato tipo di telefono, ad esempio alla frequenza con cui gli utenti utilizzano un telefono Polycom CX600, è possibile ottenere tali informazioni direttamente dal Rapporto inventario telefoni IP filtrando i dati in base al tipo di telefono in questione. Se invece si desidera ottenere informazioni riepilogative per tutti i telefoni di cui si dispone, ad esempio quanti utenti utilizzano un telefono Polycom CX600, quanti utilizzano un telefono LG-Nortel IP8540 e così via, sarà necessario esportare i dati e utilizzare un'altra applicazione, come Windows PowerShell, per eseguire questo tipo di analisi. Si supponga ad esempio di esportare i dati in un file con valori delimitati da virgole (C:\\Data\\IP\_Phone\_Inventory\_Report.csv). In tal caso, è possibile utilizzare questi due comandi per ottenere dati riepilogativi per tutti i telefoni:

    $phones = Import-Csv "C:\Data\IP_Phone_Inventory_Report.csv"
    $phones |Group-Object Manufacturer, "Hardware version" | Select-Object Count, Name | Sort-Object Count -Descending

Verranno restituiti dati simili ai seguenti:

    Count    Name
    -----    ----
      267    POLYCOM, CX700
      267    POLYCOM, CX600
      166    POLYCOM, C
       68    Microsoft, CPE
       64    LG-Nortel, IP8540
       59    Aastra, 6725ip
       37    LG-Nortel, IP
       22    POLYCOM, CX3000
       11    Microsoft, CPE_A
        9    POLYCOM, CX500
        7    Aastra, 6721ip

Analogamente, questi due comandi indicano quali telefoni si sono connessi al sistema, ma non sono mai stati utilizzati per effettuare una chiamata. Il valore della metrica Ultima attività (Last activity) è vuoto, a significare che non vi è stata alcuna ultima attività:

    $phones = Import-Csv "C:\Data\IP_Phone_Inventory_Report.csv"
    $phones | Where-Object {$_."Last activity" -eq ""}

Per ogni telefono non utilizzato verranno restituiti dati simili ai seguenti:

    Manufacturer     : POLYCOM
    Hardware version : CX600
    MAC address      : 00-04-F2-00-01-76
    User URI         : 422
    User agent       : CPE/4.0.7423.1 OCPhone/4.0.7423.1 (Microsoft Lync 2010 (Beta) Phone Edition)
    Last logon time  : 8/30/2010 4:44:48 PM
    Last logoff time : 8/30/2010 5:59:07 PM
    Last activity    :

Un altro modo interessante per utilizzare il Rapporto inventario telefoni IP è il seguente. Se si dispone dell'indirizzo MAC di un telefono IP, è possibile individuare l'utente che ha utilizzato per ultimo tale telefono semplicemente immettendo l'indirizzo nella casella di testo Indirizzo MAC (MAC address). Il Rapporto inventario telefoni IP restituirà quindi, tra gli altri dati, l'indirizzo SIP dell'utente che si è connesso per ultimo con tale telefono. In alternativa, è possibile immettere l'indirizzo SIP di un utente nella casella URI utente (User URI) per individuare tutti i telefoni utilizzati da tale utente.

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Ad esempio, il Rapporto inventario telefoni IP consente di visualizzare solo i telefoni prodotti da una società specifica o una versione specifica di tali telefoni. È inoltre possibile scegliere la modalità di raggruppamento dei dati. In questo caso le registrazioni sono raggruppabili per ora, giorno, settimana o mese.

Nella tabella seguente sono elencati i filtri applicabili al Rapporto inventario telefoni IP.

### Filtri del Rapporto inventario telefoni IP

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Da</strong></p></td>
<td><p>Data/ora di inizio dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di inizio come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Produttore</strong></p></td>
<td><p>Nome della società che produce il telefono IP. I valori per questo filtro vengono inseriti automaticamente in base ai telefoni IP presenti nel database.</p></td>
</tr>
<tr class="even">
<td><p><strong>Versione hardware</strong></p></td>
<td><p>Numero di versione del telefono IP. I filtri basati su produttore e versione hardware consentono di identificare in modo univoco un tipo di telefono specifico. I valori per questo filtro vengono inseriti automaticamente in base ai telefoni IP presenti nel database.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agente utente</strong></p></td>
<td><p>Identificatore del software utilizzato dal telefono IP. I valori per questo filtro vengono inseriti automaticamente in base ai telefoni IP presenti nel database.</p></td>
</tr>
<tr class="even">
<td><p><strong>Indirizzo MAC</strong></p></td>
<td><p>Identificatore univoco dell'interfaccia di rete del telefono IP. L'indirizzo MAC (Media Access Control), assegnato di solito al momento della produzione, è incorporato nell'hardware del dispositivo.</p>
<p>Per cercare i record relativi a un indirizzo MAC specifico, è sufficiente immettere tale indirizzo, ad esempio:</p>
<p>00-08-5D-16-16-48</p>
<p>È necessario immettere l'indirizzo completo. Un indirizzo parziale , ad esempio 00-08-5D, non restituisce alcun dato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ultima attività prima di (giorni)</strong></p></td>
<td><p>Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>10</p></li>
<li><p>20</p></li>
<li><p>30</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Ora ultima disconnessione prima di (giorni)</strong></p></td>
<td><p>Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>10</p></li>
<li><p>20</p></li>
<li><p>30</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Prefisso URI utente</strong></p></td>
<td><p>Indirizzo SIP dell'utente che ha utilizzato il telefono IP.</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella che segue sono elencate le informazioni fornite nel Rapporto inventario telefoni IP.

### Metriche del Rapporto inventario telefoni IP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento utilizzabile per eseguire l'ordinamento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Produttore</strong></p></td>
<td><p>Sì</p></td>
<td><p>Nome della società che produce il telefono IP.</p></td>
</tr>
<tr class="even">
<td><p><strong>Versione hardware</strong></p></td>
<td><p>Sì</p></td>
<td><p>Numero della versione del telefono IP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Indirizzo MAC</strong></p></td>
<td><p>Sì</p></td>
<td><p>Identificatore univoco dell'interfaccia di rete del telefono IP. L'indirizzo MAC, assegnato di solito al momento della produzione, è incorporato nell'hardware del dispositivo.</p></td>
</tr>
<tr class="even">
<td><p><strong>URI utente</strong></p></td>
<td><p>Sì</p></td>
<td><p>Indirizzo SIP dell'utente che ha utilizzato il telefono IP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agente utente</strong></p></td>
<td><p>Sì</p></td>
<td><p>Identificatore del software utilizzato dal telefono IP.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora ultimo accesso</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora dell'ultimo accesso del telefono IP a Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora ultima disconnessione</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora dell'ultima disconnessione del telefono IP da Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ultima attività</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora dell'ultimo utilizzo del telefono IP.</p></td>
</tr>
</tbody>
</table>

