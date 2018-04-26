---
title: 'Lync Server 2013: Dial plan e regole di normalizzazione'
TOCTitle: Dial plan e regole di normalizzazione
ms:assetid: fde45195-6eb4-403c-9094-57df7fc0bd2a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413082(v=OCS.15)
ms:contentKeyID: 49302576
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Dial plan e regole di normalizzazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per dial plan si intende un set denominato di regole di normalizzazione che consente di convertire i numeri di telefono relativi a una località, a un utente o a un oggetto contatto specifico in un unico formato standard (E.164) ai fini dell'autorizzazione del telefono e del routing della chiamata.

Le regole di normalizzazione definiscono il modo in cui i numeri di telefono espressi nei vari formati devono essere instradati per ogni posizione, utente o oggetto contatto specificato. La stessa stringa di composizione può essere interpretata e convertita in modo diverso a seconda della località dalla quale viene composta e dalla persona o dall'oggetto contatto che effettua la chiamata.

## Ambito del dial plan

L' *ambito* di un dial plan determina il livello gerarchico a cui è possibile applicare il dial plan. In Lync Server a un utente è possibile assegnare un dial plan specifico per utente. Se non viene assegnato un dial plan utente, viene applicato il dial plan del pool di registrazione. Se non è presente alcun dial plan del pool di registrazione, viene applicato il dial plan del sito. Infine, se non è presente alcun altro dial plan applicabile all'utente, viene applicato il dial plan globale.

I client ottengono i livelli di ambito del dial plan tramite impostazioni di provisioning di tipo in-band fornite quando gli utenti accedono a Lync Server. L'amministratore può gestire e assegnare i livelli di ambito del dial plan utilizzando Pannello di controllo di Lync Server.


> [!NOTE]
> Il dial plan del gateway PSTN (Public Switched Telephone Network) del livello di servizio viene applicato alle chiamate in arrivo da un determinato gateway.



I livelli di ambito del dial plan sono definiti come segue:

  - **Dial plan utente :** può essere assegnato a singoli utenti, gruppi o oggetti contatto. Le applicazioni vocali possono cercare e utilizzare un dial plan per utente quando si riceve una chiamata con un valore di contesto telefonico impostato su predefinito dell'utente. Ai fini dell'assegnazione di un dial plan, un oggetto contatto è trattato come un singolo utente.

  - **Dial plan pool :** può essere creato a livello di servizio per qualsiasi gateway PSTN o pool di registrazione nella topologia. Per definire un dial plan pool, è necessario specificare un particolare servizio (gateway PSTN o pool di registrazione) a cui applicare il dial plan.

  - **Dial plan sito :** può essere creato per un intero sito tranne che per utenti, gruppi o oggetti contatti assegnati a un dial plan pool o a un dial plan utente. Per definire un dial plan sito, è necessario specificare il sito a cui applicare il dial plan.

  - **Dial plan globale :** è il dial plan predefinito installato con il prodotto. È possibile modificare il dial plan globale, ma non eliminarlo. Questo dial plan si applica a tutti gli utenti, i gruppi e gli oggetti contatti di VoIP aziendale nella distribuzione a meno che non si configuri e assegni un dial plan con ambito più specifico.

## Pianificazione di dial plan

Per pianificare un dial plan, seguire la procedura seguente:

  - Elencare tutte le località in cui l'organizzazione ha una sede.
    
    L'elenco deve essere aggiornato e completo. Dovrà essere rivisto con l'evolversi della società. Nelle grandi società multinazionali con numerose filiali, questa attività può richiedere molto tempo.

  - Identificare formati di numeri validi per ogni sito.
    
    La parte della pianificazione dei dial plan che richiede più tempo è l'identificazione dei formati di numeri validi per ogni sito. In alcuni casi, può essere possibile copiare negli altri dial plan le regole di normalizzazione scritte per un dial plan, in particolare se i siti corrispondenti si trovano nello stesso paese, nella stessa area geografica o anche nello stesso continente. In altri casi, possono essere sufficienti piccole modifiche dei numeri in un dial plan per utilizzarli in altri dial plan.

  - Sviluppare uno schema a livello di organizzazione per la denominazione dei dial plan.
    
    L'adozione di uno schema di denominazione standard assicura la coerenza all'interno dell'organizzazione e agevola la manutenzione e gli aggiornamenti.

  - Stabilire se sono necessari più dial plan per una singola località.
    
    Se l'organizzazione utilizza un unico dial plan in più località, potrebbe essere comunque necessario creare un dial plan distinto per gli utenti di VoIP aziendale in fase di migrazione da un PBX (Private Branch Exchange) che hanno la necessità di conservare i numeri di interno esistenti.

  - Stabilire se sono necessari dial plan per utente. Ad esempio, se in una succursale sono presenti utenti registrati con il sito centrale o utenti registrati in un Survivable Branch Appliance, è possibile soddisfare le esigenze degli scenari di composizione specifici con dial plan per utente e regole di normalizzazione. Per informazioni dettagliate, vedere [Requisiti di resilienza dei siti di succursale per Lync Server 2013](lync-server-2013-branch-site-resiliency-requirements.md).

  - Determinare l'ambito del dial plan (come descritto in precedenza in questo argomento).

Per creare un dial plan, specificare valori nei campi seguenti, come richiesto, utilizzando Pannello di controllo di Lync Server o Lync Server Management Shell.

## Nome e nome semplice

Per i dial plan utente, è necessario specificare un nome descrittivo che identifichi gli utenti, i gruppi o gli oggetti contatto a cui verrà assegnato il dial plan. Per i dial plan sito, il campo Nome è precompilato con il nome del sito e non può essere modificato. Per i dial plan pool, il campo Nome è precompilato con il nome di dominio completo (FQDN) del gateway PSTN o del pool Front End e non può essere modificato.

Il *Nome semplice* del dial plan è precompilato con una stringa derivata dal nome del dial plan. Il campo Nome semplice è modificabile e abilita la creazione di una convenzione di denominazione più descrittiva per i dial plan. Il valore *Nome semplice* non può essere vuoto e deve essere univoco. È consigliabile sviluppare una convenzione di denominazione per l'intera organizzazione e utilizzarla in modo coerente per tutti i siti e gli utenti.

## Descrizione

Si consiglia di digitare il nome comune e riconoscibile della località geografica a cui si applica il dial plan corrispondente. Se ad esempio il nome del dial plan è Londra.Contoso.com, la descrizione consigliabile è Londra.

## Area conferenza telefonica con accesso esterno

Se si distribuisce la funzionalità di conferenza telefonica con accesso esterno, è necessario specificare un'area della conferenza telefonica con accesso esterno per associare i numeri di accesso relativi a un dial plan.

## Prefisso accesso esterno

È possibile specificare un prefisso di accesso esterno di un massimo di quattro caratteri (\#, \* e 0-9) se gli utenti devono comporre una o più cifre iniziali aggiuntive (ad esempio 9) per ottenere una linea esterna.


> [!NOTE]
> Se si specifica un prefisso di accesso esterno, non è necessario creare una regola di normalizzazione aggiuntiva per regolare il prefisso.



## Regole di normalizzazione

Le regole di normalizzazione definiscono la modalità di routing di numeri di telefono espressi in formati diversi per la località specifica. La stessa stringa numerica può essere interpretata e convertita in modo diverso a seconda delle impostazioni internazionali della località da cui viene composta. Sono necessarie per il routing delle chiamate, perché gli utenti possono utilizzare vari formati quando immettono i numeri di telefono nei rispettivi elenchi contatti.

La normalizzazione dei numeri di telefono forniti dall'utente rende disponibile un formato coerente che consente le seguenti attività:

  - Far corrispondere un numero composto all'URI SIP del destinatario previsto.

  - Applicare le regole di composizione per il chiamante.

Di seguito sono riportati alcuni campi numerici che può essere necessario includere nelle regole di normalizzazione:

  - Dial plan

  - Codice paese

  - Indicativo di località

  - Lunghezza numero di interno

  - Prefisso sito

## Creazione di regole di normalizzazione

Le regole di normalizzazione utilizzano le espressioni regolari di .NET Framework per specificare formati di corrispondenza numerica che il server utilizza per convertire le stringhe di composizione nel formato E.164 allo scopo di eseguire la ricerca inversa dei numeri. È possibile creare regole di normalizzazione nel Pannello di controllo di Lync Server immettendo manualmente le espressioni o immettendo le cifre iniziali e la lunghezza delle stringhe di composizione da associare e consentendo al Pannello di controllo di Lync Server di generare automaticamente l'espressione regolare corrispondente. In ogni caso, al termine è possibile immettere un numero di test per verificare che la regola di normalizzazione funzioni come previsto.

Per informazioni dettagliate sull'utilizzo di espressioni regolari di .NET Framework, vedere "Espressioni regolari di .NET Framework" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=140927](http://go.microsoft.com/fwlink/p/?linkid=140927).

## Regole di normalizzazione di esempio

Nella tabella seguente sono illustrati alcuni esempi di regole di normalizzazione scritte come espressioni regolari di .NET Framework. Si tratta di esempi puramente indicativi che non devono essere intesi come riferimenti obbligatori per la creazione di regole di normalizzazione.

### Tabella 1. Regole di normalizzazione tramite espressioni regolari di .NET Framework

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome regola</th>
<th>Descrizione</th>
<th>Formato numero</th>
<th>Conversione</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>4digitExtension</p></td>
<td><p>Converte i numeri di interno a 4 cifre</p></td>
<td><p>^(\d{4})$</p></td>
<td><p>+1425555$1</p></td>
<td><p>0100 viene convertito in +14255550100</p></td>
</tr>
<tr class="even">
<td><p>5digitExtension</p></td>
<td><p>Converte i numeri di interno a 5 cifre</p></td>
<td><p>^5(\d{4})$</p></td>
<td><p>+1425555$1</p></td>
<td><p>50100 viene convertito in +14255550100</p></td>
</tr>
<tr class="odd">
<td><p>7digitcallingRedmond</p></td>
<td><p>Converte i numeri a 7 cifre in numeri locali di Redmond</p></td>
<td><p>^(\d{7})$</p></td>
<td><p>+1425$1</p></td>
<td><p>5550100 viene convertito in +14255550100</p></td>
</tr>
<tr class="even">
<td><p>7digitcallingDallas</p></td>
<td><p>Converte i numeri a 7 cifre in numeri locali di Dallas</p></td>
<td><p>^(\d{7})$</p></td>
<td><p>+1972$1</p></td>
<td><p>5550100 viene convertito in +19725550100</p></td>
</tr>
<tr class="odd">
<td><p>10digitcallingUS</p></td>
<td><p>Converte i numeri a 10 cifre in numeri degli Stati Uniti</p></td>
<td><p>^(\d{10})$</p></td>
<td><p>+1$1</p></td>
<td><p>2065550100 viene convertito in +12065550100</p></td>
</tr>
<tr class="even">
<td><p>LDCallingUS</p></td>
<td><p>Converte i numeri con prefissi interurbani in numeri degli Stati Uniti</p></td>
<td><p>^1(\d{10})$</p></td>
<td><p>+$1</p></td>
<td><p>12145550100 viene convertito in +2145550100</p></td>
</tr>
<tr class="odd">
<td><p>IntlCallingUS</p></td>
<td><p>Converte i numeri con prefissi internazionali in numeri degli Stati Uniti</p></td>
<td><p>^011(\d*)$</p></td>
<td><p>+$1</p></td>
<td><p>01191445550100 viene convertito in +91445550100</p></td>
</tr>
<tr class="even">
<td><p>RedmondOperator</p></td>
<td><p>Converte il numero 0 nel numero dell'operatore di Redmond</p></td>
<td><p>^0$</p></td>
<td><p>+14255550100</p></td>
<td><p>0 viene convertito in +14255550100</p></td>
</tr>
<tr class="odd">
<td><p>RedmondSitePrefix</p></td>
<td><p>Converte i numeri con prefisso on-net (6) e il codice sito di Redmond (222)</p></td>
<td><p>^6222(\d{4})$</p></td>
<td><p>+1425555$1</p></td>
<td><p>62220100 viene convertito in +14255550100</p></td>
</tr>
<tr class="even">
<td><p>NYSitePrefix</p></td>
<td><p>Converte i numeri con prefisso on-net (6) e il codice sito di NY (333)</p></td>
<td><p>^6333(\d{4})$</p></td>
<td><p>+1202555$1</p></td>
<td><p>63330100 viene convertito in +12025550100</p></td>
</tr>
<tr class="odd">
<td><p>DallasSitePrefix</p></td>
<td><p>Converte i numeri con prefisso on-net (6) e il codice sito di Dallas (444)</p></td>
<td><p>^6444(\d{4})$</p></td>
<td><p>+1972555$1</p></td>
<td><p>64440100 viene convertito in +19725550100</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente viene illustrato un esempio di dial plan per Redmond, Washington, Stati Uniti, in base alle regole di normalizzazione riportate nella tabella precedente.

### Tabella 2. Dial plan di Redmond basato sulle regole di normalizzazione riportate nella tabella 1

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Redmond.forestFQDN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5digitExtension</p></td>
</tr>
<tr class="even">
<td><p>7digitcallingRedmond</p></td>
</tr>
<tr class="odd">
<td><p>10digitcallingUS</p></td>
</tr>
<tr class="even">
<td><p>IntlCallingUS</p></td>
</tr>
<tr class="odd">
<td><p>RedmondSitePrefix</p></td>
</tr>
<tr class="even">
<td><p>NYSitePrefix</p></td>
</tr>
<tr class="odd">
<td><p>DallasSitePrefix</p></td>
</tr>
<tr class="even">
<td><p>RedmondOperator</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> I nomi delle regole di normalizzazione illustrate nella tabella precedente non includono spazi, ma si tratta di una scelta. Il primo nome della tabella, ad esempio, potrebbe essere "5 digit extension" o "5-digit Extension" ed essere comunque valido.


