---
title: Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archivio contatti unificato
TOCTitle: Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archivio contatti unificato
ms:assetid: 6aa17ae3-764e-4986-a900-85a3cdb8c1fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688083(v=OCS.15)
ms:contentKeyID: 49887596
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archivio contatti unificato

 

_**Ultima modifica dell'argomento:** 2014-02-07_

L'archivio unificato per i contatti consente agli utenti di mantenere un elenco contatti unico, e rendere i contatti disponibili in più applicazioni, tra cui Microsoft Lync 2013, Microsoft Outlook 2013 e Microsoft Outlook Web App 2013. Quando si abilita l'archivio unificato per i contatti di un utente, i contatti di questo non sono archiviati in Microsoft Lync Server 2013 e recuperati usando il protocollo SIP; i contatti vengono invece archiviati in Microsoft Exchange Server 2013 e recuperati utilizzando i Servizi Web Exchange.


> [!NOTE]
> Tecnicamente, le informazioni del contatto sono archiviate in una coppia di cartelle che si trova nella cassetta postale di Exchange 2013 dell'utente. I contatti sono archiviati in una cartella chiamata Contatti di Lync, visibile all'utente finale. I metadati relativi ai contatti, invece, sono archiviati in una sottocartella non visibile all'utente finale.



## Abilitazione dell'archivio unificato per i contatti di un utente

Se è già stata configurata l'autenticazione server-to-server tra Lync Server 2013 e Exchange 2013, l'utilizzo dell'archivio unificato per i contatti è già attivo, e non sono necessarie ulteriori configurazioni del server. Tuttavia, per spostare i contatti di un utente all'interno dell'archivio unificato è necessaria la configurazione di un ulteriore account utente. Per impostazione predefinita, i contatti di un utente sono archiviati in Lync Server e non nell'archivio unificato per i contatti.

L'accesso all'archivio unificato per i contatti è gestito mediante i criteri dei servizi utente di Lync Server. I criteri sono dotati di una proprietà singola (UcsAllowed), utilizzata per determinare il percorso in cui sono archiviati i contatti di un utente. Se un utente è gestito da un criterio in cui UcsAllowed è stato impostato su True ($True), i contatti di quell'utente saranno archiviati nell'archivio unificato per i contatti. Se l'utente è invece gestito da un criterio in cui UcsAllowed è stato impostato su False ($False), i contatti di costui saranno archiviati in Lync Server.

Quando si installa Lync Server 2013, viene installato anche un criterio dei servizi utente (configurato a livello globale). Il valore UcsAllowed del criterio è impostato su True, e pertanto, per impostazione predefinita, i contatti degli utenti verranno archiviati nell'archivio unificato per i contatti, presupponendo che sia stato distribuito e configurato. Per migrare tutti i contatti degli utenti all'archivio unificato, non è necessario eseguire alcuna operazione.

Se si preferisce non migrare tutti i contatti all'archivio unificato per i contatti, è possibile disabilitare l'archivio per tutti gli utenti impostando su False la proprietà UcsAllowed nel criterio globale:

    Set-CsUserServicesPolicy -Identity global -UcsAllowed $False

Dopo aver disabilitato l'archivio unificato per i contatti nel criterio globale, è possibile lasciare il criterio globale intatto e creare un criterio "per utente" che consenta l'utilizzo dell'archivio unificato per i contatti. In questo modo è possibile consentire ad alcuni utenti di mantenere i contatti all'interno dell'archivio unificato per i contatti, e ad altri utenti di mantenere i contatti in Lync Server. Per creare criteri dei servizi utente, "per utente", usare un comando simile al seguente:

    New-CsUserServicesPolicy -Identity "AllowUnifiedContactStore" -UcsAllowed $True

Dopo aver creato il nuovo criterio, bisognerà assegnarlo agli utenti ai quali si desidera concedere l'accesso all'archivio unificato per i contatti. I criteri "per utente" possono essere assegnati agli utenti attraverso un comando simile al seguente:

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName "AllowUnifiedContactStore"

Dopo che il criterio è stato assegnato, Lync Server inizierà a migrare i contatti dell'utente verso l'archivio unificato per i contatti. Al termine della migrazione, i contatti dell'utente saranno archiviati in Exchange e non in Lync Server. Se l'utente ha effettuato l'accesso a Lync 2013 al termine della migrazione, una casella di testo chiederà di disconnettersi da Lync e connettersi nuovamente per finalizzare il processo. I contatti degli utenti ai quali non è stato assegnato questo criterio per utente non verranno migrati all'archivio unificato per i contatti. Tali utenti vengono infatti gestiti dal criterio globale in cui è stato disabilitato l'archivio unificato.

È possibile verificare che i contatti di un utente sono stati migrati correttamente all'archivio unificato per i contatti, eseguendo il cmdlet [Test-CsUnifiedContactStore](test-csunifiedcontactstore.md) da Lync Server Management Shell:

    Test-CsUnifiedContactStore -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetFqdn "atl-cs-001.litwareinc.com"

Se il cmdlet Test-CsUnifiedContactStore è eseguito con successo, i contatti del sip:kenmyer@litwareinc.com sono stati migrati correttamente all'archivio unificato per i contatti.

## Rollback (ripristino) dell'archivio unificato per i contatti

Se si ha bisogno di rimuovere i contatti di un utente dall'archivio unificato per i contatti (ad esempio, se l'utente deve essere riassegnato a Microsoft Lync Server 2010 e pertanto non può più utilizzare l'archivio unificato per i contatti), è necessario eseguire due operazioni. Per prima cosa, è necessario assegnare un nuovo criterio dei servizi utente all'utente in questione, un criterio che proibisca l'archiviazione dei contatti nell'archivio unificato per i contatti, ovvero un criterio in cui la proprietà UcsAllowed sia impostata su $False. Se non si dispone di un simile criterio, è possibile crearlo attraverso il seguente comando:

    New-CsUserServicesPolicy -Identity NoUnifiedContactStore -UcsAllowed $False

È quindi possibile assegnare il nuovo criterio "per utente" (NoUnifiedContactStore) attraverso un comando simile al seguente:

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName NoUnifiedContactStore

Questo comando assegna all'utente Ken Myer il nuovo criterio, e fa in modo che i contatti di Ken non vengano migrati all'archivio unificato per i contatti.


> [!NOTE]
> In alcuni casi è possibile ottenere lo stesso risultato semplicemente annullando il criterio dei servizi utente dall'utente in questione. Supponiamo, ad esempio, che a Ken Myer sia assegnato un criterio dei servizi utente di tipo "per utente", che attiva l'archivio unificato per i contatti, e che il criterio globale proibisce l'utilizzo di quest'ultimo. In questo caso, è possibile annullare il criterio dei servizi utente di tipo "per utente" da Ken. In questo modo, Ken sarà gestito automaticamente dal criterio globale, e non avrà più accesso all'archivio unificato per i contatti.<BR>Per annullare l'assegnazione di un criterio per utente precedentemente assegnato, utilizzare lo stesso comando illustrato in precedenza, ma impostare il parametro PolicyName su un valore null:<BR>Grant-CsUserServicesPolicy –Identity "Ken Myer" –PolicyName $Null



Quando si lavora con l'archivio unificato per i contatti, è importante tenere a mente la frase "fa in modo che i contatti di Ken non vengano migrati all'archivio unificato per i contatti". La sola assegnazione di un nuovo criterio dei servizi utente a Ken non sposta i contatti dall'archivio unificato per i contatti. Quando un utente accede a Lync Server 2013, il sistema verifica il criterio dei servizi utente di quel particolare utente per capire se i contatti devono essere mantenuti nell'archivio unificato per i contatti. Se la risposta è sì (ovvero, se la proprietà UcsAllowed è impostata su $True), i contatti saranno migrati all'archivio unificato per i contatti (sempre che non vi siano già).Se la risposta è no, Lync Server ignorerà i contatti dell'utente e passerà all'attività successiva. Ciò significa che Lync Server non sposta automaticamente i contatti fuori dall'archivio unificato per i contatti, indipendentemente dal valore della proprietà UcsAllowed.

Ciò significa inoltre che, dopo avere assegnato all'utente un nuovo crierio dei servizi utente, è necessario eseguire il cmdlet [Invoke-CsUcsRollback](invoke-csucsrollback.md) per spostare i contatti dell'utente fuori da Exchange 2013 e riportarli a Lync Server 2013. Ad esempio, dopo avere assegnato a Ken Myer un nuovo criterio dei servizi utente, è possibile spostare i suoi contatti fuori dall'archivio unificato per i contatti, utilizzando il seguente comando:

    Invoke-CsUcsRollback -Identity "Ken Myer"

Se si modifica il criterio dei servizi utente ma non si esegue il cmdlet Invoke-CsUcsRollback, i contatti di Ken non saranno rimossi dall'archivio unificato per i contatti. Cosa succede se si esegue il cmdlet Invoke-CsUcsRollback ma non si modifica il criterio dei servizi utente di Ken Myer? In questo caso, i contatti di Ken vengono rimossi temporaneamente dall'archivio unificato per i contatti. È importante ricordare che questa rimozione è temporanea. Dopo aver rimosso i contatti di Ken dall'archivio unificato per i contatti, Lync Server 2013 attenderà 7 giorni prima di verificare quale criterio dei servizi utente è stato assegnato a Ken. Se a Ken è ancora assegnato un criterio che consente l'utilizzo dell'archivio unificato per i contatti, i contatti saranno automaticamente spostati nuovamente nell'archivio unificato per i contatti. Per rimuovere temporaneamente i contatti dall'archivio unificato per i contatti, è necessario modificare il criterio dei servizi utente, oltre ad eseguire il cmdlet Invoke-CsUcsRollback.

In considerazione dell'elevato numero di variabili che influiscono sulla migrazione, è difficile stimare la durata di una completa migrazione degli account verso l'archivio unificato per i contatti. In linea di massima, tuttavia, la migrazione non è immediata: lo spostamento potrebbe richiedere più di 10 minuti anche se la migrazione interessa un numero molto limitato di contatti.

