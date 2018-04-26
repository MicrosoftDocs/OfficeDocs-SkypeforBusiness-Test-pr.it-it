---
title: Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013
TOCTitle: Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013
ms:assetid: 9aff949e-3dac-481a-be46-a180c72e8066
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398802(v=OCS.15)
ms:contentKeyID: 49301454
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-30_

Prima di avviare la distribuzione di Lync Server 2013 è necessario pianificare quanto segue:

  - La configurazione da utilizzare per la connessione alla rete PSTN (Public Switched Telephone Network)

  - La strategia per l'assegnazione delle aree di conferenza telefonica con accesso esterno ai numeri di accesso esterno

  - La strategia per la creazione delle directory conferenze

## Pianificazione della connettività PSTN per l'accesso esterno

Per la funzionalità di conferenza telefonica con accesso esterno sono necessari almeno un Mediation Server e un gateway PSTN.

È possibile distribuire un Mediation Server in un sito centrale o in un sito di succursale. In un sito centrale è possibile installare un Mediation Server in un pool Front End o in un server Standard Edition, oppure in un server o un pool autonomo. In un sito di succursale possibile è distribuire un Mediation Server in un server autonomo, oppure come componente di Survivable Branch Appliance.

È possibile distribuire un gateway PSTN in un sito centrale o in un sito di succursale. In un sito di succursale, il gateway PSTN può essere autonomo oppure può essere un componente di Survivable Branch Appliance.


> [!NOTE]
> Le conferenze telefoniche con accesso esterno non utilizzano il bypass multimediale, in quanto gli A/V Conferencing Server non supportano tale funzionalità.



Per informazioni dettagliate sulla pianificazione della configurazione di Mediation Server e gateway PSTN per la conferenza telefonica con accesso esterno, vedere [Componenti e topologie per Mediation Server in Lync Server 2013](lync-server-2013-components-and-topologies-for-mediation-server.md) nella documentazione relativa alla pianificazione.

## Pianificazione delle aree di conferenza telefonica con accesso esterno

Durante la configurazione dell'accesso esterno si creano dial plan e numeri di accesso per le conferenze telefoniche con accesso esterno. I dial plan sono set di regole di normalizzazione che specificano il numero e il formato delle cifre in un numero di telefono e convertono il numero di telefono nel formato standard E.164 per il routing delle chiamate. I numeri di accesso per le conferenze telefoniche con accesso esterno sono i numeri che i partecipanti chiamano per partecipare a una conferenza.

Ogni numero di accesso per le conferenze telefoniche con accesso esterno deve essere associato ad almeno un dial plan. Un'area di conferenza telefonica con accesso esterno associa un dial plan a uno o più numeri di accesso esterno. Quando si imposta un dial plan, si specifica l'area di conferenza telefonica con accesso esterno applicabile. Quando si crea il numero di accesso esterno, si selezionano le aree che associano il numero di accesso ai dial plan appropriati.

Quando si crea un dial plan se ne specifica l'ambito, che può essere a livello di utente, di pool o di sito. A ogni utente viene assegnato il dial plan per l'ambito più ristretto applicabile. Ad esempio, a un utente viene assegnato un dial plan a livello di utente, se ne esiste uno applicabile. Se non è applicabile un dial plan a livello di utente, gliene viene assegnato uno a livello di pool. Se non è applicabile un dial plan a livello di pool, gliene viene assegnato uno a livello di sito. Se non è applicabile un dial plan a livello di sito, gli viene assegnato il dial plan globale.

Prima di configurare i dial plan è importante pianificare la modalità di attribuzione dei nomi e di utilizzo delle aree. Di seguito sono riportate alcune considerazioni relative alle aree di conferenza telefonica con accesso esterno:

  - Un'area è in genere una regione geografica associata a un ufficio o un gruppo di uffici.

  - I numeri di accesso esterno sono associati a lingue. Se si supportano aree geografiche con più lingue, è opportuno stabilire come definire le aree per il supporto delle molteplici lingue. Ad esempio, è possibile definire più aree in base a una combinazione di geografia e lingua, oppure definire un'unica area basata sulla geografia e disporre di numeri di accesso esterno diversi per ogni lingua.

  - Quando un utente pianifica una riunione, per impostazione predefinita viene utilizzata l'area specificata dal dial plan dell'utente.

  - Per impostazione predefinita, nell'invito alla riunione vengono inclusi tutti numeri di accesso esterno per l'area.

  - È importante assegnare alle aree nomi che consentano di riconoscerle facilmente. L'utente può utilizzare questi nomi per modificare l'area di una riunione in modo che nell'invito vengano inclusi numeri di accesso diversi. Quando si utilizza Outlook per pianificare una riunione, per modificare l'area l'utente utilizza il componente aggiuntivo per riunioni online per Lync 2013).

  - Le aree vanno designate in modo che tutti gli invitati che desiderano accedere a una riunione possano visualizzare nell'invito un numero di accesso locale.

  - È possibile configurare l'ordine di visualizzazione dei numeri di accesso all'interno di un'area nella pagina Impostazioni conferenza telefonica con accesso esterno (e dunque l'ordine di visualizzazione nell'invito alla conferenza) utilizzando i cmdlet di Lync Server Management Shell.

  - Per partecipare a una conferenza, gli utenti possono chiamare da qualsiasi ubicazione qualsiasi numero di accesso esterno fornito.

## Pianificazione delle directory conferenze

Le directory conferenze gestiscono il mapping tra l'ID riunione alfanumerico utilizzato da un partecipante per accedere a una conferenza mediante Lync 2013 e l'ID conferenza numerico utilizzato da un partecipante di una conferenza telefonica con accesso esterno per accedere alla conferenza. Il formato dell'ID conferenza è il seguente:

    <housekeeping digit (1 digit)><conference directory (usually 1-2 digits)><conference number (variable number of digits><check digit (1 digit)>

La creazione di più directory di conferenze assicura che gli ID rimangano brevi finché non se ne crea una quantità considerevole. In un organizzazione con un numero tipo di conferenze per utente, è consigliabile creare una directory di conferenze per ogni 999 utenti nel pool. Attenendosi a questa indicazioni, gli ID conferenza rimangono in genere brevi. Tuttavia, una volta che il numero di directory di conferenze (in più pool) supera 9, l'ID diventerà di dimensioni maggiori per supportare ulteriori conferenze.

## Vedere anche

#### Concetti

[Componente Mediation Server in Lync Server 2013](lync-server-2013-mediation-server-component.md)  
[Dial plan e regole di normalizzazione in Lync Server 2013](lync-server-2013-dial-plans-and-normalization-rules.md)

