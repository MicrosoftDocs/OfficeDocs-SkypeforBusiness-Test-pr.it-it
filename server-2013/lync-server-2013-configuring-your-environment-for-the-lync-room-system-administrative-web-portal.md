---
title: "Lync Server 2013: Config. Amb. per portale Web di ammin. di Lync Room System"
TOCTitle: Configurazione dell'ambiente per il portale Web di amministrazione di Lync Room System
ms:assetid: 1bf3cc55-cfa8-46ee-a8bc-6dab3bff76b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn436325(v=OCS.15)
ms:contentKeyID: 59602747
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'ambiente di Lync Server 2013 per il portale Web di amministrazione di Lync Room System

 

_**Ultima modifica dell'argomento:** 2014-05-22_

Per usare il portale Web di amministrazione di Lync Room System (LRS) è necessario installare o configurare i prerequisiti seguenti.

> [!IMPORTANT]  
> Se per il server è configurata sia l'autenticazione Kerberos che NTLM e LRS viene eseguito in un computer non aggiunto al dominio, l'autenticazione Kerberos avrà esito negativo e l'utente non potrà vedere lo stato di LRS nel portale amministrativo. Per risolvere il problema, configurare il server con l'autenticazione NTLM oppure sia con l'autenticazione NTLM che TLS-DSK (senza Kerberos) oppure aggiungere il computer LRS al dominio.

1.  Installare Aggiornamenti cumulativi per Lync Server 2013: luglio 2013 nella topologia di Lync Server.
    
    Per ottenere l'aggiornamento o vedere cosa include, vedere [Aggiornamenti per Lync Server 2013](http://go.microsoft.com/fwlink/p/?linkid=323959).

2.  Creare un utente di Active Directory abilitato per SIP.
    
    Il portale Web di amministrazione di LRS usa queste credenziali per inviare richieste di informazioni a Lync Server. Il nome utente consigliato è LRSApp.

3.  Creare un gruppo di sicurezza Active Directory con nome LRSSupportAdminGroup.
    
    Creare il gruppo con Ambito del gruppo impostato su Globale e Tipo gruppo impostato su Sicurezza. Gli utenti abilitati per SIP aggiunti a questo gruppo saranno autorizzati a vedere l'elenco di sale ed eseguire determinati comandi, ad esempio raccogliere log.

4.  Creare un gruppo di sicurezza Active Directory con nome LRSFullAccessAdminGroup.
    
    Creare il gruppo con Ambito del gruppo impostato su Globale e Tipo gruppo impostato su Sicurezza. Gli utenti abilitati per SIP aggiunti a questo gruppo sono autorizzati a usare tutte le funzionalità del portale di amministrazione.
    
     
    
    ![Elenco dei gruppi di amministratori con il ruolo gruppo di sicurezza](images/Dn436325.5d432819-a2e2-452c-bc2a-5d4ee79d8c33(OCS.15).png "Elenco dei gruppi di amministratori con il ruolo gruppo di sicurezza")  
    
     

5.  Aggiungere LRSFullAccessAdminGroup come membro di LRSSupportAdminGroup.
    
    ![Pagina dei membri del gruppo LRSSupportAdminGroup](images/Dn436325.91a4a28a-cacf-4ef6-aac1-915ec41c9648(OCS.15).png "Pagina dei membri del gruppo LRSSupportAdminGroup")  
    
     

6.  Creare un utente di Active Directory abilitato per SIP con nome LRSSupport. Aggiungere questo utente a LRSSupportAdminGroup.
    
    ![Pagina dei membri del gruppo LRSSupportAdminGroup](images/Dn436325.7638055d-22ac-4909-914d-1966f5623909(OCS.15).png "Pagina dei membri del gruppo LRSSupportAdminGroup")  
    
     

7.  Installare ASP.NET MVC 4 per Visual Studio 2010 SP1 e Visual Web Developer 2010 SP1, disponibile nell'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=323967](http://go.microsoft.com/fwlink/p/?linkid=323967).

