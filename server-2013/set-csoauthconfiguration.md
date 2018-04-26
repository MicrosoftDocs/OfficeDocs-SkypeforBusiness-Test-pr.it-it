---
title: Set-CsOAuthConfiguration
TOCTitle: Set-CsOAuthConfiguration
ms:assetid: 43193254-acb1-47c8-8e21-143b610c2edc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204841(v=OCS.15)
ms:contentKeyID: 49300364
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOAuthConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni di configurazione di Open Authorization (OAuth) attualmente in uso nell'organizzazione. OAuth è un protocollo standard utilizzato per l'autenticazione e l'autorizzazione da server a server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsOAuthConfiguration [-ExchangeAutodiscoverAllowedDomains <String>] [-ExchangeAutodiscoverUrl <String>] [-Identity <XdsIdentity>] [-Realm <String>] [-ServiceName <String>] <COMMON PARAMETERS>

    Set-CsOAuthConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 modifica la raccolta globale delle impostazioni di configurazione di OAuth. In questo esempio la proprietà Realm viene impostata su "contoso.com".

    Set-CsOAuthConfiguration -Identity global -Realm "contoso.com"

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server e Microsoft Exchange Server 2013 di condividere informazioni, viene effettuata utilizzando il protocollo di sicurezza OAuth. Questo protocollo è sempre attivo in Lync Server 2013. Non è necessario né è possibile abilitare o disabilitare il protocollo. Per consentire tuttavia le comunicazioni tra Lync Server e altri prodotti server, ad esempio Exchange 2013 o Microsoft SharePoint 2013, potrebbe essere necessario modificare le impostazioni di configurazione di OAuth. Potrebbe essere necessario ad esempio specificare l'URL del servizio di individuazione automatica per la versione Office 365 di Exchange e indicare il nome dell'area di autenticazione. Queste impostazioni possono essere gestite solo utilizzando i cmdlet **CsOAuthConfiguration**. Non sono disponibili opzioni per la gestione delle impostazioni di OAuth nel Pannello di controllo di Lync Server 2013.

Si noti che per la versione locale di Lync Server 2013, è possibile disporre di una sola raccolta globale di impostazioni di OAuth. Non è possibile creare raccolte aggiuntive di impostazioni di OAuth né eliminare la raccolta globale. Anche per ogni tenant di Skype for Business online è valido il limite di una singola raccolta di impostazioni di configurazione di OAuth.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOAuthConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsOAuthConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeAutodiscoverAllowedDomains</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Raccolta di domini a cui possono essere reindirizzate le richieste di individuazione automatica. Ad esempio:</p>
<p>-ExchangeAutodiscoverAllowedDomains &quot;*.contoso.com&quot;,&quot;*.fabrikam.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeAutodiscoverUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio di individuazione automatica utilizzato dalla versione Office 365 di Microsoft Exchange Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione di OAuth. Poiché è possibile disporre di una sola istanza globale di queste impostazioni, non è necessario specificare un'identità quando si chiama il cmdlet <strong>Set-CsOAuthConfiguration</strong>. È tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Realm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Contenitore di sicurezza da server a server. Per impostazione predefinita, Lync Server 2013 utilizza il dominio SIP predefinito come area di autenticazione OAuth.</p></td>
</tr>
<tr class="even">
<td><p><em>ServiceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale (GUID) assegnato al servizio OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui vengono modificate le impostazioni di configurazione di OAuth. Ad esempio:</p>
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

Il cmdlet **Set-CsOAuthConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthSettings inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsOAuthConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsOAuthConfiguration](get-csoauthconfiguration.md)

