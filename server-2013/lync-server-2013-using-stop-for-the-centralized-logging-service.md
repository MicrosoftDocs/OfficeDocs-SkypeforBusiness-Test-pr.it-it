---
title: Utilizzo del comando Stop per il servizio di registrazione centralizzato
TOCTitle: Utilizzo del comando Stop per il servizio di registrazione centralizzato
ms:assetid: 09ac093e-8f30-4874-84b4-12548ac8c898
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687964(v=OCS.15)
ms:contentKeyID: 49887437
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo del comando Stop per il servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Il cmdlet Stop-CsClsLogging consente di interrompere una sessione di registrazione in esecuzione. In generale, le situazioni in cui può essere necessario interrompere una sessione di registrazione non sono molte. Ad esempio, è possibile eseguire ricerche nei log e modificare configurazioni senza bisogno di interrompere la registrazione. Se sono in esecuzione due scenari, ad esempio AlwaysOn e UserReplicator, ed è necessario raccogliere informazioni relative all'autenticazione, per poter avviare lo scenario Authentication sarà necessario interrompere uno dei due scenari, a livello globale, di pool o di sito. Per informazioni dettagliate, vedere [Stop-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging).


> [!NOTE]
> Nella determinazione degli scenari da eseguire in un dato pool, computer o distribuzione, tenere presente che l'esecuzione è limitata a due scenari <STRONG>per computer</STRONG>. Se si stanno registrando le attività in un pool, è consigliabile trattare il pool come una singola entità. Nella maggior parte dei casi l'esecuzione di scenari diversi in ogni computer di un pool non ha senso. È invece opportuno esaminare il problema su cui si stanno raccogliendo dati e stabilire quale scenario abbia più senso in un determinato computer nella distribuzione complessiva. Ad esempio, se si considera lo scenario UserReplicator, eseguire UserReplicator in un server perimetrale o in un pool di server perimetrali non risulterebbe molto utile.<BR>Una volta compresi il problema e l'ambito dell'impatto, andranno effettuate scelte attente sugli scenari da eseguire e sui computer e pool ai quali applicarli. Mentre lo scenario AlwaysOn è adatto all'applicazione su vasta scala, in quanto raccoglie informazioni su un'ampia gamma di provider, gli scenari specifici risultano utili solo se applicati a specifici computer o pool. È inoltre necessaria attenzione quando si avvia una sessione di registrazione scelta a caso senza prima comprendere il valore di un dato scenario. Se si utilizza lo scenario sbagliato, oppure si sceglie uno scenario appropriato per l'attività, ma lo si applica all'ambito sbagliato (a livello globale, di sito, di pool o di computer), si possono ottenere dati dubbi e non molto utili, come se non si fosse eseguito affatto lo scenario.



Per controllare le funzioni del servizio di registrazione centralizzato utilizzando Lync Server Management Shell è necessario essere membri del gruppo di sicurezza CsAdministrator o CsServerAdministrator per il ruolo di controllo di accesso basato sui ruoli (RBAC), oppure di un ruolo RBAC personalizzato che contenga uno dei due gruppi. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, eseguire il comando seguente dal prompt di Lync Server Management Shell o di Windows PowerShell:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

Ad esempio:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

## Per interrompere una sessione di servizio di registrazione centralizzato in esecuzione

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire una query sul servizio di registrazione centralizzato per individuare gli scenari attualmente in esecuzione digitando quanto segue:
    
        Show-CsClsLogging
    
    ![Console di Windows PowerShell dopo la chiamata a Show-CsCl](images/JJ687964.eb190c32-529c-4277-a731-52c47d22d8fa(OCS.15).jpg "Console di Windows PowerShell dopo la chiamata a Show-CsCl")
    
    Il risultato di Show-CsClsLogging è un riepilogo degli scenari in esecuzione e dei relativi ambiti di esecuzione. Per informazioni dettagliate, vedere [Show-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Show-CsClsLogging).

3.  Per interrompere una sessione di registrazione in esecuzione con uno scenario specifico, digitare:
    
        Stop-CsClsLogging -Scenario <scenario name> -Computers <comma separated list of fully qualified computer names> -Pools <comma separated list of fully qualified pool names>
    
    Ad esempio:
    
        Stop-CsClsLogging -Scenario UserReplicator -Pools pool01.contoso.net
    
    Questo comando interromperà la registrazione con lo scenario UserReplicatior in pool01.contoso.net.
    

    > [!NOTE]
    > I log creati nel corso di questa sessione di registrazione utilizzando lo scenario UserReplicator non vengono eliminati. La registrazione resta disponibile per l'esecuzione di ricerche mediante il comando Search-CsClsLogging. Per informazioni dettagliate, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Search-CsClsLogging">Search-CsClsLogging</A>.



Il cmdlet Stop-CsClsLogging funge da comando complementare a Start-CsClsLogging e interrompe la sessione di registrazione, definita dagli scenari, conservando i log creati. È possibile eseguire un totale di due scenari su un dato computer in qualsiasi momento. L'interruzione di uno scenario per raccogliere informazioni utilizzando uno scenario diverso è un'attività comune, utile nella maggior parte delle procedure di risoluzione dei problemi relativi ai carichi di lavoro.

## Vedere anche

#### Attività

[Utilizzo del comando Start per l'acquisizione dei log da parte del servizio di registrazione centralizzato](lync-server-2013-using-start-for-the-centralized-logging-service-to-capture-logs.md)  

#### Concetti

[Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md)  

#### Ulteriori risorse

[Show-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Show-CsClsLogging)  
[Start-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Start-CsClsLogging)  
[Stop-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging)

