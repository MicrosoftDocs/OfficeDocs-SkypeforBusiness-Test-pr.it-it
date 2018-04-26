---
title: 'Lync Server 2013: Creare gruppi di agenti per Response Group'
TOCTitle: Creare gruppi di agenti per Response Group
ms:assetid: 2a80de17-ead0-46e8-8a27-7a4e233dbde0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520969(v=OCS.15)
ms:contentKeyID: 49300013
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare gruppi di agenti per Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-12_

Quando si crea un gruppo di agenti, è necessario selezionare gli agenti assegnati al gruppo e specificare impostazioni aggiuntive per il gruppo, ad esempio il metodo di routing e se un agente possa o meno accedere al gruppo e disconnettervisi.

Un agente che deve accedere al gruppo e disconnettersi, operazione distinta dall'accesso o la disconnessione in Lync Server, è denominato *agente formale* . Gli agenti formali devono aver effettuato l'accesso al gruppo per poter ricevere le chiamate instradate a tale gruppo. Questo requisito può rivelarsi utile per gli agenti che rispondono alle chiamate provenienti dal gruppo a tempo parziale. Gli agenti formali accedono ai gruppi e si disconnettono scegliendo una voce di menu in Lync 2013 per aprire il browser Windows Internet Explorer e visualizzare una console su pagina Web.

Un agente che non deve accedere al gruppo o disconnettersi è denominato *agente informale* . L'accesso degli agenti informali al gruppo viene eseguito automaticamente con l'accesso a Lync Server. Questi agenti non possono disconnettersi dal gruppo.


> [!NOTE]
> Solo gli utenti locali possono essere agenti. Se un agente passa da locale a online, le chiamate del Response Group non saranno più indirizzate a lui.



## Argomenti della sezione

[Creare o modificare un gruppo di agenti in Lync Server 2013](lync-server-2013-create-or-modify-an-agent-group.md)

