---
title: Gestione dei nodi Watcher
TOCTitle: Gestione dei nodi Watcher
ms:assetid: 66deaf49-a71f-4a6e-ada0-ea8b688ee921
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688078(v=OCS.15)
ms:contentKeyID: 49887589
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione dei nodi Watcher

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Oltre a poter modificare le transazioni sintetiche eseguite su un nodo Watcher, gli amministratori possono utilizzare il cmdlet **Set-CsWatcherNodeConfiguration** per eseguire due attività importanti, ovvero abilitare e disabilitare il nodo Watcher, nonché configurarlo per utilizzare URL interni o esterni durante l'esecuzione dei test.

Per impostazione predefinita, i nodi Watcher sono progettati per eseguire periodicamente tutte le transazioni sintetiche abilitate. In alcuni casi, tuttavia, potrebbe risultare necessario sospendere tali transazioni. Se il nodo Watcher è temporaneamente disconnesso dalla rete, ad esempio, non vi è alcun motivo per eseguire le transazioni sintetiche. Senza connettività di rete, tali transazioni hanno necessariamente esito negativo. Se si desidera disabilitare temporaneamente un nodo Watcher, eseguire un comando simile al seguente da Lync Server Management Shell:

    Set-CsWatcherNodeConfiguration -Identity "atl-watcher-001.litwareinc.com" -Enabled $False

Questo comando consente di disabilitare l'esecuzione delle transazioni sintetiche nel nodo Watcher atl-watcher- 001.litwareinc.com. Per riprendere l'esecuzione delle transazioni sintetiche, reimpostare la proprietà Enabled su True ($True):

    Set-CsWatcherNodeConfiguration -Identity "atl-watcher-001.litwareinc.com" -Enabled $True


> [!NOTE]
> È possibile utilizzare la proprietà Enabled per attivare o disattivare i nodi Watcher. Per eliminare in modo definitivo un nodo Watcher, utilizzare il cmdlet <STRONG>Remove-CsWatcherNodeConfiguration</STRONG>:<BR>Remove-CsWatcherNodeConfiguration –Identity "atl-watcher-001.litwareinc.com"<BR>Questo comando consente di rimuovere tutte le impostazioni di configurazione del nodo Watcher dal computer specificato e ciò impedisce l'esecuzione automatica delle transazioni sintetiche. Il comando non disinstalla tuttavia i file agente di System Center o i file di sistema di Lync Server 2013.



Per impostazione predefinita, i nodi Watcher utilizzano gli URL esterni di un'organizzazione per l'esecuzione dei test. È comunque possibile configurare i nodi Watcher anche per l'utilizzo degli URL interni. Ciò consente agli amministratori di verificare l'accesso agli URL per gli utenti che si trovano all'interno della rete perimetrale. Per configurare un nodo Watcher per l'utilizzo degli URL interni anziché di quelli esterni, impostare la proprietà UseInternalWebUrls su True ($True):

    Set-CsWatcherNodeConfiguration -Identity "atl-watcher-001.litwareinc.com" -UseInternalWebUrls $True

Se si reimposta la proprietà sul valore predefinito False ($False), il nodo Watcher utilizzerà gli URL esterni:

    Set-CsWatcherNodeConfiguration -Identity "atl-watcher-001.litwareinc.com" -UseInternalWebUrls $False

