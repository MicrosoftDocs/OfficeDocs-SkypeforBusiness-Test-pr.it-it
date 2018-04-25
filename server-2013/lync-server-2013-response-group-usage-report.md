---
title: 'Lync Server 2013: Rapporto di utilizzo di Response Group'
TOCTitle: Rapporto di utilizzo di Response Group
ms:assetid: 3248b320-a552-400a-8485-6891af4eb0f3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558632(v=OCS.15)
ms:contentKeyID: 49300110
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto di utilizzo di Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

L'applicazione Response Group consente a Microsoft Lync Server 2013 di rispondere e instradare le chiamate telefoniche in base al numero composto e, facoltativamente, alle risposte del chiamante a una serie di domande. Le chiamate di Response Group in genere non vengono instradate a una singola persona, bensì a un team di persone noto come gruppo di agenti. Ad esempio, se qualcuno chiama il numero di telefono dell'helpdesk, Lync Server 2013 può instradare automaticamente la chiamata al primo agente disponibile dell'helpdesk. In alternativa, Lync Server può porre una serie di domande ("Premere 1 in caso di problemi hardware. Premere 2 in caso di problemi software. Premere 3 in caso di problemi di rete") e quindi instradare la chiamata all'agente più appropriato dell'helpdesk in base alla risposta fornita a tali domande.

Il Rapporto di utilizzo dei Response Group fornisce una specifica dettagliata del numero di chiamate telefoniche ricevute da tutti i flussi di lavoro di Response Group e quindi suddivide tali chiamate in categorie più limitate, ad esempio Chiamate offerte, Chiamate con risposta e Chiamate interrotte.

Per lavorare con il Rapporto di utilizzo di Response Group è fondamentale comprendere la differenza tra i tipi di chiamate segnalate:

  - **Chiamate ricevute**. Numero totale di chiamate ricevute da tutte le istanze dell'applicazione Response Group.

  - **Chiamate riuscite**. Numero totale di chiamate che hanno ricevuto risposta dall'applicazione Response Group.

  - **Chiamate offerte** . Numero totale di chiamate trasferite a un agente di Response Group.

  - **Chiamate con risposta** . Numero totale di chiamate a cui effettivamente è stata fornita una risposta da un agente di Response Group.

  - **Percentuale di chiamate interrotte** . Percentuale delle chiamate ricevute dall'applicazione Response Group ma che non hanno ricevuto risposta da un agente. Questo valore viene calcolato sottraendo le Chiamate con risposta dalle Chiamate ricevute e quindi dividendo tale valore per il numero di Chiamate ricevute. Se, ad esempio, sono state ricevute 10 chiamate di cui 7 con risposta, è necessario sottrarre 7 a 10. Il risultato sarà 3 chiamate senza risposta. Tale valore deve essere quindi diviso per 10, in modo da ottenere una percentuale di chiamate interrotte pari al 30%.

  - **Chiamate trasferite** . Numero totale di chiamate di Response Group trasferite a causa del timeout o dell'overflow di una coda.

Se osservando il Rapporto di utilizzo di Response Group non si ricorda la definizione di uno di questi tipi di chiamate, è sufficiente posizionare il mouse sull'etichetta del tipo di chiamata appropriata per visualizzare una descrizione comandi con una breve descrizione.

Il Rapporto di utilizzo di Response Group consente di applicare un filtro a un URI di un flusso di lavoro (l'indirizzo SIP associato a tale flusso di lavoro). Gli URI dei flussi di lavoro, tuttavia, non vengono visualizzati nel rapporto. Se si desidera sapere, ad esempio, quali flussi di lavoro stanno rispondendo al maggior numero di chiamate o quali flussi di lavoro stanno registrando il maggior numero di chiamate trasferite, fare clic sulla metrica appropriata per aprire il rapporto Elenco chiamate di Response Group relativo al tale periodo di tempo. Nel rapporto saranno elencati gli URI dei flussi di lavoro.

## Accesso al Rapporto di utilizzo di Response Group

L'accesso al Rapporto di utilizzo di Response Group può essere effettuato dalla home page di Relazioni monitoraggio. È possibile eseguire il drill-down del [Rapporto Elenco chiamate Response Group in Lync Server 2013](lync-server-2013-response-group-call-list-report.md) facendo clic su una di queste metriche:

  - Chiamate ricevute

  - Chiamate riuscite

  - Chiamate offerte

  - Chiamate con risposta

  - Chiamate trasferite

## Uso ottimale del Rapporto di utilizzo di Response Group

Uno degli usi più interessanti del Rapporto di utilizzo di Response Group potrebbe non essere immediatamente evidente, ovvero la capacità di recuperare informazioni sull'utilizzo per un singolo flusso di lavoro di Response Group.


> [!WARNING]
> Un flusso di lavoro di Response Group è essenzialmente un set di istruzioni che determina le azioni eseguite da Lync Server quando un utente compone un determinato numero di telefono. A tale scopo, ogni flusso di lavoro è associato in modo univoco a un numero di telefono. Quando un utente chiama tale numero, il flusso di lavoro determina la modalità di gestione della chiamata. Ad esempio, il flusso di lavoro potrebbe causare l'instradamento della chiamata a una serie di domande IVR (Interactive Voice Response) che richiedono al chiamante di immettere informazioni aggiuntive ("Premere 1 per il supporto hardware. Premere 2 per il supporto software."). In alternativa, il flusso di lavoro potrebbe causare l'inserimento della chiamata in una coda e mettere in attesa il chiamante finché un agente non sarà disponibile per rispondere alla chiamata. La disponibilità degli agenti per la risposta alle chiamate dipende anche dal flusso di lavoro: i flussi di lavoro vengono usati per configurare sia l'orario di ufficio (i giorni della settimana e le ore del giorno in cui gli agenti sono disponibili per rispondere alle chiamate) che le festività (i giorni in cui non vi sono agenti disponibili per rispondere alle chiamate). Ogni volta che si compone un numero di telefono appartenente all'applicazione Response Group, si chiama essenzialmente un flusso di lavoro di Response Group.



Sebbene gli URI dei flussi di lavoro non vengano visualizzati nel Rapporto di utilizzo di Response Group, è comunque possibile visualizzare le statistiche di utilizzo per un singolo flusso di lavoro, operazione che è spesso molto utile. Si supponga, ad esempio, di aver lanciato di recente una nuova campagna pubblicitaria e di essere curioso di sapere se gli utenti stanno chiamando per chiedere informazioni sul prodotto in questione. Se un flusso di lavoro di Response Group è stato associato al numero di telefono indicato per la campagna pubblicitaria, è possibile verificare facilmente se e quante persone stanno componendo tale numero.

È possibile adottare un approccio simile anche per misurare il numero di chiamate gestite dall'helpdesk interno o dal Servizio clienti.

Per esaminare le statistiche di utilizzo di un determinato flusso di lavoro, immettere l'URI del flusso di lavoro nella casella URI flusso di lavoro. Naturalmente, come già osservato, gli URI dei flussi di lavoro (indirizzo SIP associato a un flusso di lavoro) non vengono visualizzati nel rapporto e pertanto è necessario individuare un altro metodo per determinare l'URI di un flusso di lavoro. Un'alternativa valida può essere quella di usare Windows PowerShell e Lync Server Management Shell. Il comando che segue, ad esempio, restituisce gli URI per tutti i flussi di lavoro di Response Group:

    Get-CsRgsWorkflow | Select-Object Name, PrimaryUri

Verranno restituiti dati simili ai seguenti:

    Name                            PrimaryUri
    ----                            ----------
    Customer Support                sip:support@litwareinc.com
    Help Desk                       sip:helpdesk@litwareinc.com
    New Ad Campaign                 sip:newads@litwareinc.com

Questo comando restituisce informazioni relative a un singolo flusso di lavoro, ovvero "New Ad Campaign":

    Get-CsRgsWorkflow -Name "New Ad Campaign" | Select-Object Name, PrimaryUri

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Il Rapporto di utilizzo di Response Group ad esempio consente di visualizzare i dati di tutti i flussi di lavoro di Response Group o di un singolo flusso di lavoro. È inoltre possibile scegliere come raggruppare i dati. In questo caso, gli utilizzi vengono raggruppati per ora, giorno, settimana o mese.

Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto di utilizzo di Response Group.

### Filtri del Rapporto di utilizzo di Response Group

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
<td><p><strong>Intervallo</strong></p></td>
<td><p>Intervallo di tempo. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
<li><p>Mensile (è possibile visualizzare un massimo di 12 mesi)</p></li>
</ul>
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo giornaliero con la data di inizio 7/7/2012 e la data di fine 2/28/2012, verranno visualizzati i dati relativi ai giorni dal 8/7/2012 alle 12:00 AM al 9/7/2012 alle 12:00 AM, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>URI flusso di lavoro</strong></p></td>
<td><p>Consente di limitare i dati restituiti al flusso di lavoro Response Group specificato. Per utilizzare questo filtro, immettere l'indirizzo SIP del flusso di lavoro. Ad esempio:</p>
<p>sip:helpdesk@litwareinc.com</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente vengono elencate le informazioni fornite nel Rapporto di utilizzo di Response Group.

### Metrica del Rapporto di utilizzo di Response Group

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
<td><p><strong>Orario</strong></p>
<p><strong>Giornaliero</strong></p>
<p><strong>Settimanale</strong></p>
<p><strong>Mensile</strong></p></td>
<td><p>No</p></td>
<td><p>Indica l'intervallo di tempo selezionato. Ove applicabile, è possibile fare clic su un determinato intervallo di tempo per visualizzare informazioni dettagliate relative a tale intervallo. Se ad esempio si sta utilizzando l'intervallo giornaliero e si fa clic su 7/7/2012, verranno visualizzate le attività di registrazione degli utenti per tale data, suddivise per ore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiamate ricevute</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate ricevute da tutte le istanze dell'applicazione Response Group. Quando si fa clic su questo elemento, viene visualizzato il Rapporto Elenco chiamate Response Group relativo all'intervallo di tempo selezionato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Chiamate riuscite</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate che hanno ricevuto riposta dall'applicazione Response Group. Quando si fa clic su questo elemento, viene visualizzato il Rapporto Elenco chiamate Response Group relativo all'intervallo di tempo selezionato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiamate offerte</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate trasferite a un agente di Response Group. Quando si fa clic su questo elemento, viene visualizzato il Rapporto Elenco chiamate Response Group relativo all'intervallo di tempo selezionato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Chiamate con risposta</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate a cui effettivamente è stata fornita una risposta da un agente di Response Group. Quando si fa clic su questo elemento, viene visualizzato il Rapporto Elenco chiamate Response Group relativo all'intervallo di tempo selezionato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Percentuale di chiamate interrotte</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate ricevute dall'applicazione Response Group ma alle quali non è stata mai fornita risposta da un agente. Questo valore viene calcolato sottraendo il valore di Chiamate con risposta dal valore di Chiamate ricevute e quindi dividendo tale valore per il numero di chiamate ricevute. Se ad esempio sono state ricevute 10 chiamate, di cui sette con risposta, sarà necessario sottrarre sette da 10, lasciando tre chiamate senza risposta. Tale valore verrà poi diviso per 10 e si otterrà una percentuale di chiamate interrotte pari al 30%.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Media minuti chiamata per agente</strong></p></td>
<td><p>No</p></td>
<td><p>Quantità media di tempo dedicata da una gente di Response Group per chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiamate trasferite</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate di Response Group trasferite a causa del timeout o dell'overflow di una coda. Quando si fa clic su questo elemento, viene visualizzato il Rapporto Elenco chiamate Response Group relativo all'intervallo di tempo selezionato.</p></td>
</tr>
</tbody>
</table>

