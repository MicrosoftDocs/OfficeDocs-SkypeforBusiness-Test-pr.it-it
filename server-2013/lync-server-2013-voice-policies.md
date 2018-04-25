---
title: 'Lync Server 2013: Criteri vocali'
TOCTitle: Criteri vocali
ms:assetid: b7433c62-9d8c-48af-89a0-19f0d34806ec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412891(v=OCS.15)
ms:contentKeyID: 49301743
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Criteri vocali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

I *criteri vocali* di Lync Server definiscono quanto segue per ogni utente, sito o organizzazione a cui viene assegnato il criterio:

  - Un set di funzionalità di chiamata che possono essere abilitate o disabilitate per determinare il livello di funzionalità VoIP aziendale disponibile per gli utenti.

  - Un set di record di utilizzo PSTN (Public Switched Telephone Network) che definiscono i tipi di chiamate autorizzati.

## Pianificazione dei criteri vocali

Per pianificare i criteri vocali che saranno necessari per la distribuzione di VoIP aziendale, è utile eseguire i passaggi seguenti:

  - Stabilire come verrà configurato il criterio vocale globale, ovvero il criterio vocale predefinito installato con il prodotto). Tale criterio verrà applicato a tutti gli utenti di VoIP aziendale a cui non è stato assegnato in modo esplicito un criterio a livello di sito o per utente.

  - Identificare eventuali criteri vocali a livello di sito che potrebbero essere necessari.

  - Identificare eventuali criteri vocali per utente che potrebbero essere necessari.

  - Decidere quali funzionalità di chiamata abilitare per ogni criterio vocale.

  - Stabilire quali record di utilizzo PSTN configurare per ogni criterio vocale.

## Ambito dei criteri vocali

L' *ambito dei criteri vocali* determina il livello gerarchico a cui è possibile applicare il criterio. In Lync Server è possibile configurare criteri vocali con i livelli di ambito seguenti (elencati dal più specifico al più generale):

  - Il **criterio vocale utente** può essere assegnato a singoli utenti, gruppi o oggetti contatto. Questo è il criterio di livello più basso. È possibile distribuire criteri vocali utente per abilitare le funzionalità per determinati utenti o gruppi in un sito, ma non per altri nello stesso sito. Si potrebbe decidere ad esempio di disabilitare le chiamate interurbane per alcuni dipendenti. Ai fini dell'assegnazione di un criterio vocale, un oggetto contatto viene considerato un singolo utente.
    

    > [!NOTE]
    > È consigliabile distribuire un criterio vocale utente per gli utenti di VoIP aziendale di un sito di succursale registrati nella distribuzione del sito centrale o gli utenti registrati in un Survivable Branch Appliance.



  - Il **criterio vocale di sito** si applica a un intero sito, con l'eccezione degli utenti, gruppi o oggetti contatto a cui è stato assegnato un criterio vocale utente. Per definire un criterio vocale di sito, è necessario specificare il sito a cui si applica il criterio. Se non viene assegnato un criterio vocale utente, viene utilizzato il criterio vocale di sito.

  - Il **criterio vocale globale** è il criterio vocale predefinito installato con il prodotto, È possibile modificare il criterio vocale globale per soddisfare esigenze specifiche dell'organizzazione, ma non è possibile rinominarlo o eliminarlo. Questo criterio vocale si applica a tutti gli utenti, gruppi e oggetti contatto di VoIP aziendale nella distribuzione, a meno che non venga configurato e assegnato un criterio vocale con un ambito più specifico. Se si desidera disabilitare completamente questo criterio, assicurarsi di assegnare criteri personalizzati a tutti i siti e tutti gli utenti.

## Funzionalità di chiamata

È possibile abilitare o disabilitare le funzionalità di chiamata seguenti per ogni criterio vocale:

  - L' **inoltro di chiamata** consente agli utenti di inoltrare chiamate ad altri telefoni e dispositivi client. Funzionalità abilitata per impostazione predefinita.

  - La **delega** consente agli utenti di specificare altri utenti per l'invio e la ricezione delle chiamate per loro conto. Funzionalità abilitata per impostazione predefinita.

  - Il **trasferimento di chiamata** consente agli utenti di trasferire chiamate ad altri utenti. Funzionalità abilitata per impostazione predefinita.

  - Il **parcheggio di chiamata** consente agli utenti di parcheggiare le chiamate e quindi di rispondere da un telefono o client diverso. Funzionalità disabilitata per impostazione predefinita.

  - Lo **squillo simultaneo** consente lo squillo su un telefono aggiuntivo (ad esempio, un cellulare) o altri dispositivi endpoint per le chiamate in arrivo. Funzionalità abilitata per impostazione predefinita.

  - L' **intercettazione team** consente agli utenti in uno team specificato di rispondere alle chiamate per gli altri membri del team. Funzionalità abilitata per impostazione predefinita.

  - Il **reindirizzamento PSTN** consente di reindirizzare le chiamate effettuate dagli utenti assegnati a questo criterio ad altri utenti dell'organizzazione sulla rete PSTN, in caso di congestione o non disponibilità della rete WAN. Funzionalità abilitata per impostazione predefinita.

  - L' **override dei criteri di larghezza di banda** consente agli amministratori di ignorare le decisioni per i criteri di controllo di ammissione di chiamata per un particolare utente. Funzionalità disabilitata per impostazione predefinita.

  - La **traccia delle chiamate moleste** consente agli utenti di segnalare chiamate moleste tramite il client Lync e quindi contrassegna tali chiamate nelle registrazioni dettagli chiamata. Questa funzionalità è disabilitata per impostazione predefinita.

  - L' **escape della segreteria telefonica** è una funzionalità basata sul valore di un timer che impedisce che le chiamate vengano instradate immediatamente alla segreteria telefonica del telefono cellulare dell'utente quando è configurato lo squillo simultaneo e il telefono è spento, scarico o in una zona senza copertura. Questa impostazione consente di abilitare e disabilitare il timer e di impostarne il valore. Questa funzionalità, che può essere configurata solo mediante Lync Server Management Shell, è disabilitata per impostazione predefinita.

  - La funzionalità **Usi PSTN inoltro di chiamata e squillo simultaneo dei telefoni** consente agli amministratori di specificare un utilizzo PSTN uguale al criterio vocale per l'inoltro di chiamata e lo squillo simultaneo, di limitare questo tipo di inoltro e di squillo ai soli utenti interni di Lync oppure di specificare un utilizzo PSTN personalizzato diverso dall'utilizzo PSTN del criterio vocale. Il comportamento predefinito prevede l'applicazione di un utilizzo PSTN uguale al criterio vocale per l'inoltro di chiamata e lo squillo simultaneo.

## Record di utilizzo PSTN

A ogni criterio vocale dovrebbero essere associati uno o più record di utilizzo PSTN. Gli utilizzi PSTN possono essere associati a un criterio vocale solo ai fini dello squillo simultaneo e dell'inoltro di chiamata. Per informazioni dettagliate sulla pianificazione dei record di utilizzo PSTN, vedere [Record utilizzo PSTN in Lync Server 2013](lync-server-2013-pstn-usage-records.md).


> [!NOTE]
> L'ordine degli utilizzi PSTN è fondamentale perché, in fase di abbinamento degli utenti alle route, la funzionalità di routing in uscita confronta gli utilizzi PSTN in ordine, dall'alto verso il basso. Se il primo utilizzo corrisponde alla route della chiamata, viene utilizzata tale route. In caso contrario, la funzionalità di routing in uscita cerca l'utilizzo PSTN successivo nell'elenco e continua fino a trovare una corrispondenza. In effetti, gli utilizzi PSTN successivi rappresentano un backup nel caso il primo nell'elenco non sia disponibile.


