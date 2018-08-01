---
title: "Lync Server 2013: Elenco di controllo di distribuzione per l'archiviazione"
TOCTitle: Elenco di controllo di distribuzione per l'archiviazione
ms:assetid: 7479734d-be01-40d9-ad82-320a09d19d04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205009(v=OCS.15)
ms:contentKeyID: 49300985
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per l'archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

L'archiviazione è installata automaticamente su ciascun server Front End della distribuzione di Lync Server 2013, ma prima di utilizzarla è necessario configurarla. I passaggi necessari per la configurazione, riepilogati in questa sezione, costituiscono la distribuzione dell'archiviazione.

## Sequenza di distribuzione

La modalità di configurazione dell'archiviazione dipende dall'opzione di archiviazione che si seleziona:

  - Se si utilizza l'integrazione di Microsoft Exchange per tutti gli utenti nella distribuzione, non è necessario configurare i criteri di archiviazione di Lync Server 2013 per gli utenti. È tuttavia necessario configurare i criteri di archiviazione sul posto di Exchange affinché supportino l'archiviazione per gli utenti ospitati su Exchange 2013, e per le cui cassette postali è stata impostata l'archiviazione sul posto. Per informazioni dettagliate sulla configurazione di questi criteri, vedere la documentazione fornita dal produttore in relazione a Exchange 2013.

  - Se non si utilizza l'integrazione di Microsoft Exchange per tutti gli utenti nella distribuzione, sarà necessario aggiungere database di archiviazione di Lync Server (database SQL Server) alla topologia, e poi pubblicarla, nonché configurare criteri e impostazioni per gli utenti, prima di poter archiviare dati per questi utenti. È possibile distribuire i database di archiviazione mentre si distribuisce la topologia iniziale o dopo avere distribuito almeno un pool Front End o un server Standard Edition. In questo documento viene illustrato come distribuire database di archiviazione aggiungendoli a una distribuzione esistente.

Se si abilita l'archiviazione in un pool Front End o in un server Standard Edition, sarà necessario abilitarla per tutti gli altri pool Front End e server Standard Edition nella distribuzione. Questo è dovuto al fatto che gli utenti di cui devono essere archiviate le comunicazioni possono essere invitati a una conversazione di messaggistica istantanea di gruppo oppure a riunioni ospitate in un altro pool. Se l'archiviazione non è abilitata nel pool in cui viene ospitata la conversazione o la riunione, potrebbe non essere possibile archiviare l'intera sessione. In questi casi, è possibile archiviare la messaggistica istantanea con utenti abilitati per l'archiviazione, ma non per file di contenuto delle conferenze e eventi di accesso o abbandono della conferenza.

> [!IMPORTANT]  
> Se per motivi di conformità l'archiviazione è di importanza critica nell'organizzazione, assicurarsi di distribuire l'archiviazione, di configurare criteri e altre opzioni al livello appropriato, e di abilitare l'archiviazione per tutti gli utenti appropriati prima di abilitare tali utenti per Lync Server 2013.

## Processo di distribuzione dell'archiviazione

Nella tabella seguente viene fornita una panoramica dei passaggi da eseguire per distribuire l'archiviazione in una topologia esistente.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Ruoli e gruppi a cui è necessario appartenere</th>
<th>Documentazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Installare l'hardware e il software prerequisiti</strong></p></td>
<td><ul><li><p>Per utilizzare l'integrazione di Microsoft Exchange (utilizzando Exchange 2013 per l'archiviazione di alcuni o tutti gli utenti), è necessaria una distribuzione esistente di Exchange 2013.</p></li><li><p>Per utilizzare database di archiviazione separati (utilizzando database SQL Server) per l'archiviazione di alcuni o tutti gli utenti, è necessario SQL Server sul server che memorizzerà i dati di archiviazione.</p></li></ul>

> [!NOTE]
> L'archiviazione è eseguita sui server Front End di un pool Enterprise e server Standard Edition. Non esistono ulteriori requisiti di hardware o software oltre a quelli necessari per l'installazione di questi server.


</td>
<td><p>Utente del dominio membro del gruppo Administrators locale</p></td>
<td><p><a href="lync-server-2013-supported-hardware.md">Hardware supportato per Lync Server 2013</a> nella documentazione relativa alla supportabilità</p>
<p><a href="lync-server-2013-server-software-and-infrastructure-support.md">Supporto dell'infrastruttura e del software server in Lync Server 2013</a> nella documentazione relativa alla supportabilità</p>
<p><a href="lync-server-2013-technical-requirements-for-archiving.md">Requisiti tecnici per l'archiviazione in Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p>
<p><a href="lync-server-2013-setting-up-systems-and-infrastructure-for-archiving.md">Configurazione dei sistemi e dell'infrastruttura per l'archiviazione in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p>
<p><a href="lync-server-2013-exchange-and-sharepoint-integration-support.md">Supporto per l'integrazione di Exchange Server e SharePoint in Lync Server 2013</a> nella documentazione relativa alla supportabilità</p></td>
</tr>
<tr class="even">
<td><p><strong>Creare la topologia interna appropriata per supportare l'archiviazione (solo se non si utilizza l'integrazione di Microsoft Exchange per tutti gli utenti nella distribuzione)</strong></p></td>
<td><p>Eseguire Generatore di topologie per aggiungere database di archiviazione a Lync Server 2013 (database SQL Server) alla topologia, quindi pubblicarla.</p></td>
<td><p>Per definire una topologia che incorpori database di archiviazione, un account membro del gruppo Users locale.</p>
<p>Per pubblicare la topologia, un account che sia membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins e che disponga delle autorizzazioni di controllo completo (lettura/scrittura/modifica) sulla condivisione file da utilizzare per l'archivio file di Lync Server 2013, in modo che Generatore di topologie possa configurare gli elenchi DACL necessari.</p></td>
<td><p><a href="lync-server-2013-adding-archiving-databases-to-an-existing-lync-server-2013-deployment.md">Aggiunta dei database di archiviazione a una distribuzione Lync Server 2013 esistente</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p><strong>Configurare l'intergrazione server-to-server (solo se si utilizza l'integrazione di Microsoft Exchange)</strong></p></td>
<td><p>Configurare i server per abilitare l'autenticazione tra Lync Server 2013 e Exchange 2013. È consigliabile eseguire <strong>Test-CsExchangeStorageConnectivity testuser_sipUri –Folder Dumpster</strong> per convalidare la connettività dell'archiviazione di Exchange, prima di abilitare quest'ultima.</p></td>
<td><p>Un account con le autorizzazioni appropriate per la gestione dei certificati sul server.</p></td>
<td><p><a href="lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md">Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013</a> nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Configurare i criteri e le configurazioni per l'archiviazione</strong></p></td>
<td><p>Configurare l'archiviazione, incluso l'eventuale utilizzo dell'integrazione di Microsoft Exchange, i criteri globali e gli eventuali criteri dei siti e degli utenti (quando non si utilizza l'integrazione di Microsoft Exchange per l'intera archiviazione dati), nonché le opzioni di archiviazione specifiche, ad esempio la modalità critica e l'esportazione ed eliminazione dei dati.</p>
<p>Se si utilizza l'integrazione di Microsoft Exchange, configurare i criteri di archiviazione sul posto di Exchange a seconda delle necessità.</p></td>
<td><p>Gruppo RTCUniversalServerAdmins (solo Windows PowerShell) oppure assegnare gli utenti al ruolo CSArchivingAdministrator o CSAdministrator</p></td>
<td><p><a href="lync-server-2013-configuring-support-for-archiving.md">Configurazione del supporto per l'archiviazione in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p>
<p>documentazione fornita dal produttore in relazione a Exchange (se si utilizza l'integrazione di Microsoft Exchange).</p></td>
</tr>
</tbody>
</table>


## Distribuzione di Lync Server e Microsoft Exchange in foreste diverse

Se Microsoft Exchange Server è distribuito in una foresta diversa rispetto a Lync Server, è necessario assicurarsi che i seguenti attributi di Exchange Active Directory siano sincronizzati alla foresta nella quale è distribuito Lync Server:

1.  msExchUserHoldPolicies

2.  proxyAddresses

Si tratta di un attributo a valore multiplo. Quando si sincronizza questo attributo, è necessario unire i valori, e non sostituirli, per evitare che i valori esistenti vengano persi.

