---
title: Get-CsTenantFederationConfiguration
TOCTitle: Get-CsTenantFederationConfiguration
ms:assetid: e5f836d0-6066-4c23-9594-6e3f1cbd39ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994072(v=OCS.15)
ms:contentKeyID: 52062461
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantFederationConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione della federazione per i tenant di Microsoft Lync Online. Le impostazioni di configurazione della federazione vengono usate per determinare con quali domini possono eventualmente comunicare gli utenti.

Il cmdlet **Get-CsTenantFederationConfiguration** può essere usato solo con Skype for Business online.

## Sintassi

    Get-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-LocalStore] [-Verbose] Get-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-Filter <String>] [-LocalStore] [-Verbose]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 restituisce informazioni sulla configurazione della federazione per il tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354". Gli ID dei tenant possono essere recuperati con un comando simile al seguente:

Get-CsTenant | Select-Object TenantID

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Si noti che il parametro Tenant è facoltativo. È possibile chiamare Get-CsTenantFederationConfiguration anche con questa sintassi:

    Get-CsTenantFederationConfiguration

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per tutti i domini individuati nell'elenco dei domini consentiti per la federazione per il tenant bf19b7db-6960-41e5-a139-2aa373474354. (L'elenco dei domini consentiti include tutti i domini con i quali è permessa la federazione del tenant.) A tale scopo, il comando chiama prima di tutto il cmdlet **Get-CsTenantFederationConfiguration** per restituire informazioni sulla federazione per il tenant specificato. Queste informazioni vengono poi inviate tramite pipe al cmdlet **Select-Object**, che usa ExpandProperty per "espandere" la proprietà AllowedList. L'espansione di una proprietà significa semplicemente visualizzare tutte le informazioni archiviate in quella proprietà in un formato di facile lettura.

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty AllowedList

## Esempio 3

Il comando precedente restituisce la configurazione della federazione per tutti i tenant in uso nell'organizzazione. Per eseguire questa operazione, il comando chiama prima di tutto il cmdlet **Get-CsTenant** senza parametri, che restituisce una raccolta dei tenant disponibili. Tale raccolta viene poi inviata tramite pipe al cmdlet **ForEach-Object**. ForEach-Object viene usato per chiamare il cmdlet **Get-CsTenantFederationConfiguration** su ogni tenant nella raccolta, usando il valore della proprietà TenantID (restituito dal cmdlet **Get-CsTenant**) per rappresentare l'ID del tenant.

    Get-CsTenant | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId}

## Esempio 4

Nell'esempio 4 vengono restituite informazioni sulla configurazione della federazione solo per i tenant che non consentono la federazione con utenti pubblici. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsTenant** senza alcun parametro per restituire una raccolta di tutti i tenant configurati per l'uso nell'organizzazione. La raccolta viene poi inviata tramite pipe al cmdlet **ForEach-Object** che esegue il cmdlet **Get-CsTenantFederationConfiguration** su ogni tenant nella raccolta per restituire informazioni sulla configurazione della federazione. Il set completo di informazioni sulla configurazione della federazione viene poi inviato tramite pipe al cmdlet **Where-Object**, che seleziona solo i tenant con la proprietà AllowPublicUsers uguale a (-eq) $False.

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId} | Where-Object {$_.AllowPublicUsers -eq $False}

## Descrizione dettagliata

Il servizio di federazione consente agli utenti di scambiarsi informazioni di messaggistica istantanea e sulla presenza con utenti di altri domini. Con Lync Online gli amministratori possono usare le impostazioni di configurazione della federazione per gestire:

  - La possibilità per gli utenti di comunicare con utenti di altri domini ed eventualmente con quali domini possono comunicare.

  - La possibilità per gli utenti di comunicare con altri utenti che dispongono di account presso un servizio di messaggistica istantanea o presso un provider della presenza pubblico come Windows Live, AOL e Yahoo.

Il cmdlet **Get-CsTenantFederationConfiguration** consente agli amministratori di ottenere informazioni sulla federazione per i loro tenant di Lync Online. Questo cmdlet può essere usato anche per verificare gli elenchi dei domini consentiti e bloccati, ovvero gli elenchi usati per specificare i domini con cui gli utenti possono o meno comunicare. Gli amministratori devono comunque usare il cmdlet **Get-CsTenantPublicProvider** per scoprire i provider di servizi di messaggistica istantanea e di presenza pubblici con cui gli utenti sono autorizzati a comunicare.

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
<td><p>Consente di usare i caratteri jolly per restituire una raccolta di impostazioni di configurazione della federazione dei tenant. Poiché esiste il limite di una sola raccolta globale di impostazioni di configurazione della federazione, non è necessario usare il parametro Filter. Questa è comunque una sintassi valida per il cmdlet <strong>Get-CsTenantFederationConfiguration</strong>:</p>
<p>Get-CsTenantFederationConfiguration –Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Specifica la raccolta delle impostazioni di configurazione della federazione dei tenant da restituire. Poiché ogni tenant è limitato a un'unica raccolta globale di impostazioni della federazione, non è necessario includere questo parametro quando si chiama il cmdlet <strong>Get-CsTenantFederationConfiguration</strong>. Se si sceglie di usare il parametro Identity, è necessario includere anche il parametro Tenant. Ad esempio:</p>
<p>Get-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione della federazione dei tenant dalla replica locale dell'archivio di gestione centrale, anziché l'archivio stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di cui vengono restituite le impostazioni di federazione. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTenantFederationConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsTenantFederationConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Vedere anche

#### Ulteriori risorse

[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

