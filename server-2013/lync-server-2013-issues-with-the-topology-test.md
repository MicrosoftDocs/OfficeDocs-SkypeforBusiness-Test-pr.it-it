---
title: Problemi con il test della topologia
TOCTitle: Problemi con il test della topologia
ms:assetid: 821e8916-7b5d-4f64-8fb0-e5cc392ec1bb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205045(v=OCS.15)
ms:contentKeyID: 49301158
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Problemi con il test della topologia

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Come nel cmdlet **Test-CsTopology** Best Practice Analyzer consente di verificare che Lync Server 2013 funzioni correttamente a livello globale. Per impostazione predefinita, Best Practice Analyzer, come il cmdlet, consente di controllare l'intera infrastruttura di Lync Server 2013 verificando che i servizi richiesti siano in esecuzione e che siano state configurate le autorizzazioni e i diritti utenti appropriati per tali servizi e per i gruppi di sicurezza universali creati durante l'installazione di Lync Server 2013.

Oltre a verificare la validità di Lync Server come un insieme **Test-CsTopology** consente anche di verificare la validità di un particolare servizio. Per informazioni dettagliate sull'utilizzo del cmdlet per testare servizi specifici, vedere [Test-CsTopology](test-cstopology.md) nella documentazione relativa a Lync Server Management Shell. Utilizzare le seguenti informazioni per risolvere i problemi nella topologia.


> [!NOTE]
> A seconda della configurazione dei server perimetrali e delle relative impostazioni di rete, incluse le impostazioni e le autorizzazioni per i firewall, Best Practices Analyzer potrebbe non essere in grado di accedere ai server perimetrali e analizzarli. Se si includono server perimetrali nell'analisi, e i rapporti indicano un problema di accesso, deselezionare la casella di controllo <STRONG>Server perimetrali</STRONG> ed eseguire nuovamente la scansione per evitare che il problema compaia nei rapporti.



## Risoluzione dei problemi nella topologia

Se l'analisi della topologia riporta errori nella stessa, è possibile che gli errori siano stati originati da problemi occorsi al momento della pubblicazione o abilitazione della topologia.

Quando si apportano modifiche alla propria topologia, queste non saranno effettive finché non saranno pubblicate e abilitate. Per apportare modifiche alla topologia è necessario utilizzare Generatore di topologie. Dopo aver apportato le modifiche, è possibile pubblicare e abilitare le modifiche utilizzando Generatore di topologie.

Con la pubblicazione delle modifiche, le nuove informazioni, ad esempio un nuovo sito o un nuovo ruolo del server, vengono scritte nell'archivio di gestione centrale. Questi oggetti nuovi, o appena modificati, tuttavia non vengono aggiunti immediatamente alla topologia, ma solo dopo l'abilitazione della topologia aggiornata. Se si seleziona l'opzione Pubblicazione nello Generatore di topologie, verranno effettuate le due operazioni seguenti: le modifiche verranno pubblicate, ovvero scritte nell'archivio di gestione centrale, e la nuova topologia verrà abilitata.

Per impostazione predefinita, i membri del gruppo RTCUniversalServerAdmins sono autorizzati a eseguire il cmdlet **Publish-CsTopology** e il cmdlet **Enable-CsTopology**. Se però le autorizzazioni di installazione non sono state delegate, sarà possibile eseguire **Publish-CsTopology** solo se si effettua l'accesso come amministratori di dominio. Per conferire al gruppo RTCUniversalServerAdmins il diritto di utilizzare effettivamente il cmdlet **Publish-CsTopology**, è necessario eseguire il cmdlet **Grant-CsSetupPermission** per ogni contenitore di Active Directory con computer che eseguono servizi di Lync Server. Per concedere agli RTCUniversalServerAdmins il diritto di utilizzare realmente il cmdlet **Enable-CsTopology**, è necessario eseguire il cmdlet **Set-CsSetupPermission** per ogni contenitore di Active Directory nel quale siano presenti computer che eseguono servizi di Lync Server. Ciò si applica all'abilitazione e alla pubblicazione di una topologia attraverso Generatore di topologie. Se non si è in possesso di autorizzazioni delegate utilizzando **Set-CsSetupPermission**, solo gli amministratori di dominio saranno in grado di abilitare e pubblicare una topologia tramite Generatore di topologie.

