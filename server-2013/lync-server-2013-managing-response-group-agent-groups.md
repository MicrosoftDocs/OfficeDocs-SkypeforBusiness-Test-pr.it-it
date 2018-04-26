---
title: Gestione di gruppi di agenti per Response Group
TOCTitle: Gestione di gruppi di agenti per Response Group
ms:assetid: 36084cdc-38f1-4c45-922f-f81c7e86210c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520976(v=OCS.15)
ms:contentKeyID: 49300153
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione di gruppi di agenti per Response Group

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Un gruppo di agenti è un gruppo di persone che hanno il compito di rispondere alle chiamate di un Response Group. Quando si crea un gruppo di agenti, è necessario selezionare gli agenti assegnati al gruppo e specificare ulteriori impostazioni per il gruppo, ad esempio il metodo di routing e se un agente possa o meno accedere al gruppo e disconnettersi da esso.


> [!NOTE]
> Per poter essere aggiunti a gruppi di agenti, gli utenti devono essere abilitati per VoIP aziendale. Per informazioni dettagliate su come abilitare un utente per VoIP aziendale, vedere <A href="lync-server-2013-enable-users-for-enterprise-voice.md">Abilitare gli utenti per VoIP aziendale in Lync Server 2013</A>.




> [!NOTE]
> Solo gli utenti che si trovano in locale possono essere agenti. Se un agente viene spostato da in locale a online, le chiamate del Response Group non gli verranno instradate.



Un agente che deve accedere al gruppo e disconnettersi, operazione diversa dall'accesso o la disconnessione in Lync Server, è denominato *agente formale*. Gli agenti formali devono aver effettuato l'accesso al gruppo per poter ricevere le chiamate instradate a tale gruppo. Questo requisito può rivelarsi utile per gli agenti che rispondono solo a tempo parziale alle chiamate provenienti dal gruppo. Gli agenti formali accedono ai gruppi e si disconnettono scegliendo una voce di menu in Lync 2013 per aprire il browser Windows Internet Explorer e visualizzare una console su pagina Web.

Un agente che non deve accedere al gruppo o disconnettersi è denominato *agente informale*. L'accesso degli agenti informali al gruppo viene eseguito automaticamente con l'accesso a Lync Server. Questi agenti non possono disconnettersi dal gruppo.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Quando si assegnano utenti come agenti del Response Group, informarli che, se è abilitata la modalità Privacy, dovranno cercare i contatti &quot;RGS Presence Watcher&quot; e aggiungerli all'elenco contatti. Gli agenti con modalità privacy abilitata ma nel cui elenco contatti non sono presenti contatti &quot;RGS Presence Watcher&quot; non possono ricevere chiamate per il Response Group. Questa restrizione non si applica agli agenti non in modalità privacy.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Creare o modificare un gruppo di agenti in Lync Server 2013](lync-server-2013-create-or-modify-an-agent-group.md)

  - [Eliminare un gruppo di agenti](lync-server-2013-delete-an-agent-group.md)

