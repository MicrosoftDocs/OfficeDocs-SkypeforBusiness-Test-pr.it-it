---
title: Autenticazione utenti e client per Lync Server 2013
TOCTitle: Autenticazione utenti e client per Lync Server 2013
ms:assetid: 77f4b62a-f75c-424d-8f02-a6519090015d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481132(v=OCS.15)
ms:contentKeyID: 59679242
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Autenticazione utenti e client per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-11_

Un utente viene considerato attendibile quando le relative credenziali sono state autenticate da un server attendibile in Microsoft Lync Server 2013. In genere tale server è un server Standard Edition, un Enterprise EditionFront End Server o un server Director. Lync Server 2013 utilizza Servizi di dominio Active Directory come unico repository back-end attendibile per le credenziali dell'utente.

L'autenticazione avviene attraverso l'invio delle credenziali utente a un server attendibile. Lync Server 2013 utilizza i seguenti protocolli di autenticazione, a seconda dello stato e della posizione dell'utente.

  - **Protocollo di sicurezza MIT Kerberos versione 5** per utenti interni con credenziali Active Directory. Kerberos richiede la connettività client a Servizi di dominio Active Directory, per questo motivo non può essere utilizzato per l'autenticazione di client esterni al firewall aziendale.

  - **Protocollo NTLM** per utenti con credenziali Active Directory che eseguono la connessione da un endpoint esterno al firewall aziendale. Il servizio Access Edge trasmette le richieste di accesso a un server Director, se presente, o un Front End Server per l'autenticazione. Il servizio Access Edge non esegue alcuna autenticazione.
    

    > [!NOTE]
    > Il protocollo NTLM offre una protezione dagli attacchi inferiore rispetto a Kerberos, pertanto alcune organizzazioni riducono al minimo l'utilizzo di NTLM. Di conseguenza, l'accesso a Lync Server 2013 potrebbe essere limitato ai client o agli utenti interni connessi tramite una VPN o una connessione DirectAccess.



  - **Protocollo Digest** per utenti anonimi. Gli utenti anonimi sono utenti esterni che non dispongono di credenziali Active Directory riconosciute, ma che sono stati invitati a una conferenza locale e possiedono una chiave di conferenza valida. L'autenticazione Digest non viene utilizzata per altre interazioni con i client.

L'autenticazione di Lync Server 2013 si divide in due fasi:

1.  Viene stabilita un'associazione di sicurezza tra il client e il server.

2.  Il client e il server utilizzano l'associazione di sicurezza esistente per contrassegnare i messaggi inviati e controllare i messaggi ricevuti. Se l'autenticazione è abilitata nel server, i messaggi non autenticati inviati da un client non vengono accettati.

L'attendibilità utente è associata a ogni messaggio proveniente da un utente, non all'identità utente stessa. Il server verifica la presenza di credenziali utente valide per ogni messaggio. Se le credenziali dell'utente sono valide, il messaggio viene ritenuto attendibile non solo dal primo server che lo riceve ma anche da tutti gli altri server nel cloud di server attendibili.

Gli utenti con credenziali emesse da un partner federato vengono considerati attendibili, ma è possibile che a causa di ulteriori limitazioni non dispongano dell'intera gamma di privilegi concessi agli utenti interni.

Anche i protocolli ICE e TURN utilizzano la verifica Digest come descritto nella specifica IETF TURN RFC.

I certificati client forniscono agli utenti un modo alternativo per ottenere l'autenticazione da Lync Server 2013. Invece di fornire un nome utente e una password, gli utenti dispongono di un certificato e della chiave privata corrispondente al certificato richiesto per risolvere una verifica di crittografia. Tale certificato deve presentare un nome soggetto o un nome alternativo del soggetto che identifichi l'utente e deve essere emesso da una CA radice ritenuta attendibile dai server che eseguono Lync Server 2013. Deve inoltre trovarsi all'interno del periodo di validità del certificato e non essere stato revocato. Per ottenere l'autenticazione, gli utenti devono semplicemente digitare un PIN. I certificati sono particolarmente utili per i telefoni e altri dispositivi che eseguono Microsoft Lync 2013 Phone Edition, dove l'immissione di un nome utente e/o una password è meno agevole.

