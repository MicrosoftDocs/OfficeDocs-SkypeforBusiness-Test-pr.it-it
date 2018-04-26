---
title: New-CsPartnerApplication
TOCTitle: New-CsPartnerApplication
ms:assetid: 0248acde-626d-42b4-a071-c96171364a18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204628(v=OCS.15)
ms:contentKeyID: 49299496
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPartnerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova applicazione partner. Un'applicazione partner è un'applicazione con cui Lync Server 2013 può scambiare direttamente token di sicurezza senza dover passare attraverso un server dei token di sicurezza di terze parti. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPartnerApplication -ApplicationIdentifier <String> -ApplicationTrustLevel <User | Application | Full> -CertificateRawData <String> -Realm <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Tenant <Guid>] <COMMON PARAMETERS>

    New-CsPartnerApplication -ApplicationIdentifier <String> -ApplicationTrustLevel <User | Application | Full> -CertificateFileData <String> -Realm <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Tenant <Guid>] <COMMON PARAMETERS>

    New-CsPartnerApplication -ApplicationIdentifier <String> -ApplicationTrustLevel <User | Application | Full> -UseOAuthServer <SwitchParameter> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Realm <String>] [-Tenant <Guid>] <COMMON PARAMETERS>

    New-CsPartnerApplication -ApplicationTrustLevel <User | Application | Full> -MetadataUrl <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-Enabled <$true | $false>] [-Identity <XdsGlobalRelativeIdentity>] [-Tenant <Guid>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando dell'esempio 1 crea una nuova applicazione partner con identità (Identity) "MicrosoftExchange". In questo esempio la nuova applicazione partner utilizza l'URL di metadati https://autodiscover.litwareinc.com/metadata/json/1.

    New-CsPartnerApplication -Identity "MicrosoftExchange" -ApplicationTrustLevel "Full" -MetadataUrl"https://autodiscover.litwareinc.com/metadata/json/1"

## Esempio 2

Anche il comando riportato nell'esempio 2 crea una nuova applicazione con identità (Identity) "MicrosoftExchange". In questo caso però la nuova applicazione partner non utilizza un URL di metadati ed è configurata invece per l'utilizzo di un server OAuth predefinito. Per ottenere questo risultato, il comando utilizza il parametro UseOAuthServer anziché il parametro MetadataUrl.

    New-CsPartnerApplication -Identity "MicrosoftExchange" -ApplicationIdentifier "microsoft.exchange" -ApplicationTrustLevel "Full" -UseOAuthServer

## Descrizione dettagliata

In Lync Server 2013 l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 e Exchange 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che i due server possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, in genere non è necessario utilizzare un server dei token. Questi prodotti server, infatti, sono in grado di generare propri token di sicurezza. Sarà necessario tuttavia configurare l'altro prodotto server, ad esempio Exchange 2013, come applicazione partner. Sarà necessario inoltre configurare Lync Server 2013 come applicazione partner per l'altro prodotto server. In Lync Server 2013 le applicazioni partner vengono gestite utilizzando i cmdlet **CsPartnerApplication**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPartnerApplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsPartnerApplication** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>ApplicationIdentifier</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco dell'applicazione partner. Il valore di ApplicationIdentifier è fornito dall'applicazione server. Non è possibile utilizzare il parametro ApplicationIdentifier e il parametro MetadataUrl nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ApplicationTrustLevel</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>ApplicationTrustLevel</p></td>
<td><p>Specifica il livello di attendibilità tra Lync Server 2013 e l'applicazione partner. I valori consentiti sono:</p>
<p>* Full: l'applicazione partner viene considerata attendibile per rappresentare se stessa e qualsiasi utente dell'area di autenticazione. Questo è il valore predefinito.</p>
<p>* Application: l'applicazione partner viene considerata attendibile per rappresentare se stessa nell'area di autenticazione. Per rappresentare un utente, deve ottenere il consenso da un server dei token di sicurezza.</p>
<p>* User: l'applicazione partner deve ottenere il consenso da un server dei token di sicurezza per rappresentare un utente e non può rappresentare se stessa.</p>
<p>Il valore predefinito è Full.</p></td>
</tr>
<tr class="odd">
<td><p><em>CertificateFileData</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Percorso di un file di certificato che può essere assegnato all'applicazione partner, ad esempio:</p>
<p>-CertificateFileData &quot;C:\Certificates\PartnerApplication.cer&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateRawData</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Certificato (in formato con codifica Base64) che può essere assegnato all'applicazione partner. Per leggere i dati non elaborati di un certificato e quindi convertirli nel formato necessario, utilizzare comandi simili ai seguenti:</p>
<p>$x = Get-Content &quot;C:\Certificates\PartnerApplication.cer&quot; –Encoding Byte</p>
<p>$y = [Convert]::ToBase64String($x)</p>
<p>È quindi possibile utilizzare la sintassi seguente per assegnare i dati del certificato archiviati nella variabile $y:</p>
<p>-CertificateRawData $y</p></td>
</tr>
<tr class="odd">
<td><p><em>MetadataUrl</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>URL in cui vengono pubblicati i metadati WS-FederationMetadata dell'applicazione partner. Le applicazioni partner utilizzano i metadati per concordare i tipi di token che verranno scambiati e le chiavi che verranno utilizzate per la firma dei token.</p></td>
</tr>
<tr class="even">
<td><p><em>UseOAuthServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se specificato, indica che l'applicazione partner utilizzerà uno dei server OAuth pre-autorizzati anziché il server dei token di sicurezza incorporato nell'applicazione stessa.</p></td>
</tr>
<tr class="odd">
<td><p><em>AcceptSecurityIdentifierInformation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True ($True), è possibile utilizzare gli ID di sicurezza (SID) per l'autenticazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True, l'applicazione partner verrà abilitata e sarà disponibile per l'utilizzo immediato. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco della nuova applicazione partner.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Realm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Contenitore di sicurezza tra server. Per impostazione predefinita, Lync Server 2013 utilizza il dominio SIP predefinito come area di autenticazione OAuth.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per cui viene creata la nuova applicazione partner. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsPartnerApplication** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsPartnerApplication** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsPartnerApplication](get-cspartnerapplication.md)  
[Remove-CsPartnerApplication](remove-cspartnerapplication.md)  
[Set-CsPartnerApplication](set-cspartnerapplication.md)

