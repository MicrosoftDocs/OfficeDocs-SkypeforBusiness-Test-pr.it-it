---
title: Get-CsPartnerApplication
TOCTitle: Get-CsPartnerApplication
ms:assetid: a20738b5-d9e7-4da4-bcac-e967f73c4bdc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205128(v=OCS.15)
ms:contentKeyID: 49301513
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPartnerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su tutte le applicazioni partner configurate per l'utilizzo nell'organizzazione. Per applicazione partner si intende qualsiasi applicazione con cui Lync Server 2013 può scambiare direttamente token di sicurezza senza dover scambiare tali token mediante un server dei token di sicurezza di terze parti. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPartnerApplication [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPartnerApplication [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le applicazioni partner configurate per l'utilizzo nell'organizzazione.

    Get-CsPartnerApplication

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per l'applicazione partner con l'identità MicrosoftExchange.

    Get-CsPartnerApplication -Identity "MicrosoftExchange"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni per tutte le applicazioni partner con identificatore uguale a "microsoft.exchange". A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPartnerApplication** senza alcun parametro. Viene così restituita una raccolta di tutte le applicazioni partner configurate. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le applicazioni partner in cui la proprietà ApplicationIdentifier è uguale a "microsoft.exchange".

    Get-CsPartnerApplication | Where-Object {$_.ApplicationIdentifier -eq "microsoft.exchange"}

## Esempio 4

Nell'esempio 4 vengono restituite informazioni per tutte le applicazioni partner attualmente disabilitate. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPartnerApplication** per restituire una raccolta di tutte le applicazioni partner, sia abilitate che disabilitate. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le applicazioni in cui la proprietà Enabled è uguale a False.

    Get-CsPartnerApplication | Where-Object {$_.Enabled -eq $False}

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 e Exchange 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, non è necessario in genere utilizzare un server dei token. Questi prodotti server infatti sono in grado di generare propri token di sicurezza. Sarà necessario tuttavia configurare l'altro prodotto server, ad esempio Exchange 2013, come applicazione partner. Sarà necessario inoltre configurare Lync Server 2013 come applicazione partner per l'altro prodotto server. In Lync Server 2013 le applicazioni partner vengono gestite utilizzando i cmdlet **CsPartnerApplication**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPartnerApplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPartnerApplication** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare valori con caratteri jolly per restituire una o più applicazioni partner. Ad esempio, per restituire tutte le applicazioni partner che hanno un'identità che include il valore stringa &quot;Microsoft&quot;, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*Microsoft*&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco dell'applicazione partner. Ad esempio:</p>
<p>-Identity &quot;MicrosoftExchange&quot;</p>
<p>Se nel comando non viene incluso né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPartnerApplication</strong> restituirà informazioni per tutte le applicazioni partner.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati delle applicazioni partner dalla replica locale dell'archivio di gestione centrale anziché direttamente da tale archivio.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per il quale devono essere recuperate le impostazioni delle applicazioni partner.</p>
<p>Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPartnerApplication** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPartnerApplication** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsPartnerApplication](new-cspartnerapplication.md)  
[Remove-CsPartnerApplication](remove-cspartnerapplication.md)  
[Set-CsPartnerApplication](set-cspartnerapplication.md)

