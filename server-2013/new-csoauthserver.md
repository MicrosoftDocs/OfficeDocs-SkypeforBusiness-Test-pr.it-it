---
title: New-CsOAuthServer
TOCTitle: New-CsOAuthServer
ms:assetid: b9d10216-a743-4e62-9cf0-6d5fb55dd64e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205206(v=OCS.15)
ms:contentKeyID: 49301786
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOAuthServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo server OAuth (Open Authorization) per l'utilizzo nell'organizzazione. I server OAuth, noti anche come server dei token di sicurezza, generano token di sicurezza utilizzati nell'autenticazione e nell'autorizzazione da server a server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsOAuthServer -MetadataUrl <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsGlobalRelativeIdentity>] [-InMemory <SwitchParameter>] [-Realm <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene creato un nuovo server OAuth denominato "Office 365". Il nuovo server utilizza l'URL dei metadati https://sts.office365.microsoft.com/metadata/json/1.

    New-CsOAuthServer -Identity "Office 365" -MetadataUrl "https://sts.office365.microsoft.com/metadata/json/1"

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 e Microsoft Exchange Server 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, non è necessario in genere utilizzare un server dei token. Questi prodotti server infatti sono in grado di generare propri token di sicurezza. Se tuttavia si desidera comunicare con un altro prodotto server, tra cui i prodotti server contenuti in Office 365, sarà necessario utilizzare un server dei token. I server dei token possono essere gestiti utilizzando i cmdlet **CsOAuthServer**.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOAuthServer"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet New-CsOAuthServer non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>MetadataUrl</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URL in cui vengono pubblicati i metadati WS-FederationMetadata per il server. I server utilizzano i metadati per concordare i tipi di token che verranno scambiati, nonché le chiavi che verranno utilizzate per firmare tali token. L'URL specificato deve essere disponibile quando si esegue il cmdlet <strong>New-CsOAuthServer</strong>, altrimenti il comando avrà esito negativo.</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome descrittivo (e univoco) utilizzato per identificare il server OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Realm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Contenitore di sicurezza da server a server. Per impostazione predefinita, Lync Server 2013 utilizza il dominio SIP predefinito come area di autenticazione OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per il quale viene creato il nuovo server OAuth, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsOAuthServer** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsOAuthServer** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsOAuthServer](get-csoauthserver.md)  
[Remove-CsOAuthServer](remove-csoauthserver.md)  
[Set-CsOAuthServer](set-csoauthserver.md)

