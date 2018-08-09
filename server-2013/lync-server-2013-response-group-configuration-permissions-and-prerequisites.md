---
title: "Lync Server 2013: Autorizzaz. e prerequisiti per configurare Response Group"
TOCTitle: Autorizzazioni e prerequisiti per la configurazione di Response Group
ms:assetid: 4266f16a-b387-452c-a8ca-d771a3c58f0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204840(v=OCS.15)
ms:contentKeyID: 49300341
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Autorizzazioni e prerequisiti per la configurazione di Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Response Group è una funzionalità di gestione delle chiamate di VoIP aziendale. In questo argomento vengono indicati i componenti di cui è necessario disporre prima di poter configurare Response Group e le autorizzazioni e le credenziali amministrative richieste per eseguire le attività di configurazione.

In questa sezione si presuppone la lettura della documentazione relativa alla pianificazione correlata a Response Group. Per informazioni dettagliate, vedere [Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md) nella documentazione relativa alla pianificazione.

## Strumenti di configurazione e ruoli amministrativi

È possibile utilizzare gli strumenti amministrativi seguenti per configurare Response Group:

  - Pannello di controllo di Lync Server

  - Strumento di configurazione di Response Group

  - Lync Server Management Shell

Per configurare i Response Group, è necessario essere membri di almeno uno dei ruoli amministrativi seguenti:


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Gruppo di sicurezza Active Directory (1)</strong></p></td>
<td><p>Creare flusso di lavoro</p></td>
<td><p>Assegnare responsabile</p></td>
<td><p>Creare/assegnare agenti, code</p></td>
<td><p>Creare/gestire festività e orari di ufficio</p></td>
<td><p>Attivare/disattivare il flusso di lavoro</p></td>
<td><p>Configurare il flusso di lavoro (IVR o gruppo di risposta)</p></td>
</tr>
<tr class="even">
<td><p><strong>CsResponseGroupAdministrator</strong></p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
</tr>
<tr class="odd">
<td><p><strong>CsResponseGroupManager</strong></p></td>
<td> </td>
<td><p>v(2)</p></td>
<td><p>v(3)</p></td>
<td><p>v(3)</p></td>
<td><p>v(3)</p></td>
<td><p>v(3)</p></td>
</tr>
<tr class="even">
<td><p><strong>CsVoiceAdministrator</strong></p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
</tr>
<tr class="odd">
<td><p><strong>CsServerAdministrator</strong></p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
</tr>
<tr class="even">
<td><p><strong>CsAdministrator</strong></p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
<td><p>v</p></td>
</tr>
<tr class="odd">
<td><p><strong>CsViewOnlyAdministrator</strong></p></td>
<td><p>v(4)</p></td>
<td><p>v(4)</p></td>
<td><p>v(4)</p></td>
<td><p>v(4)</p></td>
<td><p>v(4)</p></td>
<td><p>v(4)</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <STRONG>(1)</STRONG> Un oggetto utente Servizi di dominio Active Directory deve essere membro del gruppo di sicurezza Active Directory specificato nella tabella. Un amministratore o un altro membro delegato del gruppo Active Directory provvisto delle autorizzazioni appropriate per aggiungere utenti a un gruppo di sicurezza (ad esempio Administrator, Account Operators) deve aggiungere un oggetto utente al gruppo o al gruppo di sicurezza elencato perché l'utente possa eseguire le funzioni elencate. <STRONG>(2)</STRONG> Solo per i flussi di lavoro che il ruolo CsResponseGroupAdministrator ha assegnato al CsResponseGroupManager. <STRONG>(3)</STRONG> Un responsabile di Response Group può assegnare un altro membro di CsResponseGroupManager a un flusso di lavoro già gestito dal responsabile corrente. <STRONG>(4)</STRONG> CsViewOnlyAdministrator può eseguire solo i cmdlet di Lync Server Management Shell che includono il verbo "Get".



## Response Group Prerequisiti di configurazione

Response Group richiede i componenti seguenti:

  - Servizio applicazione

  - applicazione Response Group

  - Language Pack

  - Archivio file (per gestire i file audio)

  - Servizi Web (sono inclusi lo Strumento di configurazione di Response Group e la console di accesso e disconnessione degli agenti)

Tutti questi componenti vengono installati per impostazione predefinita quando si distribuisce VoIP aziendale.

Prima di configurare Response Group può essere necessario eseguire le attività seguenti:

  - Abilitare gli utenti per Lync Server 2013 e VoIP aziendale.

  - Modificare un file di configurazione in modo che sia conforme agli standard FIPS (Federal Information Processing Standard).

  - Modificare le regole di confronto del database per supportare caratteri Yi, Meng e Zang per i nomi di code e i nomi dei gruppi di agenti.

## Abilitazione degli utenti

Il primo passaggio della configurazione dell'applicazione Response Group consiste nella creazione di gruppi di agenti. Prima di poter creare un gruppo di agenti, è necessario abilitare gli utenti che saranno agenti di Response Group per Lync Server 2013 e VoIP aziendale. L'abilitazione degli utenti per Lync Server 2013 è in genere un passaggio incluso nella distribuzione dei server Enterprise Edition o Standard Edition. Per informazioni dettagliate sull'abilitazione degli utenti per Lync Server 2013, vedere [Disabilitare o abilitare nuovamente gli account utente per Lync Server](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md). L'abilitazione degli utenti per VoIP aziendale è in genere un passaggio incluso nella distribuzione di VoIP aziendale. Per informazioni dettagliate, vedere [Abilitare gli utenti per VoIP aziendale in Lync Server 2013](lync-server-2013-enable-users-for-enterprise-voice.md).

## Conformità ai requisiti FIPS

Fare riferimento a questa sezione solo se l'organizzazione deve essere conforme agli standard FIPS (Federal Information Processing Standards).

Per essere conformi a FIPS, è necessario modificare il file Web.config a livello dell'applicazione in modo da usare un algoritmo di crittografia diverso dopo aver installato Servizi Web. È necessario specificare l'uso dell'algoritmo 3DES (Triple Data Encryption Standard) per ASP.NET per l'elaborazione dei dati sugli stati di visualizzazione. Per l'applicazione Response Group, questo requisito si applica a Strumento di configurazione di Response Group e alla console di accesso e disconnessione degli agenti. Per informazioni dettagliate su questo requisito, vedere l'articolo della Microsoft Knowledge Base 911722 intitolato "È possibile che venga visualizzato un messaggio di errore quando si accede a pagine Web ASP.NET con ViewState abilitato dopo l'aggiornamento da ASP.NET 1.1 ad ASP.NET 2.0" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=196183](http://go.microsoft.com/fwlink/p/?linkid=196183).

Per modificare il file Web.config, eseguire le operazioni seguenti:

1.  In un editor di testo come Blocco note aprire il file Web.config a livello dell'applicazione.

2.  Nel file Web.config individuare la sezione `<system.web>`.

3.  Aggiungere la sezione `<machineKey>` seguente alla sezione `<system.web>`:
    
        <machineKey validationKey="AutoGenerate,IsolateApps" decryptionKey="AutoGenerate,IsolateApps" validation="3DES" decryption="3DES"/>

4.  Salvare il file Web.config.

5.  Riavviare il servizio Internet Information Services (IIS) eseguendo il comando seguente al prompt dei comandi:
    
        iisreset

## Supporto di caratteri Yi, Meng e Zang

Fare riferimento a questa sezione solo se l'organizzazione richiede il supporto di caratteri Yi, Meng o Zang.


> [!NOTE]
> Per informazioni sui caratteri Yi, Meng e Zang e sull'importanza che potrebbero avere per una distribuzione, vedere le informazioni relative ai set di caratteri GB18030, disponibili all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=240223">http://go.microsoft.com/fwlink/p/?linkId=240223</A>.



Per il supporto di caratteri Yi, Meng o Zang è necessario modificare le regole di confronto del database Rgsconfig. Modificare le regole di confronto della colonna **Name** nelle tabelle seguenti di ogni database Rgsconfig:

  - dbo.AgentGroups

  - dbo.BusinessHours

  - dbo.HolidaySets

  - dbo.Queues

  - dbo.Workflows

Per SQL Server 2008 R2 e SQL Server 2012, usare le regole di confronto Latin\_General\_100 (distinzione tra caratteri accentati e non accentati). Se si utilizzano queste regole di confronto, la distinzione tra maiuscole e minuscole non viene applicata ad alcun nome di oggetto.

È possibile modificare le regole di confronto utilizzando Microsoft SQL Server Management Studio. Per informazioni dettagliate sull'utilizzo di questo strumento, vedere "Utilizzo di SQL Server Management Studio" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=196184](http://go.microsoft.com/fwlink/p/?linkid=196184). Per modificare le regole di confronto, eseguire la procedura seguente:

1.  Verificare che SQL Server Management Studio sia configurato per consentire modifiche che richiedono la ricreazione di tabelle. Per informazioni dettagliate, vedere "Finestra di dialogo Salva (non consentito)" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=196186](http://go.microsoft.com/fwlink/p/?linkid=196186). Per informazioni dettagliate sull'impostazione di regole di confronto di colonna, vedere "Procedura: Impostazione di una sequenza di confronto tra colonne (Visual Database Tools)" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=196185](http://go.microsoft.com/fwlink/p/?linkid=196185).

2.  Utilizzando Microsoft SQL Server Management Studio connettersi al database Rgsconfig.

3.  Trovare la tabella che si desidera modificare nel database Rgsconfig, fare clic con il pulsante destro del mouse sulla tabella e quindi scegliere **Progetta** .

4.  Modificare le regole di confronto della colonna **Name** e salvare la tabella.

