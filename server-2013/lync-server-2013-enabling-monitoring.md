---
title: Abilitazione del monitoraggio in Lync Server 2013
TOCTitle: Abilitazione del monitoraggio in Lync Server 2013
ms:assetid: 244df419-d0a8-4b1d-aedd-a92114172ab6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687994(v=OCS.15)
ms:contentKeyID: 49887481
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione del monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-17_

Sebbene gli agenti di raccolta dati unificati vengano automaticamente installati e attivati su ogni Front End Server, ciò non significa che verrà automaticamente avviata la raccolta di dati di monitoraggio non appena viene completata l'installazione di Microsoft Lync Server 2013. Al contrario, è necessario eseguire due operazioni: associare Front End Server e pool Front End a un database di monitoraggio e abilitare il monitoraggio di registrazione dettagli chiamata e/o QoE nell'ambito globale e/o del sito.

Per istruzioni dettagliate sull'associazione di Front End Server o pool Front End con un database di monitoraggio, vedere l'argomento [Associazione di un archivio di monitoraggio a un pool Front End](lync-server-2013-associating-a-monitoring-store-with-a-front-end-pool.md) nella guida alla distribuzione. Dopo aver completato queste associazioni e dopo aver pubblicato la nuova topologia di Lync Server, non è ancora possibile raccogliere dati di monitoraggio. Ciò dipende dal fatto che, per impostazione predefinita, la raccolta di dati di registrazione dettagli chiamata e QoE è disabilitata quando si installa Lync Server 2013.

Per iniziare la raccolta dei dati, è necessario abilitare il monitoraggio di registrazione dettagli chiamata e/o QoE. In alternativa, è possibile abilitare un tipo di monitoraggio e non l'altro. Per abilitare il monitoraggio di registrazione dettagli chiamata nell'ambito globale, eseguire il comando di seguito dall'interno di Lync Server Management Shell:

    Set-CsCdrConfiguration -Identity "global" -EnableCDR $True

In alternativa, è possibile abilitare il monitoraggio di registrazione dettagli chiamata dal Pannello di controllo di Lync Server 2013. Dal Pannello di controllo di Lync Server, completare la procedura seguente:

1.  Fare clic su **Monitoraggio**.

2.  Nella scheda **Registrazione dettagli chiamata** fare doppio clic sull'impostazione **Globale**.

3.  Nel riquadro **Modifica impostazione di registrazione dettagli chiamata** selezionare **Abilita monitoraggio registrazioni dettagli chiamata** e fare clic su **Commit**.

Per abilitare il monitoraggio QoE nell'ambito globale, eseguire il comando dall'interno di Lync Server Management Shell:

    Set-CsQoEConfiguration -Identity "global" -EnableQoE $True

In alternativa, è inoltre possibile abilitare il monitoraggio QoE dal Pannello di controllo di Lync Server. Dal Pannello di controllo, completare la procedura seguente:

1.  Fare clic su **Monitoraggio**.

2.  Nella scheda **Dati QoE** fare doppio clic sull'impostazione **Globale**.

3.  Nel riquadro **Modifica impostazione QoE** selezionare **Abilita monitoraggio dei dati QoE** e fare clic su **Commit**.

Come si può notare, negli esempi precedenti il monitoraggio viene abilitato nell'ambito globale, ciò significa che il monitoraggio di registrazione dettagli chiamata e QoE viene abilitato per l'intera organizzazione. In alternativa, è possibile creare impostazioni di configurazione di registrazione dettagli chiamata e QoE nell'ambito del sito, quindi abilitare o disabilitare in modo selettivo per ogni sito. Ad esempio, è possibile abilitare il monitoraggio di registrazione dettagli chiamata per il sito di Parigi, ma disabilitarlo per il sito di Milano. Per ulteriori informazioni sulla gestione delle impostazioni di configurazione del monitoraggio, vedere l'argomento [Configurazione delle impostazioni di Registrazione dettagli chiamata e Qualità percepita dagli utenti](lync-server-2013-configuring-call-detail-recording-and-quality-of-experience-settings.md) nella guida relativa alla distribuzione.

