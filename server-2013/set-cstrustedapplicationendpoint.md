---
title: Set-CsTrustedApplicationEndpoint
TOCTitle: Set-CsTrustedApplicationEndpoint
ms:assetid: 6c2713f4-8e2c-48fc-9f27-07c1d6b87a18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398509(v=OCS.15)
ms:contentKeyID: 49300889
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrustedApplicationEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un contatto endpoint esistente per un'applicazione attendibile. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsTrustedApplicationEndpoint -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-Enabled <$true | $false>] [-EnabledForFederation <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrimaryLanguage <String>] [-SecondaryLanguages <MultiValuedProperty>] [-SipAddress <String>] [-Type <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio, viene modificato l'oggetto contatto endpoint con l'indirizzo SIP endpoint1@litwareinc.com. Si noti che il valore Identity inizia con la stringa sip: seguita dall'indirizzo SIP. Il parametro successivo, DisplayName, ha come valore "Endpoint 1" che modifica con quel valore il nome visualizzato del contatto.

    Set-CsTrustedApplicationEndpoint -Identity "sip:endpoint1@litwareinc.com" -DisplayName "Endpoint 1"

## ESEMPIO 2

In questo esempio viene modificato il numero visualizzato dell'endpoint dell'applicazione con nome visualizzato Endpoint 1. Il comando chiama innanzitutto il cmdlet **Get-CsTrustedApplicationEndpoint** con l'identità (Identity) Endpoint 1. In questo modo viene recuperato l'oggetto contatto endpoint con tale nome visualizzato. Questo oggetto viene quindi inviato tramite pipe al cmdlet **Set-CsTrustedApplicationEndpoint**, che cambia il valore di DisplayNumber sostituendolo in questo caso con (425)555-1212.

    Get-CsTrustedApplicationEndpoint -Identity "Endpoint 1" | Set-CsTrustedApplicationEndpoint -DisplayNumber "(425)555-1212"

## Descrizione dettagliata

L'endpoint di un'applicazione attendibile è un oggetto contatto Active Directory che consente il routing delle chiamate verso un'applicazione attendibile. Questo cmdlet modifica un oggetto contatto endpoint in Servizi di dominio Active Directory.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsTrustedApplicationEndpoint** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrustedApplicationEndpoint"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'identità (il nome distinto) o l'indirizzo SIP dell'endpoint dell'applicazione da modificare.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome visualizzato dell'oggetto contatto endpoint.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero telefonico del contatto come apparirà nella Rubrica.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il contatto è abilitato per Lync Server.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledForFederation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti federati hanno accesso a questo contatto.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il contatto è abilitato per VoIP aziendale.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica la posizione in cui vengono archiviate le sessioni di messaggistica istantanea del contatto. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero telefonico del contatto. Deve avere il formato TEL:&lt;numero&gt;, ad esempio TEL:+14255551212.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si include questo parametro, il cmdlet non modificherà solo l'oggetto contatto, ma restituirà il nuovo oggetto come risultato.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La lingua primaria utilizzata dall'applicazione attendibile. La lingua deve essere configurata utilizzando un valido codice lingua, quali en-US (Inglese U.S.), fr-FR (Francese), ecc.</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Una raccolta di lingue che può essere utilizzata per applicazioni attendibili. I valori devono essere configurati come elenco di codici lingua delimitati da virgole. Ad esempio, la seguente sintassi imposta Francese canadese e Francese come lingua secondaria: -SecondaryLanguages &quot;fr-CA&quot;,&quot;fr-FR&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Non è possibile modificare l'indirizzo SIP di un contatto. L'indirizzo SIP viene assegnato quando viene creato l'endpoint dell'applicazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro non è utilizzato con questo cmdlet.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact. Accetta input tramite pipeline di oggetti endpoint dell'applicazione attendibile.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationEndpoint](new-cstrustedapplicationendpoint.md)  
[Remove-CsTrustedApplicationEndpoint](remove-cstrustedapplicationendpoint.md)  
[Get-CsTrustedApplicationEndpoint](get-cstrustedapplicationendpoint.md)

