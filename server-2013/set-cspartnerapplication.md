---
title: Set-CsPartnerApplication
TOCTitle: Set-CsPartnerApplication
ms:assetid: 29c8c511-157b-478e-814f-b911955a8251
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204755(v=OCS.15)
ms:contentKeyID: 49300004
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPartnerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un'applicazione partner esistente. Un'applicazione partner è un'applicazione con cui Skype for Business online può scambiare direttamente token di sicurezza senza dover passare attraverso un server dei token di sicurezza di terze parti. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> -MetadataUrl <String> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -CertificateRawData <String> -Identity <XdsGlobalRelativeIdentity> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -CertificateFileData <String> -Identity <XdsGlobalRelativeIdentity> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication -Identity <XdsGlobalRelativeIdentity> -UseOAuthServer <SwitchParameter> [-AcceptSecurityIdentifierInformation <$true | $false>] [-ApplicationTrustLevel <User | Application | Full>] [-Enabled <$true | $false>] [-Tenant <Guid>] <COMMON PARAMETERS>

    Set-CsPartnerApplication [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 disabilita l'applicazione partner MicrosoftExchange. Per ottenere questo risultato, la proprietà Enabled viene impostata su False ($False).

    Set-CsPartnerApplication -Identity "MicrosoftExchange" -Enabled $False

## Esempio 2

Nell'esempio 2 vengono disabilitate tutte le applicazioni partner attualmente in uso nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPartnerApplication** per restituire una raccolta di tutte le applicazioni partner. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. A sua volta il cmdlet **ForEach-Object** esegue il cmdlet **Set-CsPartnerApplication** su ogni applicazione della raccolta in modo da disabilitare tutte le applicazioni partner.

    Get-CsPartnerApplication | ForEach-Object {Set-CsPartnerApplication -Identity $_.Identity -Enabled $False}

## Esempio 3

Nell'esempio 3 vengono disabilitate tutte le applicazioni partner la cui proprietà ApplicationTrustLevel è impostata su User. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPartnerApplication** senza parametri per restituire una raccolta di tutte le applicazioni partner configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le applicazioni la cui proprietà ApplicationTrustLevel è uguale a "User". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che utilizza il cmdlet **Set-CsPartnerApplication** per selezionare tutti gli elementi della raccolta e impostare la proprietà Enabled su $False.

    Get-CsPartnerApplication | Where-Object {$_.ApplicationTrustLevel -eq "User"} | ForEach-Object {Set-CsPartnerApplication -Identity $_.Identity -Enabled $False}

## Descrizione dettagliata

In Skype for Business online l'autenticazione da server a server, ad esempio l'autenticazione che consente a Lync Server 2013 ed Exchange 2013 di condividere informazioni, viene eseguita utilizzando il protocollo di sicurezza OAuth. Per questo tipo di autenticazione in genere sono necessari tre server: i due server che devono comunicare tra loro (il server A e il server B) e un server dei token di sicurezza di terze parti. Se i server A e B devono comunicare tra loro, contattano il server dei token, noto anche come server OAuth, e ottengono token di sicurezza reciprocamente attendibili che i due server possono scambiarsi per provare la propria identità.

Se si utilizza una versione locale di Lync Server 2013 e si desidera comunicare con un altro prodotto server che supporta completamente il protocollo OAuth, ad esempio Exchange 2013 o Microsoft SharePoint 2013, in genere non è necessario utilizzare un server dei token. Questi prodotti server, infatti, sono in grado di generare propri token di sicurezza. Sarà necessario tuttavia configurare l'altro prodotto server, ad esempio Exchange 2013, come applicazione partner. Sarà necessario inoltre configurare Lync Server 2013 come applicazione partner per l'altro prodotto server. In Lync Server 2013 le applicazioni partner vengono gestite utilizzando i cmdlet **CsPartnerApplication**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPartnerApplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsPartnerApplication** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco dell'applicazione partner, ad esempio:</p>
<p>-Identity &quot;MicrosoftExchange&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>MetadataUrl</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>URL dei metadati di federazione del servizio token di sicurezza con le chiavi di firma, l'identificatore dell'autorità emittente e l'URL dell'endpoint dell'autorità emittente.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseOAuthServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, l'applicazione partner utilizzerà per l'autenticazione tra server il server OAuth configurato. Se invece non si specifica questo parametro, l'applicazione partner utilizzerà per l'autenticazione tra server il servizio token di sicurezza incorporato.</p></td>
</tr>
<tr class="even">
<td><p><em>AcceptSecurityIdentifierInformation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True ($True), è possibile utilizzare gli ID di sicurezza (SID) per l'autenticazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>ApplicationTrustLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ApplicationTrustLevel</p></td>
<td><p>Specifica il livello di attendibilità tra Lync Server 2013 e l'applicazione partner. I valori consentiti sono:</p>
<p>* Full: l'applicazione partner viene considerata attendibile per rappresentare se stessa e qualsiasi utente dell'area di autenticazione. Questo è il valore predefinito.</p>
<p>* Application: l'applicazione partner viene considerata attendibile per rappresentare se stessa nell'area di autenticazione. Per rappresentare un utente, deve ottenere il consenso da un server dei token di sicurezza.</p>
<p>* User: l'applicazione partner deve ottenere il consenso da un server dei token di sicurezza per rappresentare un utente e non può rappresentare se stessa.</p>
<p>Il valore predefinito è Full.</p></td>
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
<td><p>Se si imposta questo parametro su True, l'applicazione partner è disponibile per l'utilizzo con Lync Server 2013. Se invece si imposta questo parametro su False, l'applicazione partner continuerà a essere eseguita, ma non sarà in grado di comunicare con Lync Server finché la proprietà Enabled non verrà impostata su True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per l'applicazione partner da modificare. Ad esempio:</p>
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

Nessuno. Il cmdlet **Set-CsPartnerApplication** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPartnerApplication** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SSAuth.PartnerApplication\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsPartnerApplication](get-cspartnerapplication.md)  
[New-CsPartnerApplication](new-cspartnerapplication.md)  
[Remove-CsPartnerApplication](remove-cspartnerapplication.md)

