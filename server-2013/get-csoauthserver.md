---
title: Get-CsOAuthServer
TOCTitle: Get-CsOAuthServer
ms:assetid: c2a61eb0-cdff-4069-99e4-2bdf42812f47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205238(v=OCS.15)
ms:contentKeyID: 49301901
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOAuthServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui server Open Authorization (OAuth) configurati per l'utilizzo da parte dell'organizzazione. I server OAuth, noti anche come server dei token di sicurezza, generano token di sicurezza utilizzati nell'autenticazione e nell'autorizzazione da server a server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsOAuthServer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsOAuthServer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutti i server OAuth configurati per l'utilizzo nell'organizzazione.

    Get-CsOAuthServer

## ESEMPIO 2

Nell'esempio 2 le informazioni vengono restituite per il server OAuth con valore Identity "Office 365".

    Get-CsOAuthServer -Identity "Office 365"

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 e Microsoft Exchange Server 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che i due server possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, non è necessario in genere utilizzare un server dei token. Questi prodotti server, infatti, sono in grado di generare propri token di sicurezza. Se tuttavia si desidera comunicare con un altro prodotto server, tra cui i prodotti server contenuti in Office 365, sarà necessario utilizzare un server dei token. I server dei token possono essere gestiti utilizzando i cmdlet **CsOAuthServer**.

Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOAuthServer"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsOAuthServer** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare i caratteri jolly per restituire uno o più server OAuth. Ad esempio, per restituire tutti i server OAuth aventi un valore Identity contenente il valore stringa &quot;Microsoft&quot;, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*Microsoft*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il server OAuth da restituire. Esempio:</p>
<p>-Identity &quot;Office 365&quot;</p>
<p>Se né il parametro Identity né il parametro Filter vengono inclusi nel comando, il cmdlet <strong>Get-CsOAuthServer</strong> restituirà informazioni su tutti i server OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera il dati del servizio OAuth dalla replica locale dell'Archivio di gestione centrale anziché dall'archivio stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui è necessario recuperare le impostazioni del server OAuth.</p>
<p>Esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsOAuthServer** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsOAuthServer** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthServer\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsOAuthServer](new-csoauthserver.md)  
[Remove-CsOAuthServer](remove-csoauthserver.md)  
[Set-CsOAuthServer](set-csoauthserver.md)

