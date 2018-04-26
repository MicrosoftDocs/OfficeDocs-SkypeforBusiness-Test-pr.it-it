---
title: 'Lync Server 2013: Rapporto registrazione utenti'
TOCTitle: Rapporto registrazione utenti
ms:assetid: 151d5cc9-cc1b-4cfa-be9c-55ebe321f7a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558614(v=OCS.15)
ms:contentKeyID: 49299777
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto registrazione utenti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il rapporto registrazione utenti fornisce una panoramica delle attività di accesso utente, in particolare informazioni sul numero di utenti che hanno eseguito l'accesso a Microsoft Lync Server 2013 nel corso di un determinato periodo (orario, giornaliero, settimanale o mensile). Il rapporto segnala solo il numero di persone che ha eseguito l'accesso, senza specificarne la *tipologia* . Relazioni monitoraggio non fornisce informazioni sulla tipologia di utenti che utilizzano Lync Server 2013. È tuttavia possibile ottenere una stima approssimativa di informazioni utente mediante il rapporto attività utente.

Nel fornire informazioni sull'accesso degli utenti, il rapporto registrazione utenti opera due importanti distinzioni. Innanzitutto, suddivide gli accessi in due categorie principali: accessi interni e accessi esterni. Gli accessi interni si riferiscono agli utenti che effettuano l'accesso dall'interno del firewall dell'organizzazione, ovvero mentre sono connessi alla rete aziendale. Gli accessi esterni indicano gli utenti che effettuano l'accesso dall'esterno del firewall tramite un server perimetrale. Un utente che esegue l'accesso da un Internet café ad esempio viene conteggiato come accesso esterno. Se è necessario conoscere il numero di utenti che effettuano l'accesso dall'esterno del firewall, il rapporto registrazione utenti è in grado di fornire questa informazione.

Inoltre, il rapporto registrazione utenti annota il numero di utenti *attivi* presenti nel corso di un determinato periodo. Un utente attivo è una persona che ha partecipato a una sessione di messaggistica istantanea o a una riunione Lync, effettuato o ricevuto una chiamata o altrimenti utilizzato Lync Server durante il periodo di tempo specificato. Differisce da un utente che ha effettuato l'accesso, ma non si è mai avvalso effettivamente del sistema.

## Accesso al rapporto registrazione utenti

Il rapporto registrazione utenti è accessibile solo dalla home page Relazioni monitoraggio e non è collegato ad altri rapporti.

## Utilizzo ottimale del rapporto registrazione utenti

Terminata la distribuzione di Lync Server spesso si desidera sapere se gli utenti utilizzano effettivamente questa nuova tecnologia. Sebbene presenti qualche limitazione, il rapporto registrazione utenti può contribuire a fornire una risposta al riguardo. Per determinare se gli utenti utilizzano Lync Server, è necessario eseguire due operazioni. Innanzitutto, occorre acquisire il valore metrico degli utenti con accesso univoco dal rapporto registrazione utenti. Tale valore indica il numero di singoli individui che ha effettuato l'accesso a Lync Server.

In confronto, la metrica Totale accessi segnala il numero totale di volte in cui un individuo ha effettuato l'accesso a Lync Server. Supponendo ad esempio che Davide Garghentini si è connesso a Lync Server cinque volte nell'arco di una giornata, tali connessioni vengono conteggiate come cinque distinte sessioni di accesso per la metrica Totale accessi, ma come un unico accesso utente per la metrica Utenti con accesso univoco. Analogamente, non è raro che un utente effettui l'accesso da più dispositivi o più posizioni. Ad esempio, un utente può connettersi sia con il computer desktop che con il portatile e disporre di un telefono IP che si connette automaticamente a Lync Server. L'esempio riportato indica un unico utente con tre accessi.

Per spiegare ulteriormente la differenza tra accessi totali e accessi univoci, osservare gli accessi relativi a uno specifico periodo nella tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>Ora accesso</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Davide Garghentini</p></td>
<td><p>7/7/2012 08:45:00</p></td>
</tr>
<tr class="even">
<td><p>Davide Garghentini</p></td>
<td><p>7/7/2012 08:46:00</p></td>
</tr>
<tr class="odd">
<td><p>Daniela Cazzaniga</p></td>
<td><p>7/7/2012 09:17:00</p></td>
</tr>
<tr class="even">
<td><p>Davide Garghentini</p></td>
<td><p>7/7/2012 09:22:00</p></td>
</tr>
<tr class="odd">
<td><p>Daniela Cazzaniga</p></td>
<td><p>7/7/2012 09:31:00</p></td>
</tr>
</tbody>
</table>


Sebbene complessivamente vengano indicati cinque accessi, vi sono in realtà solo due utenti con accesso univoco: Davide Garghentini, che si è connesso tre volte, e Luisa Cazzaniga, che ha effettuato l'accesso due volte. Questa è la differenza tra accessi e utenti con accesso univoco.

Oltre a conoscere il numero di accessi univoci, è necessario conoscere il numero totale di utenti abilitati per Lync Server. È possibile recuperare questo valore aprendo Lync Server 2013 Management Shell ed eseguendo il seguente comando di Windows PowerShell:

    (Get-CsUser).Count

Se il comando precedente restituisce un valore pari a 1.236 e la metrica Utenti con accesso univoco restituisce un valore medio pari a 667, è ipotizzabile che ogni giorno poco più della metà degli utenti con abilitazione per Lync acceda effettivamente al sistema (667 diviso 1.236 è uguale al 54% circa).


> [!WARNING]
> Le metriche di accesso registrano solo gli utenti che hanno effettivamente eseguito l'accesso durante il periodo specificato, senza tenere traccia degli utenti già connessi al sistema. Se, ad esempio, la metrica Utenti con accesso univoco indica 667 accessi su 1.236 utenti, si può ipotizzare che circa la metà degli utenti acceda al sistema. Supponiamo però che 300 utenti fossero già connessi al sistema nel momento in cui si è iniziato a controllare i dati di accesso. Ciò vorrebbe dire che in realtà hanno effettuato l'accesso a Lync Server quasi 1.000 utenti e che pertanto gli utenti effettivamente connessi ammontano all'incirca all'80%.



È inoltre opportuno confrontare i valori delle metriche Utenti con accesso univoco e Utenti attivi univoci. La metrica Utenti attivi univoci indica quanti utenti univoci si sono effettivamente avvalsi di Lync Server: effettuando una chiamata, partecipando a una riunione Lync o prendendo parte a una sessione di messaggistica istantanea. L'informazione è utile in quanto è possibile configurare l'avvio automatico di Microsoft Lync 2013 ogni volta che un utente avvia Windows. Un numero notevole di utenti potrebbe pertanto accedere automaticamente a Lync ogni giorno al momento della connessione a Windows, ma non utilizzare mai effettivamente Lync Server durante il periodo di connessione.

La metrica Utenti attivi univoci fornisce inoltre dati più significativi nelle organizzazioni in cui gli utenti generalmente non si disconnettono da Windows alla fine della giornata, preferendo bloccare i propri computer e lasciare Windows e Lync in esecuzione. In situazioni del genere si potrebbero registrare pochissimi accessi al giorno in quanto gli utenti si sono connessi molti giorni prima senza disconnettersi mai. Utenti attivi univoci tuttavia segnala se gli utenti utilizzano attivamente Lync o un altro client di Lync Server.

## Filtri

I filtri consentono di ottenere un set di dati più mirato o di visualizzare i dati restituiti in diversi modi. Il rapporto registrazione utenti ad esempio consente di visualizzare i dati di tutti i pool di registrazione e i server perimetrali oppure di visualizzare i dati di un singolo pool. È inoltre possibile scegliere la modalità di raggruppamento dei dati. In tal caso, le registrazioni vengono raggruppate in base all'ora, al giorno, alla settimana o al mese.

Nella tabella seguente sono riportati i filtri che è possibile utilizzare con il rapporto registrazione utenti.

### Filtri per il rapporto registrazione utenti

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
<td><p>Data e ora di inizio per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di inizio come segue:</p>
<p>7/7/2012 13.00</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>07.07.12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>03.07.12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data e ora di fine per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di fine come segue:</p>
<p>7/7/2012 13.00</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>07.07.12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>03.07.12</p>
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
<p>Se le date di inizio e fine superano il numero massimo di valori consentiti per l'intervallo specificato, verrà visualizzato solo il numero massimo di valori a partire dalla data di inizio. Se ad esempio si seleziona l'intervallo giornaliero con data di inizio 07/07/2012 e data di fine 28/02/2012, verranno visualizzati i dati per i giorni da 07/08/2012 ore 12.00 a 07/09/2012 ore 12.00 (per un totale di 31 giorni).</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool oppure selezionare <strong>[Tutto]</strong> per visualizzare i dati di tutti i pool. Le voci disponibili in questo elenco a discesa vengono inserite automaticamente in base ai record presenti nel database.</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente vengono riportate le informazioni fornite nel rapporto registrazione utenti.

### Metrica del rapporto registrazione utenti

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
<td><p>Indica l'intervallo di tempo selezionato sulla barra degli strumenti dei filtri. Ove applicabile, è possibile fare clic su un determinato intervallo di tempo per visualizzare informazioni dettagliate relative a tale intervallo. Se ad esempio si sta utilizzando l'intervallo giornaliero e si fa clic su 07/07/2012, verranno visualizzate le attività di registrazione degli utenti per tale data, suddivise per ore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale accessi</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni di accesso che hanno avuto esito positivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Accessi interni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di accessi nella rete interna.</p></td>
</tr>
<tr class="even">
<td><p><strong>Accessi esterni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di accessi dal di fuori della rete interna, utilizzando il server perimetrale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Utenti con accesso univoco</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di utenti che hanno avuto almeno una sessione di accesso. Un utente che ha avuto più sessioni di accesso viene considerato come un unico utente, al pari di una persona che ha avuto una sola sessione di accesso.</p></td>
</tr>
<tr class="even">
<td><p><strong>Utenti attivi univoci</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di utenti che sono stati coinvolti in una sessione peer-to-peer o di conferenza. Un utente che ha avuto più sessioni viene considerato come un unico utente, al pari di una persona che ha avuto una sola sessione.</p></td>
</tr>
</tbody>
</table>

