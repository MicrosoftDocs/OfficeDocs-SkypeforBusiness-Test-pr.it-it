---
title: 'Lync Server 2013: Abilitazione degli utenti per i servizi di emergenza'
TOCTitle: Abilitazione degli utenti per i servizi di emergenza
ms:assetid: 3cc64f5b-492e-4c47-9713-3c376f2aad02
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425892(v=OCS.15)
ms:contentKeyID: 49300275
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione degli utenti per i servizi di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-06_

Durante la registrazione client Lync Server utilizza un criterio percorso per configurare le proprietà E9-1-1 degli utenti abilitati per VoIP aziendale. In un criterio percorso sono contenute tutte le impostazioni che definiscono come verrà implementata la funzionalità E9-1-1. Sono contenute ad esempio informazioni come la stringa di composizione di emergenza e l'eventuale obbligo per un utente di immettere manualmente una posizione qualora non ne venga fornita automaticamente una dal servizio Informazioni percorso. Per una definizione completa di un criterio percorso, vedere [Definizione di criteri percorso per Lync Server 2013](lync-server-2013-defining-the-location-policy.md).

Lync Server può assegnare un criterio percorso ai client in base alla subnet oppure agli utenti in base a un criterio di tipo globale, per sito o per utente. Per decidere come abilitare gli utenti, è consigliabile innanzitutto tenere conto degli aspetti seguenti.

  - **Valutare se si prevede di abilitare tutti gli utenti o di limitare il supporto a specifiche aree geografiche dell'organizzazione**  
    È possibile assegnare una posizione a tutti gli utenti dell'organizzazione utilizzando un criterio percorso globale. Assegnando tuttavia un criterio percorso a un sito di rete di Lync Server e aggiungendo quindi le subnet al sito, è possibile limitare il supporto E9-1-1 a località selezionate nell'organizzazione e specificare il comportamento di routing di E9-1-1 in base al sito.

<!-- end list -->

  - **Valutare se si prevede di abilitare singoli utenti mediante un criterio utente**  
    È possibile assegnare criteri percorso direttamente a utenti specifici o a oggetti contatto di telefoni di area comune se si desidera personalizzare il relativo supporto E9-1-1.

<!-- end list -->

  - **Valutare se abilitare per E9-1-1 i client che effettuano il roaming all'esterno della rete o si connettono da una subnet non definita**  
    È possibile che gli utenti a cui è stato assegnato un criterio percorso globale, per sito o per utente debbano immettere manualmente una posizione nel client se il client non è posizionato in una subnet definita o se non è stata trovata alcuna posizione da parte del servizio Informazioni percorso. Per informazioni dettagliate, vedere [Definizione dell'esperienza utente per l'acquisizione manuale di una posizione in Lync Server 2013](lync-server-2013-defining-the-user-experience-for-manually-acquiring-a-location.md).

