---
title: 'Lync Server 2013: Query del database di Chat persistente di esempio'
TOCTitle: Query del database di Chat persistente di esempio
ms:assetid: 545b1a93-9758-4344-98cc-aa0e559d494f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558649(v=OCS.15)
ms:contentKeyID: 49300597
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Query del database di Chat persistente di esempio per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

In questa sezione sono incluse query di esempio per il database di Chat persistente.

Utilizzare l'esempio seguente per ottenere un elenco delle chat Chat persistente dopo una certa data.

    SELECT nodeName as ChatRoom, COUNT(*) as ChatMessages
      FROM tblChat, tblNode
      WHERE channelId = nodeID AND dbo.fnTicksToDate(chatDate) > '1/1/2011'
      GROUP BY nodeName
      ORDER BY ChatMessages DESC

Utilizzare l'esempio seguente per ottenere un elenco degli utenti più attivi dopo una certa data.

    SELECT prinName as Name, count(*) as ChatMessages
      FROM tblChat, tblPrincipal
      WHERE prinID = userId AND dbo.fnTicksToDate(chatDate) > '1/1/2011'
      GROUP BY prinName
      ORDER BY ChatMessages DESC

Utilizzare l'esempio seguente per ottenere un elenco di tutti gli utenti che hanno inviato un messaggio contenente "Hello World".

    SELECT nodeName as ChatRoom, prinName as Name, content as Message
      FROM tblChat, tblNode, tblPrincipal
      WHERE channelId = nodeID AND userId = prinID AND content like '%Hello World%'

Utilizzare l'esempio seguente per ottenere un elenco delle appartenenze a gruppi per una certa entità.

    SELECT prinName as Name    
      FROM tblPrincipalAffiliations as pa, tblPrincipal
      where principalID = 7 and affiliationID = prinID

Utilizzare l'esempio seguente per ottenere un elenco di tutte le chat di cui è membro diretto l'utente Jane Dow.

    SELECT DISTINCT nodeName as ChatRoom, prinName as Name          
      FROM tblPrincipalRole, tblPrincipal, tblNode
      WHERE  prinRoleNodeID = nodeID AND prinRolePrinID = prinID AND prinName = 'Jane Dow'

Utilizzare l'esempio seguente per ottenere un elenco degli inviti ricevuti da un utente.

    SELECT prinName
          ,nodeName
          ,invID   
          ,createdOn
      FROM tblPrincipalInvites as inv, tblPrincipal as p, tblNode as n
      where inv.prinID = 5 AND inv.prinID = p.prinID and inv.nodeID = n.nodeID
      ORDER BY invID DESC

