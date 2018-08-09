---
title: "Lync Server 2013: Prerequisiti di configuraz. e sicurezza per VoIP aziendale"
TOCTitle: Prerequisiti di configurazione e sicurezza per VoIP aziendale
ms:assetid: 15354abe-733e-466b-bcd4-a6cfbf58caf8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398221(v=OCS.15)
ms:contentKeyID: 49299778
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti di configurazione e sicurezza per VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

Verificare che l'infrastruttura soddisfi i prerequisiti di sicurezza, configurazione utente e hardware specifici dello scenario.

## Diritti amministrativi e infrastruttura di certificazione

Verificare che nell'ambiente siano configurati i gruppi di utenti con privilegi amministrativi e l'infrastruttura di certificazione seguenti da utilizzare durante il processo di distribuzione di VoIP aziendale.

  - Gli amministratori che distribuiscono VoIP aziendale devono essere membri del gruppo RTCUniversalServerAdmins.

  - Gli amministratori che eseguono le attività di configurazione devono disporre di diritti appropriati:
    
      - **CsVoiceAdministrator:** questo ruolo di amministratore consente di eseguire attività di configurazione vocale, di gestire le applicazioni vocali e di assegnare criteri vocali agli utenti finali.
    
      - **CsUserAdministrator:** questo ruolo di amministratore consente di gestire le proprietà degli utenti, ad esempio l'abilitazione di VoIP aziendale per un utente. Consente inoltre di assegnare criteri per utente, ad eccezione del criterio di archiviazione, di spostare gli utenti e di gestire i telefoni di area comune e i dispositivi analogici.
    
      - **CsAdministrator:** questo ruolo di amministratore consente di eseguire tutte le attività di CsVoiceAdministrator e CsUserAdministrator.
    

    > [!NOTE]
    > La delega consente a più amministratori di partecipare alla distribuzione di Lync Server senza dover concedere accesso non necessario alle risorse.



  - La distribuzione e la configurazione dell'infrastruttura MKI (Managed Key Infrastructure) vengono eseguite utilizzando un'infrastruttura di autorità di certificazione (CA) Microsoft o di terze parti.
    

    > [!NOTE]
    > Per informazioni dettagliate sui requisiti dei certificati in Lync Server, vedere <A href="lync-server-2013-certificate-infrastructure-requirements.md">Requisiti dell'infrastruttura dei certificati per Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Configurazione utente

Se il Mediation Server è stato collocato con ogni pool Front End o server Standard Edition durante la distribuzione Front End, le impostazioni utente necessarie per VoIP aziendale sono state configurate automaticamente durante l'installazione dei file per tali ruoli del server.

Se si sta procedendo ora alla distribuzione del carico di lavoro di VoIP aziendale, prima di iniziare il processo di distribuzione designare un numero di telefono primario per ogni utente che si intende abilitare per VoIP aziendale. In qualità di amministratori, è necessario verificare che questo numero sia univoco. Prima dell'implementazione, è necessario normalizzare tutti i numeri di telefono primari (in modo che siano nel formato corretto) e copiarli nella proprietà **URI linea** di ogni utente utilizzando il Pannello di controllo di Lync Server.


> [!NOTE]
> Per alcuni esempi di numeri di telefono primari necessari per la distribuzione di VoIP aziendale, vedere la sezione <A href="lync-server-2013-dial-plans-and-normalization-rules.md">Dial plan e regole di normalizzazione in Lync Server 2013</A> di <A href="lync-server-2013-dial-plans-and-normalization-rules.md">Dial plan e regole di normalizzazione in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Passaggi successivi: installare i file o configurare la connettività PSTN

Dopo avere verificato i prerequisiti software e ambientali per VoIP aziendale, è possibile utilizzare il contenuto seguente per eseguire una delle operazioni indicate di seguito:

  - Installare il Mediation Server, come descritto in [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md), ma solo se si desidera distribuire un Mediation Server o un pool autonomo, poiché i Mediation Server vengono installati con il processo di distribuzione del pool Front End o del server Standard Edition quando vengono collocati.

  - In alternativa, iniziare la configurazione delle impostazioni per il routing delle chiamate per gli utenti di VoIP aziendale, come descritto in [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md).

