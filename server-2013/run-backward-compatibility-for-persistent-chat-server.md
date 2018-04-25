---
title: Eseguire la compatibilità con le versioni precedenti per il server Chat persistente
TOCTitle: Eseguire la compatibilità con le versioni precedenti per il server Chat persistente
ms:assetid: 53f1a706-3104-4a94-8b4e-8badd9a066d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204901(v=OCS.15)
ms:contentKeyID: 49300611
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la compatibilità con le versioni precedenti per il server Chat persistente

 

_**Ultima modifica dell'argomento:** 2013-02-21_

L'endpoint server Chat persistente di Lync Server 2013 consente di creare un URL semplice che punti a un pool di server Chat persistente. Questa caratteristica è utile per i client legacy ( Group Chat Server di Microsoft Office Communications Server 2007 R2 o Lync Server 2010, Group Chat). Gli utenti, infatti, possono immettere un URL semplice nella configurazione manuale per puntare i client legacy a un computer che esegue Chat persistente di Lync 2013. Questo endpoint non è usato da Chat persistente ed è necessario solo per i client legacy. È provvisoriamente utile durante i periodi di passaggio, ad esempio durante la migrazione di chat, se i client Lync 2013 non sono stati distribuiti in tutta l'organizzazione. Gli utenti che eseguono Group Chat di Lync 2010 (client) potranno ancora connettersi al server back-end di server Chat persistente.

Non è necessario creare più endpoint server Chat persistente. Ne basta uno per ogni pool di server Chat persistente. Gli amministratori possono creare più endpoint (uno per pool), ma è possibile configurare i client legacy per la connessione a un solo pool alla volta. Nello scenario abituale o in uno scenario tradizionale la distribuzione legacy comprende un solo pool. Una nuova distribuzione, che in genere esegue la migrazione di questo pool in un nuovo Lync Server 2013, potrebbe aggiungere pool di server Chat persistente aggiuntivi.

Uno scenario di questo tipo in genere segue questo schema:

  - Gli utenti vengono gestiti con un solo pool Lync Server 2010, Group Chat e i client Lync 2010, Group Chat si connettono al pool tramite un utente noto (l'utente predefinito sip:ocschat@ *\<nomeDominio\>* .com o simile). Gli utenti sono utenti Servizi di dominio Active Directory abilitati per SIP. Per ricevere le richieste in arrivo, la registrazione del servizio di ricerca viene eseguita con Servizi di dominio Active Directory.

  - Successivamente si installa server Chat persistente di Lync Server 2013 e un pool di server Chat persistente.

  - In un momento in cui gli utenti sono in genere offline, ad esempio durante il weekend:
    
      - Arrestare Lync Server 2010, Group Chat.
    
      - Eseguire la migrazione dei dati dal pool Lync Server 2010, Group Chat al pool di server Chat persistente di Lync Server 2013 .
    
      - Eliminare l'utente noto da Servizi di dominio Active Directory.
    
      - Creare un nuovo *endpoint legacy* con lo stesso URI SIP dell'utente noto eliminato in precedenza.
    
      - Avviare i server Chat persistente di Lync Server 2013.

  - Gli utenti accedono usando Lync 2010, Group Chat (client) e si connettono ai propri dati senza dover modificare la configurazione.

  - In seguito sarà possibile rimuovere dalla configurazione Lync Server 2010, Group Chat e quindi distribuire server Chat persistente di Lync Server 2013 e installare i nuovi pool di server Chat persistente di Lync Server 2013 .

Per informazioni dettagliate sulla migrazione da Lync Server 2010, Group Chat a server Chat persistente di Lync Server 2013, vedere [Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md).

Per eseguire la compatibilità con le versioni precedenti (per creare un endpoint server Chat persistente che punta a un pool di server Chat persistente, che può essere usato dai client dei pool Group Chat legacy):

    New-CsPersistentChatEndpoint -SipAddress <CO name, ex. persistentchat@contoso.com> -PersistentChatPoolFqdn <pool FQDN, like pcpool.contoso.com>

Configurare quindi i client Chat persistente in modo che usino l'indirizzo SIP come oggetto contatto. L'indirizzo SIP viene creato dal cmdlet **New-CsPersistentChatEndpoint** per un pool di server Chat persistente specifico.

Per aggiungere l'endpoint server Chat persistente tramite interfaccia della riga di comando Windows PowerShell, esaminare l'esempio seguente. In questo caso si configura l'oggetto contatto con il nome "persistentchat" nella topologia "contoso.com", dove il nome di dominio completo (FQDN) del pool è "pcpool.contoso.com":

    New-CsPersistentChatEndpoint -SipAddress sip:persistentchat@contoso.com -PersistentChatPoolFqdn pcpool.contoso.com

## Vedere anche

#### Concetti

[Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)

