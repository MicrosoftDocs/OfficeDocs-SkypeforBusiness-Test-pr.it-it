---
title: Configurare regole per il PIN della conferenza telefonica con accesso esterno in Lync Server 2013
TOCTitle: Configurare regole per il PIN della conferenza telefonica con accesso esterno in Lync Server 2013
ms:assetid: 27b79fb1-e2dc-4f71-bc82-b6eb61be2b16
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520967(v=OCS.15)
ms:contentKeyID: 49299986
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare regole per il PIN della conferenza telefonica con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-19_

Gli utenti di Lync Server 2013 che nell'organizzazione dispongono di credenziali di Servizi di dominio Active Directory possono partecipare alle conferenze telefoniche con accesso esterno come utenti autenticati usando un PIN. Il criterio PIN definisce le regole per il funzionamento dei PIN per le conferenze telefoniche con accesso esterno.

È possibile creare un nuovo criterio PIN se si desidera un criterio specifico da applicare a un sito o a un determinato gruppo di utenti. Se si desidera utilizzare lo stesso criterio PIN per l'intera organizzazione, è possibile utilizzare il criterio PIN globale e modificarlo in base alle esigenze. I criteri PIN si applicano agli utenti partendo dall'ambito più limitato fino all'ambito più esteso. Se si assegna a un utente un criterio PIN a livello utente, tali impostazioni avranno la priorità. Se invece non si assegna un criterio utente, si applicherà il criterio PIN a livello di sito, se esistente. Se non si applica alcun criterio utente o sito, le impostazioni predefinite verranno fornite dal criterio PIN globale.

## Argomenti della sezione

  - [Modifica delle impostazioni predefinite dei PIN per le conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-modify-the-default-dial-in-conferencing-pin-settings.md)

  - [Creare o modificare le impostazioni del PIN di conferenza telefonica con accesso esterno in Lync Server 2013 per un sito o un gruppo di utenti](lync-server-2013-create-or-modify-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md)

  - [Eliminare le impostazioni del PIN di conferenza telefonica con accesso esterno per un sito o un gruppo di utenti](lync-server-2013-delete-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md)

