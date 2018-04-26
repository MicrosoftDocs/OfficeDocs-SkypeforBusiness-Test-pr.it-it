---
title: Concetti comuni sulle conferenze
TOCTitle: Concetti comuni sulle conferenze
ms:assetid: a21d4987-1c0a-44c8-8a39-9c17ffb57f3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688158(v=OCS.15)
ms:contentKeyID: 49887683
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Concetti comuni sulle conferenze

 

_**Ultima modifica dell'argomento:** 2012-09-19_

A tutti i tipi di conferenze sono comuni diversi concetti, illustrati nelle sezioni riportate di seguito.

## Criteri e gestione della larghezza di banda

Lync Server 2013 consente agli amministratori di impostare criteri per i tipi di riunioni che gli utenti possono organizzare. In questo modo è possibile applicare i criteri dell'organizzazione e controllare l'utilizzo della larghezza di banda. È possibile definire un'ampia gamma di criteri di riunione e assegnarli a singoli utenti e gruppi di utenti. È inoltre possibile impostare criteri che controllano le conversazioni peer-to-peer. Per informazioni dettagliate sull'impostazione di criteri di conferenza, vedere [Criteri conferenza in Lync Server 2013](lync-server-2013-conferencing-policies.md) nella documentazione relativa alle operazioni. Per informazioni dettagliate sulla gestione della larghezza di banda, vedere [Panoramica del controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-overview-of-call-admission-control.md) e [Configurazione della larghezza di banda video in Lync Server 2013](lync-server-2013-configuring-video-bandwidth.md).

## Funzionalità di archiviazione e conformità

Lync Server 2013 include funzionalità utili nel caso l'organizzazione sia tenuta a rispettare regolamentazioni di conformità. È possibile utilizzare le funzionalità di archiviazione per archiviare il contenuto presentato nelle riunioni, nonché il contenuto delle conversazioni e delle conferenze istantanee. Per informazioni dettagliate, vedere [Pianificazione dell'archiviazione in Lync Server 2013](lync-server-2013-planning-for-archiving.md) nella documentazione relativa alla pianificazione. È possibile utilizzare le funzionalità di conformità del server di Chat persistente per archiviare conversazioni basate su un argomento che coinvolgono più persone e che vengono salvate in modo permanente. Per informazioni dettagliate, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione.

## Funzionalità di monitoraggio

La funzionalità Monitoring Server consente di acquisire le registrazioni dettagli chiamata, che possono essere utilizzate per tenere traccia degli utenti che parlano con altri utenti utilizzando Lync Server 2013. Per informazioni dettagliate sulla distribuzione e sulla configurazione del monitoraggio, vedere [Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md).

## Consentire la partecipazione esterna alle conferenze

È possibile aumentare notevolmente i vantaggi dell'investimento in strumenti per le conferenze di Lync Server 2013 consentendo agli utenti esterni di partecipare alle conferenze anche dietro invito. Gli utenti esterni possono essere:

  - **Utenti remoti**   Utenti dell'organizzazione che lavorano all'esterno dei firewall utilizzando computer portatili o altri dispositivi di Lync Server 2013.

  - **Utenti federati**   Utenti di società con cui si collabora, che utilizzano Lync Server 2013. Per consentire agli utenti di mettersi facilmente in contatto con questi utenti, si creano relazioni federate con le relative società.

  - **Utenti anonimi**   Qualsiasi altro utente esterno invitato in modo specifico da uno degli utenti interni a partecipare a una conferenza specifica. L'organizzatore di una riunione può inviare un invito tramite posta elettronica per una conferenza a un utente esterno. Il messaggio di posta elettronica include un collegamento su cui l'utente esterno può fare clic per partecipare alla conferenza.

Per abilitare qualsiasi scenario tra questi oppure tutti, è necessario distribuire un server perimetrale per consentire comunicazioni sicure tra la distribuzione di Lync Server 2013 e gli utenti esterni. La soluzione Lync Server 2013 con server perimetrali offre servizi multimediali di qualità superiore rispetto ad altre soluzioni, come una rete VPN. Per ulteriori informazioni, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md).

Inoltre, indipendentemente dal fatto che si decida o meno di distribuire server perimetrali, è possibile consentire agli utenti (interni o esterni all'organizzazione) di partecipare ad audioconferenze in locale chiamando da telefoni PSTN standard. Ciò è possibile con la distribuzione della funzionalità per conferenze telefoniche con accesso esterno di Lync Server 2013.

## Compatibilità tra tipi di riunioni e versioni client

Se esistono esigenze di interoperabilità tra Lync Server 2013 e versioni precedenti di Office Communications Server e relativi client, è necessario tenere conto dei problemi seguenti:

  - Gli utenti che utilizzano Lync Server 2013 non possono pianificare conferenze di Live Meeting o modificare eventuali riunioni di questo tipo di cui è stata eseguita la migrazione.

  - Gli utenti che utilizzano Lync Server 2013 e devono partecipare a conferenze di Live Meeting ospitate in server che eseguono Office Communications Server 2007 R2 devono avere il client Live Meeting installato nei computer (oltre a Lync Server 2013) per partecipare a queste riunioni.

  - Quando viene eseguita la migrazione delle conferenze di Live Meeting in Lync Server 2013, il contenuto delle riunioni non viene incluso nella migrazione e dovrà essere caricato di nuovo, se è necessario.

