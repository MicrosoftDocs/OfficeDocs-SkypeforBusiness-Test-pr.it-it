---
title: Remove-CsOAuthServer
TOCTitle: Remove-CsOAuthServer
ms:assetid: fac7be48-06bb-4572-86a2-b872fe96d199
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205408(v=OCS.15)
ms:contentKeyID: 49302538
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsOAuthServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un server OAuth (Open Authorization) esistente. I server OAuth, noti anche come server dei token di sicurezza, generano token di sicurezza utilizzati nell'autenticazione e nell'autorizzazione da server a server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsOAuthServer -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina un singolo server OAuth: il server con l'identità "Office 365".

    Remove-CsOAuthServer -Identity "Office365"

## Esempio 2

Nell'esempio 2 vengono eliminati tutti i server OAuth configurati per l'utilizzo nell'organizzazione. Per eseguire questa attività, nel comando viene innanzitutto chiamato il cmdlet **Get-CsOAuthServer** senza alcun parametro per restituire tutti i server OAuth. Questi server vengono quindi inviati tramite pipe al cmdlet **Remove-CsOAuthServer**, che li rimuove.

    Get-CsOAuthServer | Remove-CsOAuthServer

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 e Microsoft Exchange Server 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che i due server possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, non è necessario in genere utilizzare un server dei token. Questi prodotti server infatti sono in grado di generare propri token di sicurezza. Se tuttavia si desidera comunicare con un altro prodotto server, tra cui i prodotti server contenuti in Office 365, sarà necessario utilizzare un server dei token. I server dei token possono essere gestiti utilizzando i cmdlet **CsOAuthServer**.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsOAuthServer"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsOAuthServer** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco per il server OAuth da eliminare. Esempio:</p>
<p>-Identity &quot;Office 365&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant Skype for Business online per il server OAuth da eliminare. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive cosa accadrebbe se si eseguisse il comando senza eseguirlo effettivamente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsOAuthServer** accetta istanze da pipeline dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated.

## Tipi restituiti

Nessuno. Viceversa, il cmdlet **Remove-CsOAuthServer** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsOAuthServer](get-csoauthserver.md)  
[New-CsOAuthServer](new-csoauthserver.md)  
[Set-CsOAuthServer](set-csoauthserver.md)

