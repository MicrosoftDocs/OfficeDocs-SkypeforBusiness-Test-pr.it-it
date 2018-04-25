---
title: Set-CsOAuthServer
TOCTitle: Set-CsOAuthServer
ms:assetid: 52825ca3-d287-4e09-9aec-b8b2d7bafc06
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204896(v=OCS.15)
ms:contentKeyID: 49300576
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOAuthServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un server OAuth (Open Authorization) esistente. I server OAuth, noti anche come server dei token di sicurezza, generano token di sicurezza utilizzati nell'autenticazione e nell'autorizzazione da server a server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsOAuthServer <COMMON PARAMETERS>

    Set-CsOAuthServer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MetadataUrl <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 aggiorna l'URL dei metadati per il server OAuth Office 365.

    Set-CsOAuthServer -Identity "Office 365" -MetadataUrl "https://sts.office365.microsoft.com/metadata/json/1"

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 e Microsoft Exchange Server 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, non è necessario in genere utilizzare un server dei token. Questi prodotti server infatti sono in grado di generare propri token di sicurezza. Se tuttavia si desidera comunicare con un altro prodotto server, tra cui i prodotti server contenuti in Office 365, sarà necessario utilizzare un server dei token. I server dei token possono essere gestiti utilizzando i cmdlet CsOAuthServer.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOAuthServer"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsOAuthServer** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome descrittivo (e univoco) utilizzato per identificare il server OAuth.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MetadataUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL in cui vengono pubblicati i metadati WS-FederationMetadata del server. I server utilizzano i metadati per concordare i tipi di token che verranno scambiati e le chiavi che verranno utilizzate per la firma dei token.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per il server OAuth da modificare. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsOAuthServer** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsOAuthServer** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsOAuthServer](get-csoauthserver.md)  
[New-CsOAuthServer](new-csoauthserver.md)  
[Remove-CsOAuthServer](remove-csoauthserver.md)

