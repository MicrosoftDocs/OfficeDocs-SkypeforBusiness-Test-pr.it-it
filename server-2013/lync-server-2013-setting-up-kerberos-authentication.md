---
title: "Lync Server 2013: Configurazione dell'autenticazione Kerberos"
TOCTitle: Configurazione dell'autenticazione Kerberos
ms:assetid: dd8009ef-6265-4cc0-b2c7-e474cd1f4b09
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398976(v=OCS.15)
ms:contentKeyID: 49302208
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'autenticazione Kerberos in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Lync Server 2013 supporta l'autenticazione NTLM e Kerberos per i servizi Web. In Office Communications Server 2007 e Office Communications Server 2007 R2 vengono utilizzati gli account predefiniti RTCComponentService e RTCService come account utente per l'esecuzione del pool di applicazioni di servizi Web, consentendo di assegnare un nome dell'entità servizio (SPN, Service Principal Name) agli account utente che agisca da entità di autenticazione. In Lync Server viene utilizzato NetworkService per l'esecuzione di servizi Web, a cui non è possibile assegnare nomi SPN.

Per risolvere il problema della mancanza di oggetti di Active Directory che contengano i nomi SPN, nel Pannello di controllo di Lync Server è possibile utilizzare gli oggetti account computer a questo scopo. Gli oggetti account computer possono contenere i nomi SPN e non sono soggetti a scadenza della password, un problema associato all'utilizzo degli account utente nelle versioni precedenti.

Per configurare gli oggetti computer per fornire l'autenticazione Kerberos, utilizzare i cmdlet di Windows PowerShell.

## Argomenti della sezione

  - [Prerequisiti per abilitare l'autenticazione Kerberos in Lync Server 2013](lync-server-2013-prerequisites-for-enabling-kerberos-authentication.md)

  - [Creare un account di autenticazione Kerberos in Lync Server 2013](lync-server-2013-create-a-kerberos-authentication-account.md)

  - [Assegnare un account di autenticazione Kerberos a un sito in Lync Server 2013](lync-server-2013-assign-a-kerberos-authentication-account-to-a-site.md)

  - [Configurazione delle password degli account di autenticazione Kerberos in Lync Server 2013](lync-server-2013-setting-up-kerberos-authentication-account-passwords.md)

  - [Aggiungere l'autenticazione Kerberos ad altri siti in Lync Server 2013](lync-server-2013-add-kerberos-authentication-to-other-sites.md)

  - [Rimuovere l'autenticazione Kerberos da un sito in Lync Server 2013](lync-server-2013-remove-kerberos-authentication-from-a-site.md)

  - [Verifica e segnalazione dello stato e dell'assegnazione dell'autenticazione Kerberos in Lync Server 2013](lync-server-2013-testing-and-reporting-the-status-and-assignment-of-kerberos-authentication.md)

