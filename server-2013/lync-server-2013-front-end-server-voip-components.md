---
title: 'Lync Server 2013: Componenti VoIP per Front End Server'
TOCTitle: Componenti VoIP per Front End Server
ms:assetid: 310e81a7-da45-47d4-95d0-92837e386502
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425812(v=OCS.15)
ms:contentKeyID: 49300090
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti VoIP per Front End Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

I componenti VoIP disponibili nei Front End Server sono:

  - Servizio di conversione

  - Componente di routing in ingresso

  - Componente di routing in uscita

  - Componente di routing per Messaggistica unificata di Exchange

  - Componente di routing tra cluster

  - [Componente Mediation Server in Lync Server 2013](lync-server-2013-mediation-server-component.md)

## Servizio di conversione

Il servizio di conversione è il componente server responsabile della conversione di un numero composto nel formato E.164 o in un altro formato, in base alle regole di normalizzazione definite dall'amministratore. Questo servizio può eseguire la conversione in formati diversi dal formato E.164 se nell'organizzazione viene utilizzato un sistema di numerazione privato oppure un gateway o un PBX che non supporta il formato E.164.

## Componente di routing in ingresso

Il componente di routing in ingresso gestisce le chiamate in arrivo principalmente in base alle preferenze specificate dagli utenti nei relativi client VoIP aziendale. Consente inoltre di utilizzare le funzionalità di chiamata ai delegati e di squillo simultaneo, se configurate dall'utente. Gli utenti possono ad esempio specificare se le chiamate senza risposta devono essere inoltrate o semplicemente registrate a scopo di notifica. Se è abilitato l'inoltro di chiamata, gli utenti possono specificare se le chiamate senza risposta devono essere inoltrate a un altro numero oppure a un server di Messaggistica unificata di Exchange configurato per offrire servizi di risponditore automatico. Per impostazione predefinita, il componente di routing in ingresso viene installato in tutti i server server Standard Edition e Front End Server.

## Componente di routing in uscita

Il componente di routing in uscita instrada le chiamate a destinazioni PBX o PSTN. Applica ai chiamanti le regole di autorizzazione per le chiamate, secondo quanto definito dal criterio vocale dell'utente, e determina il gateway PSTN ottimale per il routing di ogni chiamata. Per impostazione predefinita, il componente di routing in uscita viene installato in tutti i server server Standard Edition e Front End Server.

La logica di routing utilizzata dal componente di routing in uscita viene in buona parte configurata dagli amministratori di rete o di telefonia in base ai requisiti dell'organizzazione.

## Componente di routing per Messaggistica unificata di Exchange

Il componente di routing per Messaggistica unificata di Exchange gestisce il routing tra Lync Server e i server che eseguono Messaggistica unificata di Exchange per integrare Lync Server con le funzionalità di messaggistica unificata.

Il componente di routing per Messaggistica unificata di Exchange gestisce inoltre il rerouting della segreteria telefonica su PSTN se non sono disponibili server di Messaggistica unificata di Exchange. Se si dispone in siti di succursale di utenti VoIP aziendale senza collegamento WAN resiliente a un sito centrale, il Survivable Branch Appliance distribuito nel sito di succursale offre la modalità Survivability per la segreteria telefonica in caso di interruzione della WAN. Quando il collegamento WAN non è disponibile, il Survivable Branch Appliance esegue le operazioni seguenti:

  - Reinstrada le chiamate senza risposta sulla rete PSTN verso il server di Messaggistica unificata di Exchange nel sito centrale

  - Consente a un utente di recuperare i messaggi di segreteria telefonica sulla rete PSTN

  - Accoda le notifiche di chiamate senza risposta e quindi le carica nel server di Messaggistica unificata di Exchange quando viene ripristinato il collegamento WAN

Per abilitare il rerouting della segreteria telefonica, è consigliabile che l'amministratore di Exchange configuri l'operatore automatico di Messaggistica unificata di Exchange in modo da accettare solo i messaggi.

Per informazioni dettagliate su queste funzionalità, vedere rispettivamente [Pianificazione dell'integrazione della messaggistica unificata di Exchange in Lync Server 2013](lync-server-2013-planning-for-exchange-unified-messaging-integration.md) e [Pianificazione della resilienza di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice-resiliency.md).

## Componente di routing tra cluster

Il componente di routing tra cluster è responsabile del routing delle chiamate al pool di registrazione principale del destinatario della chiamata. Se il pool non è disponibile, il componente instrada la chiamata al pool di registrazione di backup del destinatario della chiamata. Se i pool di registrazione principale e di backup del destinatario della chiamata non sono raggiungibili sulla rete IP, il componente di routing tra cluster reinstrada la chiamata sulla rete PSTN al numero di telefono dell'utente.

## Altri componenti di Front End Server necessari per VoIP

Tra gli altri componenti presenti nel Front End Server o nel Server Director che offrono un supporto essenziale per il protocollo VoIP, ma che non sono componenti VoIP, sono inclusi i seguenti:

  - **Servizi utente.** Consente di eseguire la ricerca inversa nel numero di telefono di destinazione per ogni chiamata in arrivo e di associare tale numero all'URI SIP dell'utente di destinazione. Queste informazioni vengono usate dal componente di routing in ingresso per distribuire la chiamata agli endpoint SIP registrati dell'utente. Servizi utente è un componente di base di tutti i Front End Server e Director.

  - **User Replicator.** Estrae i numeri di telefono degli utenti da Servizi di dominio Active Directory e li scrive nelle tabelle del database RTC, da cui sono disponibili per Servizi utente e il server della Rubrica. User Replicator è un componente di base di tutti i Front End Server.

  - **Server della Rubrica.** Fornisce informazioni dell'Elenco indirizzi globale da Servizi di dominio Active Directory ai client Lync Server. Recupera inoltre informazioni sugli utenti e sui contatti dal database RTC, scrive le informazioni nei file della Rubrica e archivia quindi i file in una cartella condivisa da dove vengono scaricati dai client Lync. Il server della Rubrica scrive le informazioni nel database RTCAb, che viene usato dal servizio query Web della Rubrica per rispondere alle query di ricerca degli utenti da Microsoft Lync 2010 Mobile. Consente di normalizzare facoltativamente i numeri di telefono di utenti Enterprise scritti nel database RTC allo scopo di effettuare il provisioning dei contatti utente in Lync. Il servizio Rubrica viene installato per impostazione predefinita in tutti i Front End Server. Il servizio query Web della Rubrica viene installato per impostazione predefinita con i servizi Web in ogni Front End Server.

