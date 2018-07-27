---
title: Configurazione di Lync Server 2013 per l'utilizzo dell'archiviazione di Microsoft Exchange Server 2013
TOCTitle: Configurazione di Lync Server 2013 per l'utilizzo dell'archiviazione di Exchange Server 2013
ms:assetid: 260346d1-edc8-4a0c-8ad2-6c2401c3c377
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ679896(v=OCS.15)
ms:contentKeyID: 49887483
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archiviazione di Microsoft Exchange Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-24_

Microsoft Lync Server 2013 consente agli amministratori di archiviare le trascrizioni di messaggistica istantanea e Web Conferencing nella cassetta postale di Microsoft Exchange Server 2013 di un utente anziché in un database di SQL Server. Se si abilita questa opzione, le trascrizioni vengono scritte nella cartella Eliminazioni della cassetta postale dell'utente. Questa cartella è nascosta e si trova nella cartella Elementi ripristinabili. Sebbene questa cartella non sia visibile agli utenti finali, è indicizzata dal motore di ricerca di Exchange e può essere rilevata utilizzando la ricerca cassetta postale di Exchange e/o Microsoft SharePoint Server 2013. Poiché le informazioni sono archiviate nella stessa cartella utilizzata dalla funzionalità Archiviazione sul posto di Exchange (responsabile dell'archiviazione di posta elettronica e altre comunicazioni di Exchange), gli amministratori hanno la possibilità di utilizzare un solo strumento per cercare tutte le comunicazioni elettroniche archiviate per un utente.

> [!IMPORTANT]  
> Per disabilitare completamente l'archiviazione della conversazione Lync, è inoltre necessario disabilitare la cronologia conversazioni Lync. Per ulteriori informazioni, vedere gli argomenti seguenti: <a href="lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md">Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013</a>, <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy">New-CsClientPolicy</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy">Set-CsClientPolicy</a>.

Per archiviare le trascrizioni in Exchange 2013, è necessario iniziare a configurare l'autenticazione da server a server tra i due server. Dopo la configurazione dell'autenticazione da server a server, è possibile eseguire le attività seguenti in Microsoft Lync Server 2013 (si noti che, in base all'installazione e alla configurazione, potrebbe non essere necessario completare tutte le attività):

1.  Abilitare l'archiviazione di Exchange modificando le impostazioni di configurazione dell'archiviazione di Lync Server. Questo passaggio è obbligatorio per tutte le distribuzioni.

2.  Abilitare l'archiviazione per le comunicazioni interne e/o esterne per gli utenti. Questo passaggio è obbligatorio per tutte le distribuzioni.

3.  Configurare la proprietà ExchangeArchivingPolicy per ogni utente. Questo passaggio è obbligatorio solo se Lync Server e Exchange si trovano in foreste diverse.

## Passaggio 1: Abilitazione dell'archiviazione di Exchange

L'archiviazione in Lync Server è principalmente gestita utilizzando le impostazioni di configurazione dell'archiviazione. Quando si installa Lync Server 2013, viene automaticamente assegnata una singola raccolta globale di queste impostazioni. Se lo desiderano, gli amministratori possono creare nuove raccolte di impostazioni di archiviazione nell'ambito del sito. Per impostazione predefinita, l'archiviazione non è abilitata nelle impostazioni globali, né lo è l'archiviazione di Exchange. Per utilizzare l'archiviazione di Exchange, gli amministratori devono configurare le proprietà EnableArchiving ed EnableExchangeArchiving in queste impostazioni di configurazione. La proprietà EnableArchiving può essere impostata su uno di tre possibili valori:

  - **None** . L'archiviazione è disabilitata. Questo è il valore predefinito. Se la proprietà EnableArchiving è impostata su None, nel database di archiviazione di Lync Server o in Exchange 2013 non verrà archiviato nulla.

  - **ImOnly** . Vengono archiviate solo le trascrizioni dei messaggi istantanei. Se l'archiviazione di Exchange è abilitata queste trascrizioni verranno archiviate in Exchange 2013. Se l'archiviazione di Exchange è disabilitata, queste trascrizioni verranno archiviate in Lync Server.

  - **ImAndWebConf** . Vengono archiviate sia le trascrizioni dei messaggi istantanei sia quelle di Web Conferencing. Se l'archiviazione di Exchange è abilitata queste trascrizioni verranno archiviate in Exchange 2013. Se l'archiviazione di Exchange è disabilitata, queste trascrizioni verranno archiviate in Lync Server.

La proprietà EnableExchangeArchiving è un valore booleano: impostare EnableExchangeArchiving su True ($True) per abilitare l'archiviazione di Exchange o impostare EnableExchangeArchiving su False ($False) per disabilitare l'archiviazione di Exchange. Ad esempio, questo comando abilita l'archiviazione delle trascrizioni dei messaggi istantanei e anche l'archiviazione di Exchange:

    Set-CsArchivingConfiguration -Identity "global" -EnableArchiving ImOnly -EnableExchangeArchiving $True

Per disabilitare l'archiviazione di Exchange, utilizzare un comando simile al seguente, che abilita l'archiviazione della messaggistica istantanea, ma disabilita l'archiviazione in Exchange (in altre parole, le trascrizioni verranno archiviate in Lync Server):

    Set-CsArchivingConfiguration -Identity "global" -EnableArchiving ImOnly -EnableExchangeArchiving $False


> [!NOTE]
> Se la proprietà EnableArchiving è impostata su None, Lync Server non archivierà le trascrizioni di messaggistica istantanea e di Web Conferencing. In tal caso, il server ignorerà semplicemente il valore configurato per EnableExchangeArchiving.



L'archiviazione di Exchange può inoltre essere abilitata o disabilita tramite il Pannello di controllo di Lync Server. A tale scopo, completare la procedura seguente:

1.  Nel Pannello di controllo fare clic su **Monitoraggio e archiviazione** e quindi su **Configurazione archiviazione** .

2.  Nella scheda **Configurazione archiviazione** fare doppio clic sulla raccolta delle impostazioni di archiviazione da modificare (ad esempio la raccolta **Globale** ).

3.  Nel riquadro **Modifica impostazione di archiviazione** fare clic sull'elenco a discesa **Impostazione di archiviazione** e selezionare **Archivia sessioni di messaggistica istantanea** per archiviare solo le sessioni di messaggistica istantanea o su **Archivia sessioni di messaggistica istantanea e Web Conferencing** per archiviare sia le sessioni di messaggistica istantanea sia quelle di Web Conferencing.

4.  Dopo aver scelto gli elementi da archiviare, selezionare la casella di controllo **Integrazione Exchange Server** per abilitare l'archiviazione di Exchange. Per disabilitare l'archiviazione di Exchange, deselezionare questa casella di controllo.


> [!NOTE]
> La casella di controllo <STRONG>Integrazione Exchange Server</STRONG> non sarà disponibile se <STRONG>Impostazione di archiviazione</STRONG> è impostata su <STRONG>Disabilita archiviazione</STRONG> . È necessario abilitare prima l'archiviazione, quindi abilitare l'archiviazione di Exchange.



Se Lync Server 2013 e Exchange 2013 si trovano nella stessa foresta, l'archiviazione per singoli utenti, o almeno per utenti con account di posta elettronica in Exchange 2013, viene gestita utilizzando i criteri di archiviazione sul posto di Exchange. Se sono presenti utenti ospitati in una versione precedente di Exchange, l'archiviazione per tali utenti sarà gestita utilizzando i criteri di archiviazione di Lync Server. Si noti che solo per gli utenti con account in Exchange 2013 è possibile archiviare le trascrizioni di Lync in Exchange.

Se Lync Server 2013 e Exchange 2013 si trovano in foreste diverse, l'archiviazione per singoli utenti viene gestita configurando la proprietà ExchangeArchivingPolicy per ogni singolo account utente. Per ulteriori informazioni, vedere il passaggio 3.

## Passaggio 2: Abilitazione dell'archiviazione delle comunicazioni interne e/o esterne

Dopo aver abilitato l'archiviazione, e l'archiviazione di Exchange, è quindi necessario modificare i criteri di archiviazione appropriati per garantire l'effettiva archiviazione delle sessioni utente. Si noti che con la semplice abilitazione dell'archiviazione (passaggio 1) non si avvia l'archiviazione di Lync Server delle trascrizioni di messaggistica istantanea e Web Conferencing. È invece necessario utilizzare i criteri di archiviazione per abilitare l'archiviazione interna e/o esterna. Quando si installa Lync Server 2013 viene anche installato un singolo criterio di archiviazione globale che contiene due proprietà:

  - **ArchiveInternal** . Se impostata su True ($True), indica che verranno archiviate le sessioni di comunicazione interna che interessano solo gli utenti con account Active Directory attivi nell'organizzazione.

  - **ArchiveExternal** . Se impostata su True ($True), indica che verranno archiviate le sessioni di comunicazione esterna (sessioni che interessano almeno un utente che non ha un account Active Directory attivo nell'organizzazione.

Per impostazione predefinita, i valori di entrambe queste proprietà sono impostati su False, pertanto non vengono archiviate le sessioni di comunicazione né interna né esterna. Per modificare il criterio globale, è possibile utilizzare Lync Server Management Shell e il cmdlet Set-CsArchivingPolicy. Questo comando abilita l'archiviazione delle sessioni di comunicazione sia interna sia esterna:

    Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $True -ArchiveExternal $True

In alternativa, è possibile utilizzare New-CsArchivingPolicy per creare un nuovo criterio nell'ambito del sito o per utente. Ad esempio, questo comando crea un nuovo criterio di archiviazione per utente denominato RedmondArchivingPolicy:

    New-CsArchivingPolicy -Identity "RedmondArchivingPolicy" -ArchiveInternal $True -ArchiveExternal $True

Se si crea un criterio per utente, sarà quindi necessario assegnarlo agli utenti appropriati. Ad esempio:

    Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName  "RedmondArchivingPolicy"

I criteri di archiviazione possono inoltre essere gestiti utilizzando il Pannello di controllo di Lync Server. Nel Pannello di controllo, fare clic su **Monitoraggio e archiviazione** , quindi su **Criteri di archiviazione** . Per modificare criteri esistenti, fare doppio clic sui criteri (ad esempio Globale), quindi nel riquadro **Modifica criteri di archiviazione** selezionare o deselezionare le caselle di controllo **Archivia comunicazioni interne** e **Archivia comunicazioni esterne** secondo le esigenze. Per creare nuovi criteri di archiviazione, fare clic su **Nuovo** e selezionare **Criterio sito** o **Criteri utente** . Se si creano nuovi criteri utente, è quindi necessario accedere agli account utente appropriati (dalla scheda **Utenti** ) e assegnare a tali utenti i nuovi criteri.

## Passaggio 3: Configurazione della proprietà ExchangeArchivingPolicy

Se Lync Server 2013 e Exchange 2013 si trovano in foreste diverse, non è sufficiente abilitare l'archiviazione di Exchange nelle impostazioni di configurazione di archiviazione; ciò non ha come risultato l'archiviazione delle trascrizioni di messaggistica istantanea e Web Conferencing in Exchange. Al contrario, è necessario configurare la proprietà ExchangeArchivingPolicy in ciascuno degli account utente di Lync Server rilevanti. Questa proprietà può essere impostata su uno di quattro possibili valori:

1.  Uninitialized. Indica che l'archiviazione sarà basata sulle impostazioni di archiviazione sul posto configurate per la cassetta postale di Exchange dell'utente; se l'archiviazione sul posto non è abilitata nella cassetta postale dell'utente, le trascrizioni di messaggistica e Web Conferencing dell'utente saranno archiviate in Lync Server.

2.  **UseLyncArchivingPolicy** . Indica che le trascrizioni di messaggistica istantanea e Web Conferencing dell'utente devono essere archiviate in Lync Server anziché in Exchange.

3.  **NoArchiving** . Indica che le trascrizioni di messaggistica istantanea e Web Conferencing non devono essere archiviate. Si noti che questa impostazione sostituisce qualsiasi criterio di archiviazione di Lync Server assegnato all'utente.

4.  **ArchivingToExchange** . Indica che le trascrizioni di messaggistica istantanea e Web Conferencing devono essere archiviate in Exchange indipendentemente dalle impostazioni di archiviazione sul posto assegnate o meno alla cassetta postale dell'utente.

Ad esempio, per configurare un account utente in modo che le trascrizioni di messaggistica istantanea e Web Conferencing vengano sempre archiviate in Exchange è possibile utilizzare un comando simile al seguente da Lync Server Management Shell:

    Set-CsUser -Identity "Ken Myer" -ExchangeArchivingPolicy ArchivingToExchange

Per impostare gli stessi criteri di archiviazione per un gruppo di utenti (ad esempio tutti gli utenti ospitati in un pool di registrazione specificato), è possibile utilizzare un comando simile al seguente:

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Set-CsUser -ExchangeArchivingPolicy ArchivingToExchange

Si noti che è necessario utilizzare Lync Server Management Shell (e Windows PowerShell) per configurare il valore della proprietà di ExchangeArchivingPolicy. Questa proprietà non è esposta agli amministratori nel Pannello di controllo di Lync Server.

Per visualizzare un elenco di tutti gli utenti a cui è stato assegnato un criterio di archiviazione specifico, è possibile utilizzare un comando simile al seguente che restituisce il nome visualizzato di Active Directory di tutti gli utenti la cui proprietà ExchangeArchivingPolicy è impostata su Uninitialized:

    Get-CsUser | Where-Object {$_.ExchangeArchivingPolicy -eq "Uninitialized"} | Select-Object DisplayName

In modo analogo, questo comando restituisce il nome visualizzato degli utenti la cui proprietà ExchangeArchivingPolicy non è impostata su UseLyncArchivingPolicy:

    Get-CsUser | Where-Object {$_.ExchangeArchivingPolicy -ne "UseLyncArchivingPolicy"} | Select-Object DisplayName

