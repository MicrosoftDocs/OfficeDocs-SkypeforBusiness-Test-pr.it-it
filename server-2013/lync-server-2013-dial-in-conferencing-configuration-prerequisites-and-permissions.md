---
title: 'Lync Server 2013: Prerequisiti e autorizzazioni per la configurazione delle conferenze telefoniche con accesso esterno'
TOCTitle: Prerequisiti e autorizzazioni per la configurazione delle conferenze telefoniche con accesso esterno
ms:assetid: b3b251e5-78ac-44a2-8c36-2a061c9b2314
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412865(v=OCS.15)
ms:contentKeyID: 49301718
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti e autorizzazioni per la configurazione delle conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-20_

La funzionalità di conferenza telefonica con accesso esterno è un componente facoltativo del carico di lavoro del Servizio di conferenza di Lync Server 2013. I componenti che devono essere installati prima di poter configurare le conferenze telefoniche con accesso esterno vengono distribuiti quando si utilizza Generatore di topologie per progettare la topologia e quindi impostare il pool Front End o il server Standard Edition. In questo argomento vengono descritte le operazioni da eseguire prima di poter configurare le conferenze telefoniche con accesso esterno.

In questa sezione si presuppone che siano state lette le sezioni sulla pianificazione correlate al carico di lavoro per le conferenze e in particolare alle conferenze telefoniche con accesso esterno.

## Prerequisiti per la configurazione delle conferenze telefoniche con accesso esterno

Per le conferenze telefoniche con accesso esterno sono necessari i componenti di Lync Server 2013 seguenti:

  - Servizi per applicazioni per comunicazioni unificate, noti come *servizio applicazione* )

  - applicazione Operatore Conferenza

  - applicazione Annuncio conferenza

  - Pagina Web Impostazioni Conferenza telefonica con accesso esterno

  - Almeno un Mediation Server di Lync Server 2013 e almeno un gateway PSTN

Questi componenti vengono distribuiti quando si utilizza Generatore di topologie per definire e pubblicare la topologia e quindi si distribuisce un pool Front End o un server Standard Edition. Se si intende distribuire VoIP aziendale, è necessario distribuire questa funzionalità prima di configurare le conferenze telefoniche con accesso esterno. Se non è prevista la distribuzione di VoIP aziendale, è possibile distribuire un Mediation Server e un gateway PSTN (Public Switched Telephone Network) quando si distribuisce il pool Front End o il server Standard Edition.


> [!NOTE]
> Se si esegue l'aggiornamento da Office Communications Server 2007 R2 a Lync Server 2013, distribuire le funzionalità di conferenza telefonica con accesso esterno in tutti i pool che si prevede di utilizzare per ospitare conferenze di Lync Server 2013. Per informazioni dettagliate sulla migrazione delle conferenze telefoniche con accesso esterno, vedere <A href="migration-from-office-communications-server-2007-r2-to-lync-server-2013.md">Migrazione da Office Communications Server 2007 R2 a Lync Server 2013</A>.



In questa sezione si presuppone che siano già state eseguite le operazioni seguenti:

  - Applicazione degli aggiornamenti più recenti all'ambiente Office Communications Server 2007 R2, in caso di migrazione in Lync Server 2013.

  - Utilizzo di Generatore di topologie per progettare e configurare la topologia. Durante la definizione del carico di lavoro per il Servizio di conferenza, è necessario avere selezionato l'opzione per le conferenze telefoniche con accesso esterno. Per informazioni dettagliate sulla definizione della topologia, vedere [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md) nella documentazione relativa alla distribuzione.

  - Pubblicazione della topologia e impostazione del pool Front End e del server Standard Edition. Per informazioni dettagliate sulla pubblicazione della topologia e sull'installazione di Lync Server 2013, vedere [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md) nella documentazione relativa alla distribuzione.
    

    > [!NOTE]
    > Quando si installa la topologia pubblicata, la pagina Web Impostazioni conferenza telefonica con accesso esterno viene installata nel Front End Server o nel server Standard Edition come parte dei servizi Web.

    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si modifica il percorso per l'archivio file in Generatore di topologie dopo la distribuzione di Lync Server 2013, è necessario riavviare le applicazioni Operatore Conferenza e Annuncio conferenza in modo che che venga utilizzato il nuovo percorso.</td>
    </tr>
    </tbody>
    </table>


  - Distribuzione di VoIP aziendale. Se VoIP aziendale non è stato incluso nella distribuzione, si è scelto di collocare un Mediation Server nell'Enterprise Edition Front End Server o nel server Standard Edition oppure è stato distribuito un Mediation Server autonomo e un gateway PSTN. Per informazioni dettagliate sulla distribuzione di VoIP aziendale, vedere [Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md) nella documentazione relativa alla distribuzione. Per informazioni dettagliate sull'installazione di un Mediation Server autonomo e un gateway PSTN, vedere [Distribuzione di Mediation Server e definizione di peer in Lync Server 2013](lync-server-2013-deploying-mediation-servers-and-defining-peers.md) nella documentazione relativa alla distribuzione.

Il diagramma di flusso seguente mostra i passaggi da eseguire prima di poter configurare le conferenze telefoniche con accesso esterno e i passaggi per eseguire la configurazione delle conferenze telefoniche con accesso esterno.

**Distribuzione delle conferenze telefoniche con accesso esterno**

![Diagramma di flusso per la distribuzione delle conferenze telefoniche con accesso esterno](images/Gg412865.fde8c246-b5ed-4323-a6e7-af1983a5ec86(OCS.15).jpg "Diagramma di flusso per la distribuzione delle conferenze telefoniche con accesso esterno")

## Autorizzazioni per le conferenze telefoniche con accesso esterno

Per configurare le conferenze telefoniche con accesso esterno, è necessario utilizzare gli strumenti di amministrazione seguenti:

  - Pannello di controllo di Lync Server 2013

  - Lync Server Management Shell

Questi strumenti di amministrazione consentono di configurare le impostazioni per le conferenze telefoniche con accesso esterno, nonché i dial plan, i criteri e le altre impostazioni necessarie per questo tipo di conferenze.

Per configurare le conferenze telefoniche con accesso esterno sono necessari i ruoli amministrativi seguenti, a seconda dell'attività:

  - **CsVoiceAdministrator**   Questo ruolo amministrativo è autorizzato a creare, configurare e gestire le impostazioni e i criteri correlati alle funzionalità vocali.

  - **CsUserAdministrator**   Questo ruolo amministrativo è autorizzato ad abilitare e disabilitare gli utenti per Lync Server, nonché ad assegnare agli utenti i criteri esistenti, ad esempio i criteri di conferenza e i criteri PIN.

  - **CsAdministrator**   Questo ruolo amministrativo è autorizzato a eseguire tutte le attività dei ruoli CsVoiceAdministrator e CsUserAdministrator.

## Vedere anche

#### Concetti

[Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md)

