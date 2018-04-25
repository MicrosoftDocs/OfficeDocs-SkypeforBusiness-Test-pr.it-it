---
title: Get-CsPrivacyConfiguration
TOCTitle: Get-CsPrivacyConfiguration
ms:assetid: f10ebf4a-1af5-48cf-96dc-4f5d56281848
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413002(v=OCS.15)
ms:contentKeyID: 49302418
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPrivacyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione della privacy attualmente in uso nell'organizzazione. Tali impostazioni consentono di determinare quante informazioni gli utenti rendono disponibili per altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsPrivacyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPrivacyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Il comando indicato nell'esempio 1 restituisce tutte le impostazioni di configurazione della privacy attualmente in uso nell'organizzazione.

    Get-CsPrivacyConfiguration

## ESEMPIO 2

Nell'esempio 2 viene restituita una raccolta singola delle impostazioni di configurazione della privacy, ovvero le impostazioni con Identity site:Redmond.

    Get-CsPrivacyConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni per tutte le impostazioni di configurazione della privacy che sono state assegnate nell'ambito del sito. A tale scopo, viene incluso il parametro Filter con il valore di filtro "site:\*". Tale valore del filtro garantisce che vengano restituite solo le impostazioni il cui parametro Identity (l'unica proprietà alla quale è possibile applicare il filtro) inizia con i caratteri "site:".

    Get-CsPrivacyConfiguration -Filter "site:*"

## ESEMPIO 4

Il comando mostrato nell'esempio 4 restituisce informazioni su tutte le impostazioni di configurazione della privacy in cui è stata abilitata la modalità privacy. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsPrivacyConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni relative alla privacy. La raccolta viene quindi inoltrata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnablePrivacyMode è uguale a True.

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $True}

## Descrizione dettagliata

Lync Server consente agli utenti di condividere con altre persone un'elevata quantità di informazioni sulla presenza, grazie alla possibilità di pubblicare foto personali, di fornire informazioni dettagliate sulla posizione e di rendere automaticamente disponibili le informazioni sulla presenza a chiunque sia membro dell'organizzazione (anziché rendere disponibili tali informazioni solo alle persone presenti nell'elenco Contatti personale).

Alcuni utenti apprezzeranno la possibilità di rendere disponibili queste informazioni ai propri colleghi, mentre altri potrebbero essere più restii a condividere questi dati. Ad esempio, molte persone potrebbero essere riluttanti ad includere le proprie foto personali nei dati sulla presenza. Gli utenti in genere hanno il controllo sulle informazioni che intendono o non intendono condividere, ad esempio possono selezionare o deselezionare una casella di controllo per scegliere se condividere con altri le proprie informazioni sulla posizione. I cmdlet di configurazione della privacy consentono inoltre agli amministratori di gestire le impostazioni relative alla privacy degli utenti. In alcuni casi, gli amministratori possono abilitare o disabilitare determinate impostazioni. Ad esempio, se la proprietà AutoInitiateContacts è impostata su True, i membri del team verranno aggiunti automaticamente all'elenco Contatti di ciascun utente. Se invece è impostata su False, i membri del team non verranno aggiunti automaticamente all'elenco Contatti di ciascun utente.

In altri casi, gli amministratori possono configurare i valori predefiniti in Lync Server, dando comunque agli utenti la possibilità di modificare tali valori. Ad esempio, per impostazione predefinita i dati sulla posizione vengono pubblicati per gli utenti, nonostante gli utenti abbiano il diritto di disabilitare la pubblicazione della posizione. Impostando la proprietà PublishLocationDataByDefault su False, gli amministratori possono modificare questo comportamento. In tal caso, i dati sulla posizione non verranno pubblicati per impostazione predefinita, nonostante gli utenti abbiano ancora il diritto di pubblicare questi dati se lo desiderano.

Le impostazioni di configurazione della privacy possono essere applicate nell'ambito globale, nell'ambito del sito e nell'ambito del servizio (ma solo per il servizio Server utente). Il cmdlet **Get-CsPrivacyConfiguration** consente di recuperare informazioni su tutte le impostazioni di configurazione della privacy attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsPrivacyConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli Controllo degli accessi in base al ruolo a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli Controllo degli accessi in base al ruolo personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPrivacyConfiguration"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare caratteri jolly per restituire una o più raccolte delle impostazioni di configurazione della privacy. Ad esempio, per restituire tutte le impostazioni configurate nell'ambito del sito, è possibile utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per restituire tutte le impostazioni configurate nell'ambito del servizio, utilizzare la seguente sintassi: -Filter &quot;service:*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione della privacy da recuperare. Per restituire le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per restituire le impostazioni configurate nell'ambito del sito, utilizzare la sintassi: -Identity site:Redmond. Per modificare le impostazioni a livello del servizio, utilizzare una sintassi simile alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Get-CsPrivacyConfiguration</strong> restituirà tutte le impostazioni di configurazione della privacy attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione della privacy dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui si devono recuperare le impostazioni di configurazione relative alla privacy.</p>
<p>Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Eseguendo questo comando è possibile fare in modo che venga restituito l'ID di ogni tenant:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet**Get-CsPrivacyConfiguration** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPrivacyConfiguration** restituisce le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

