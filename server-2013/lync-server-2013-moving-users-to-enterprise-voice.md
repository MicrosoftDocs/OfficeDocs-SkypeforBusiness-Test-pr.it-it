---
title: 'Lync Server 2013: Spostamento di utenti in VoIP aziendale'
TOCTitle: Spostamento di utenti in VoIP aziendale
ms:assetid: a2df6d51-5cf2-4d3e-8f97-496af5fd5e5e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412758(v=OCS.15)
ms:contentKeyID: 49301535
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostamento di utenti in VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

Se si desidera spostare gli utenti da un'infrastruttura di telefonia PBX esistente a VoIP aziendale, il processo di distribuzione include alcuni passaggi che non fanno parte del processo di pianificazione già descritto in [Pianificazione di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice.md). Per informazioni sulla migrazione di utenti da una distribuzione di VoIP aziendale precedente, vedere i documenti sulla migrazione forniti con il supporto di installazione.

Il processo di trasferimento degli utenti da un'infrastruttura di telefonia esistente a VoIP aziendale prevede i passaggi seguenti:

1.  Designazione dei numeri di telefono primari.

2.  Abilitazione degli utenti per VoIP aziendale.

3.  Preparare i dial plan per gli utenti.

4.  Pianificazione dei criteri vocali per gli utenti.

5.  Pianificazione delle route delle chiamate.

6.  Configurazione del sistema PBX o del trunk SIP per il reinstradamento delle chiamate degli utenti abilitati per VoIP aziendale.

7.  Trasferimento degli utenti alla Messaggistica unificata di Exchange (operazione consigliata).

In questo argomento sono descritte le attività di pianificazione necessarie per ognuno di questi passaggi.

## Passaggio 1. Designare i numeri di telefono primari

VoIP aziendale integra funzionalità vocali con altre funzionalità multimediali di messaggistica. Ad esempio, quando il server riceve una chiamata in arrivo, esegue il mapping del numero all'URI SIP dell'utente e quindi inoltra la chiamata a tutti gli endpoint client associati a tale URI SIP. Per questo processo è necessario che ogni utente sia associato a un numero di telefono primario.

Un numero di telefono primario deve avere le caratteristiche seguenti:

  - Deve essere globalmente univoco o, nel caso dei numeri di interno, univoco nell'azienda.

  - Deve essere di proprietà dell'azienda e instradabile. Non deve essere un numero personale.

In Servizi di dominio Active Directory possono essere elencati due o più numeri di telefono per gli utenti Enterprise. Tutti i numeri di telefono associati a un determinato utente possono essere visualizzati o modificati nella finestra delle proprietà dell'utente nello snap-in Utenti e computer di Active Directory.

La casella **Numero di telefono** nella scheda **Generale** della finestra di dialogo **Proprietà utente** deve contenere il numero di lavoro principale dell'utente. Questo numero viene in genere designato come numero di telefono primario.

Alcuni utenti potrebbero avere requisiti particolari, ad esempio per un dirigente può essere necessario instradare tutte le chiamate in arrivo a un assistente amministrativo. Tali eccezioni devono essere limitate solo a casi di evidente necessità.

Una volta scelto, il numero primario deve essere:

  - Normalizzato nel formato E.164, quando possibile.

  - Copiato nell'attributo **msRTCSIP-line** di Active Directory.
    

    > [!NOTE]
    > <STRONG>Coesistenza con il controllo delle chiamate remote (RCC)</STRONG><BR>Il controllo delle chiamate remote (RCC, Remote Call Control) è la possibilità di utilizzare Lync Server per monitorare e controllare un telefono PBX da scrivania. Il controllo viene instradato tramite il server, che funge da gateway verso il centralino (PBX). Non è possibile configurare un utente sia per RCC che per VoIP aziendale. In entrambi i casi, tuttavia il numero di telefono primario dell'utente viene designato dall'impostazione URI linea.<BR>Se si desidera che alcuni utenti selezionati continuino a utilizzare un'infrastruttura PBX esistente, è possibile introdurre VoIP aziendale nell'organizzazione in modo graduale. Per informazioni dettagliate su questo scenario di distribuzione, vedere <A href="lync-server-2013-direct-sip-deployment-options.md">Opzioni di distribuzione SIP diretta in Lync Server 2013</A> nella documentazione relativa alla pianificazione.<BR>Nelle versioni precedenti per uno stesso utente è possibile abilitare sia RCC che VoIP aziendale, ma solo se per l'utente è configurata anche la funzionalità di biforcazione doppia, con la quale una chiamata in arrivo fa squillare il telefono PBX dell'utente e Communicator contemporaneamente. In Lync Server 2010 la funzionalità di biforcazione doppia non è supportata.



Per popolare l'attributo **msRTCSIP-line** sono disponibili tre metodi:

  - Microsoft Identity Integration Server (scelta consigliata)

  - La pagina **Utenti** nel Pannello di controllo di Lync Server

Nei casi in cui è necessario elaborare molti numeri di telefono, uno script personalizzato sviluppato dall'organizzazione rappresenta la scelta più appropriata. A seconda della modalità con cui l'organizzazione rappresenta i numeri di telefono in Servizi di dominio Active Directory, può accadere che lo script debba normalizzare i numeri di telefono primari in base al formato E.164 prima di copiarli nell'attributo **msRTCSIP-line**.

  - Se l'organizzazione gestisce tutti i numeri di telefono in un unico formato in Servizi di dominio Active Directory e se tale formato è E.164, è necessario utilizzare lo script solo per scrivere ogni numero di telefono primario nell'attributo **msRTCSIP-line**.

  - Se l'organizzazione gestisce tutti i numeri di telefono in un unico formato in Servizi di dominio Active Directory, ma tale formato non è E.164, è necessario utilizzare lo script per definire una regola di normalizzazione appropriata in modo da convertire i numeri di telefono primari dal formato esistente in E.164 prima di scriverli nell'attributo **msRTCSIP-line**.

  - Se l'organizzazione non adotta un formato standard per i numeri di telefono in Servizi di dominio Active Directory, è necessario utilizzare lo script per definire le regole di normalizzazione appropriate per convertire i numeri di telefono primari dai diversi formati in un formato conforme a E.164 prima di scriverli nell'attributo **msRTCSIP-line**.

Lo script dovrà inoltre aggiungere il prefisso **Tel:** ai numeri primari prima di scriverli nell'attributo **msRTCSIP-line**.

Il formato previsto del numero specificato in questo attributo è il seguente:

  - Tel:+14255550100;ext=50100.

  - Tel:5550100 (per i numeri di interno univoci a livello aziendale)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>La normalizzazione eseguita dal servizio Rubrica (ABS) non sostituisce né elimina in altro modo la necessità di normalizzare il numero di telefono primario di ogni utente in Servizi di dominio Active Directory. ABS infatti non dispone dell'accesso a Servizi di dominio Active Directory e pertanto non può copiare i numeri primari nell'attributo <strong>msRTCSIP-line</strong>.</td>
    </tr>
    </tbody>
    </table>


## Passaggio 2. Abilitare gli utenti per VoIP aziendale

Oltre a identificare gli utenti da abilitare, per completare questo passaggio non sono necessarie attività di pianificazione particolari.

## Passaggio 3. Preparare i dial plan per gli utenti.

Senza dial plan, gli utenti abilitati per VoIP aziendale non sono in grado di effettuare chiamate verso la rete PSTN. Per dial plan si intende un set denominato di regole di normalizzazione che consente di convertire i numeri di telefono relativi a una località, a un utente o a un oggetto contatto specifico in un unico formato standard (E.164) ai fini dell'autorizzazione del telefono e del routing della chiamata. Le regole di normalizzazione definiscono la modalità di instradamento dei numeri di telefono espressi in diversi formati per ogni località, utente o oggetto contatto specificato.

Per informazioni sulla preparazione di dial plan, vedere [Dial plan e regole di normalizzazione in Lync Server 2013](lync-server-2013-dial-plans-and-normalization-rules.md).

## Passaggio 4. Pianificare i criteri vocali degli utenti

Le impostazioni utente relative alla classe di servizio in un sistema PBX legacy, ad esempio il diritto di effettuare chiamate interurbane o internazionali dai telefoni dell'azienda, devono essere configurate come criteri VoIP per gli utenti trasferiti in VoIP aziendale. Per i dettagli sulla pianificazione e la creazione di criteri per VoIP aziendale, vedere [Criteri vocali in Lync Server 2013](lync-server-2013-voice-policies.md).

## Passaggio 5. Pianificare le route delle chiamate in uscita

Le route delle chiamate specificano come devono essere gestite in Lync Server le chiamate in uscita effettuate da utenti di VoIP aziendale. Quando un utente compone un numero, il server, se necessario, normalizza la stringa di composizione al formato E.164 e tenta di associarla a un URI SIP. Se il server non riesce a effettuare l'associazione, applica la logica di routing delle chiamate in uscita in base al numero. Il passaggio finale della definizione della logica consiste nel creare una route di chiamata denominata separata per ogni insieme di numeri di telefono di destinazione elencati in ogni dial plan.

Per i dettagli sulla pianificazione di route delle chiamate, vedere [Route vocali in Lync Server 2013](lync-server-2013-voice-routes.md).

## Passaggio 6. Configurare il sistema PBX o il trunk SIP per il reinstradamento delle chiamate degli utenti abilitati per VoIP aziendale

Dopo il trasferimento, gli utenti precedentemente ospitati in un sistema PBX tradizionale o che usufruivano di una connessione trunk SIP a un provider di servizi di telefonia Internet (ITSP, Internet Telephony Service Provider) mantengono lo stesso numero di telefono. L'unico requisito è che dopo il trasferimento il sistema PBX o il trunk SIP venga riconfigurato per instradare le chiamate per utenti di VoIP aziendale al Mediation Server.

## Passaggio 7. Trasferire gli utenti al servizio Messaggistica unificata di Exchange (operazione consigliata).

Il passaggio degli utenti al servizio Messaggistica unificata di Exchange è costituito dalle seguenti attività:

  - Configurazione della collaborazione tra il servizio Messaggistica unificata di Exchange e Lync Server.

  - Abilitazione degli utenti per il risponditore automatico del servizio Messaggistica unificata di Exchange e per Outlook Voice Access. Questa attività viene eseguita nel server di Messaggistica unificata di Exchange. Per informazioni dettagliate, vedere la libreria TechNet di Exchange Server 2010 all'indirizzo [http://go.microsoft.com/fwlink/p/?linkID=139372](http://go.microsoft.com/fwlink/p/?linkid=139372).

