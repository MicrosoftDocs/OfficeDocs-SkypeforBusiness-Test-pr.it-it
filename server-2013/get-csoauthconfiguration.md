---
title: Get-CsOAuthConfiguration
TOCTitle: Get-CsOAuthConfiguration
ms:assetid: a3fda8bf-84e3-4d14-a1c5-093e6eb36ffe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205155(v=OCS.15)
ms:contentKeyID: 49301541
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOAuthConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle impostazioni di configurazione di Open Authorization (OAuth) attualmente in uso nell'organizzazione. OAuth è un protocollo standard utilizzato per l'autenticazione e l'autorizzazione da server a server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsOAuthConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsOAuthConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni sulle impostazioni di configurazione OAuth in uso nell'organizzazione.

    Get-CsOAuthConfiguration

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server e Microsoft Exchange Server 2013 di condividere informazioni, viene effettuata utilizzando il protocollo di sicurezza OAuth. Questo protocollo è sempre attivo in Lync Server 2013. Non è necessario né è possibile abilitare o disabilitare il protocollo. Per consentire tuttavia le comunicazioni tra Lync Server e altri prodotti server, ad esempio Exchange 2013 o Microsoft SharePoint 2013, potrebbe essere necessario modificare le impostazioni di configurazione di OAuth. Potrebbe essere necessario ad esempio specificare l'URL del servizio di individuazione automatica per la versione Office 365 di Exchange e indicare il nome dell'area di autenticazione. Queste impostazioni possono essere gestite solo utilizzando i cmdlet **CsOAuthConfiguration**. Non sono disponibili opzioni per la gestione delle impostazioni di OAuth nel Pannello di controllo di Lync Server 2013.

Si noti che per la versione locale di Lync Server 2013, è possibile disporre di una sola raccolta globale di impostazioni di OAuth. Non è possibile creare raccolte aggiuntive di impostazioni di OAuth né eliminare la raccolta globale. Anche per ogni tenant di Skype for Business online è valido il limite di una singola raccolta di impostazioni di configurazione di OAuth.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOAuthConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsOAuthConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare valori con caratteri jolly per fare riferimento a una raccolta di impostazioni di configurazione OAuth. Poiché è possibile disporre di una sola istanza globale di queste impostazioni, il parametro Filter non è necessario. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Filter &quot;g*&quot;</p>
<p>Questa sintassi recupera tutte le impostazioni di configurazione OAuth la cui identità inizia con la lettera &quot;g&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione OAuth. Dal momento che è possibile disporre di una sola istanza globale di tali impostazioni, non è necessario specificare un'identità nella chiamata al cmdlet <strong>Get-CsOAuthConfiguration</strong>. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione OAuth dalla replica locale dell'archivio di gestione centrale anziché direttamente da tale archivio.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online di cui devono essere recuperate le impostazioni di configurazione OAuth.</p>
<p>Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsOAuthConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsOAuthConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.OAuthSettings.

## Vedere anche

#### Ulteriori risorse

[Set-CsOAuthConfiguration](set-csoauthconfiguration.md)

