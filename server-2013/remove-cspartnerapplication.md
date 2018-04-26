---
title: Remove-CsPartnerApplication
TOCTitle: Remove-CsPartnerApplication
ms:assetid: 3918a2eb-d464-4729-888b-fafebe2227ce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204820(v=OCS.15)
ms:contentKeyID: 49300224
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPartnerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un'applicazione partner esistente. Un'applicazione partner è un'applicazione con cui Lync Server 2013 può scambiare direttamente token di sicurezza senza dover passare attraverso un server dei token di sicurezza di terze parti. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina l'applicazione con identità (Identity) "MicrosoftExchange".

    Remove-CsPartnerApplication -Identity "MicrosoftExchange"

## Esempio 2

Nell'esempio 2 vengono eliminate tutte le applicazioni partner configurate per l'utilizzo nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPartnerApplication** per restituire una raccolta di tutte le applicazioni partner. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPartnerApplication**, che elimina ogni applicazione inclusa nella raccolta.

    Get-CsPartnerApplication | Remove-CsPartnerApplication

## Esempio 3

Nell'esempio 3 vengono eliminate tutte le applicazioni partner con livello di attendibilità impostato su un valore diverso da Full. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPartnerApplication** senza parametri per restituire una raccolta di tutte le applicazioni partner configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le applicazioni in cui la proprietà ApplicationTrustLevel è diversa da (-ne) "Full". Le applicazioni che soddisfano questo criterio vengono quindi inviate tramite pipe al cmdlet **Remove-CsPartnerApplication**, che le rimuove.

    Get-CsPartnerApplication | Where-Object {$_.ApplicationTrustLevel -ne "Full"} | Remove-CsPartnerApplication

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 ed Exchange 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che i due server possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta completamente il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, in genere non è necessario utilizzare un server dei token. Questi prodotti server, infatti, sono in grado di generare propri token di sicurezza. Sarà necessario tuttavia configurare l'altro prodotto server, ad esempio Exchange 2013, come applicazione partner. Sarà necessario inoltre configurare Lync Server 2013 come applicazione partner per l'altro prodotto server. In Lync Server 2013 le applicazioni partner vengono gestite utilizzando i cmdlet **CsPartnerApplication**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPartnerApplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsPartnerApplication** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco dell'applicazione partner da rimuovere, ad esempio:</p>
<p>-Identity &quot;MicrosoftExchange&quot;</p>
<p>Non è possibile utilizzare caratteri jolly per specificare un'identità.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per l'applicazione partner da eliminare. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsPartnerApplication** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPartnerApplication** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsPartnerApplication](get-cspartnerapplication.md)  
[New-CsPartnerApplication](new-cspartnerapplication.md)  
[Set-CsPartnerApplication](set-cspartnerapplication.md)

