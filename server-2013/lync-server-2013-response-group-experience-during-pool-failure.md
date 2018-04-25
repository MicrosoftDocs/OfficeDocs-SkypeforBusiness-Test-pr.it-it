---
title: 'Lync Server 2013: Esperienza dei Response Group durante un errore del pool'
TOCTitle: Esperienza dei Response Group durante un errore del pool
ms:assetid: 4e00fb38-64b1-4fd9-903d-7639177bc303
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204886(v=OCS.15)
ms:contentKeyID: 49300502
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esperienza dei Response Group in Lync Server 2013 durante un errore del pool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione viene descritto in dettaglio in che modo l'attività dei Response Group viene interessata dalle circostanze seguenti:

  - Si verifica un'interruzione nel pool primario, ma il failover non è ancora attivo.

  - Il failover del servizio al pool di backup è attivo.

  - Il failback del servizio al pool primario è attivo.

## Esperienza utente in caso di interruzione

Se si verifica un'interruzione del pool o del sito e l'amministratore non ha ancora avviato il failover, l'attività dei Response Group viene gestita come illustrato nella tabella seguente.


> [!NOTE]
> Durante il ripristino di emergenza, il comportamento delle chiamate è diverso, a seconda che i Response Group del pool primario siano stati importati o meno nel pool di backup durante il ripristino. Nella tabella seguente i riferimenti all'importazione dei Response Group si riferiscono all'importazione dei Response Group del pool primario nel pool di backup durante il ripristino di emergenza.



### Interruzione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di chiamata o azione utente</th>
<th>Durante l'interruzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiamate connesse a un agente</p></td>
<td><ul>
<li><p>Le chiamate normali restano connesse.</p></li>
<li><p>Le chiamate anonime vengono disconnesse.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamate in corso non ancora connesse a un agente</p></td>
<td><p>Le chiamate vengono disconnesse.</p></td>
</tr>
<tr class="odd">
<td><p>Nuove chiamate</p></td>
<td><ul>
<li><p>Le chiamate vengono disconnesse.</p></li>
<li><p>Se i Response Group sono stati importati, le chiamate vengono connesse al pool di backup, ma gli agenti disponibili nel pool primario non sono raggiungibili.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamate degli agenti per conto del Response Group</p></td>
<td><p>La funzionalità è disabilitata in questa fase.</p></td>
</tr>
<tr class="odd">
<td><p>Accesso e informazioni degli agenti</p></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati sulla console degli agenti, ma questi ultimi non possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti importati non sono visualizzati sulla console degli agenti.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configurazione dei Response Group</p></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati, a seconda della disponibilità del database back-end del pool primario, ma non possono essere modificati.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati e modificati.</p></li>
<li><p>I Response Group importati non possono essere visualizzati con il Pannello di controllo di Lync Server o lo Strumento di configurazione di Response Group, ma possono essere configurati mediante cmdlet di Lync Server Management Shell.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Esperienza utente durante il failover

Quando un amministratore richiama il failover a un pool di backup, durante e dopo il failover l'attività dei Response Group viene gestita come descritto nella tabella che segue. La prima colonna descrive il tipo di attività che potrebbe avere luogo. La colonna centrale descrive in che modo ciascuna attività viene gestita durante il breve periodo necessario per il failover al pool di backup. L'ultima colonna descrive in che modo l'attività viene gestita per un periodo più lungo, dopo il completamento del processo di failover, durante il quale il pool di backup prende il posto del pool primario.


> [!NOTE]
> Durante il ripristino di emergenza, il comportamento delle chiamate è diverso, a seconda che i Response Group del pool primario siano stati importati o meno nel pool di backup durante il ripristino. Nella tabella seguente i riferimenti all'importazione dei Response Group si riferiscono all'importazione dei Response Group del pool primario nel pool di backup durante il ripristino di emergenza.



### Attivazione del failover

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di chiamata o azione utente</th>
<th>Durante il failover</th>
<th>Dopo il completamento del failover</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiamate connesse a un agente</p></td>
<td><ul>
<li><p>Le chiamate normali restano connesse.</p></li>
<li><p>Le chiamate anonime vengono disconnesse.</p></li>
</ul></td>
<td><ul>
<li><p>Le chiamate normali restano connesse.</p></li>
<li><p>Per i Response Group importati, le chiamate anonime che hanno raggiunto il pool di backup restano connesse.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamate in corso non ancora connesse a un agente</p></td>
<td><p>Le chiamate vengono disconnesse.</p></td>
<td><ul>
<li><p>Se i Response Group non sono stati importati, non ci sono chiamate con questo stato.</p></li>
<li><p>Per i Response Group importati, le chiamate che hanno raggiunto il pool di backup restano connesse.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nuove chiamate</p></td>
<td><ul>
<li><p>Le chiamate vengono disconnesse.</p></li>
<li><p>Per i Response Group importati, le chiamate vengono connesse al pool di backup, ma gli agenti disponibili nel pool primario non sono raggiungibili.</p></li>
</ul></td>
<td><ul>
<li><p>Se i Response Group non sono stati importati, le chiamate vengono disconnesse.</p></li>
<li><p>Per i Response Group importati, le chiamate vengono connesse al pool di backup.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamate degli agenti per conto del Response Group</p></td>
<td><p>La funzionalità è disabilitata in questa fase.</p></td>
<td><ul>
<li><p>Se i Response Group non sono stati importati, le chiamate non riescono.</p></li>
<li><p>Per i Response Group importati, le chiamate vengono effettuate.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Accesso e informazioni degli agenti</p></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati sulla console degli agenti, ma questi ultimi non possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti importati vengono visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
</ul></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati sulla console degli agenti, ma questi ultimi non possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti importati vengono visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configurazione dei Response Group</p></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati, a seconda della disponibilità del database back-end del pool primario, ma non possono essere modificati.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati e modificati.</p></li>
<li><p>I Response Group importati non possono essere visualizzati con il Pannello di controllo di Lync Server o lo Strumento di configurazione di Response Group, ma possono essere configurati mediante cmdlet di Lync Server Management Shell.</p></li>
</ul></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati, a seconda della disponibilità del database back-end, ma non possono essere modificati.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati e modificati.</p></li>
<li><p>I Response Group importati non possono essere visualizzati con il Pannello di controllo di Lync Server o lo Strumento di configurazione di Response Group, ma possono essere configurati mediante cmdlet di Lync Server Management Shell.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Esperienza utente durante il failback

Quando un amministratore richiama il failback al pool primario, durante e dopo il failback l'attività dei Response Group viene gestita come descritto nella tabella che segue.


> [!NOTE]
> Durante il ripristino di emergenza, il comportamento delle chiamate è diverso, a seconda che i Response Group del pool primario siano stati importati o meno nel pool di backup durante il ripristino. Nella tabella seguente i riferimenti all'importazione dei Response Group si riferiscono all'importazione dei Response Group del pool primario nel pool di backup durante il ripristino di emergenza.



### Gestione delle chiamate in failback

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di chiamata o azione utente</th>
<th>Durante il failback</th>
<th>Dopo il completamento del failback</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiamate connesse a un agente</p></td>
<td><ul>
<li><p>Le chiamate normali restano connesse.</p></li>
<li><p>Se i Response Group non sono stati importati, non ci sono chiamate anonime con questo stato.</p></li>
<li><p>Per i Response Group importati, le chiamate anonime restano connesse.</p></li>
</ul></td>
<td><ul>
<li><p>Le chiamate normali restano connesse.</p></li>
<li><p>Se i Response Group non sono stati importati, non ci sono chiamate anonime con questo stato.</p></li>
<li><p>Per i Response Group importati, le chiamate anonime restano connesse.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamate in corso non ancora connesse a un agente</p></td>
<td><ul>
<li><p>Se i Response Group non sono stati importati, non ci sono chiamate con questo stato.</p></li>
<li><p>Per i Response Group importati, le chiamate vengono disconnesse.</p></li>
</ul></td>
<td><ul>
<li><p>Se i Response Group non sono stati importati, non ci sono chiamate con questo stato.</p></li>
<li><p>Per i Response Group importati, le chiamate vengono disconnesse.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nuove chiamate</p></td>
<td><p>Le chiamate vengono connesse al pool primario, ma gli agenti disponibili in questo pool non sono raggiungibili.</p></td>
<td><p>Le chiamate vengono connesse al pool primario.</p></td>
</tr>
<tr class="even">
<td><p>Chiamate degli agenti per conto del Response Group</p></td>
<td><p>La funzionalità è disabilitata in questa fase.</p></td>
<td><p>Le chiamate vengono effettuate.</p></td>
</tr>
<tr class="odd">
<td><p>Accesso e informazioni degli agenti</p></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati sulla console degli agenti, ma questi ultimi non possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti importati vengono visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
</ul></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati sulla console degli agenti e questi ultimi possono effettuare l'accesso.</p></li>
<li><p>I gruppi di agenti importati non sono visualizzati sulla console degli agenti.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configurazione dei Response Group</p></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati, a seconda della disponibilità del database back-end del pool primario, ma non possono essere modificati.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati e modificati.</p></li>
<li><p>I Response Group importati non possono essere visualizzati con il Pannello di controllo di Lync Server o lo Strumento di configurazione di Response Group, ma possono essere configurati mediante cmdlet di Lync Server Management Shell.</p></li>
</ul></td>
<td><ul>
<li><p>I gruppi di agenti di proprietà del pool primario possono essere visualizzati e modificati.</p></li>
<li><p>I gruppi di agenti di proprietà del pool di backup possono essere visualizzati e modificati.</p></li>
<li><p>I Response Group importati non possono essere visualizzati con il Pannello di controllo di Lync Server o lo Strumento di configurazione di Response Group, ma possono essere configurati mediante cmdlet di Lync Server Management Shell.</p></li>
</ul></td>
</tr>
</tbody>
</table>

