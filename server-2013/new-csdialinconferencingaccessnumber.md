---
title: New-CsDialInConferencingAccessNumber
TOCTitle: New-CsDialInConferencingAccessNumber
ms:assetid: c6d0536c-0ba3-45e0-affe-7ee00a070435
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398818(v=OCS.15)
ms:contentKeyID: 49301913
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingAccessNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo numero di accesso per le conferenze telefoniche con accesso esterno. Tali conferenze consentono agli utenti di utilizzare un "normale" telefono, un cellulare o entrambi (un dispositivo sulla rete PSTN), per partecipare alla parte audio di una conferenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDialInConferencingAccessNumber -Pool <Fqdn> -Regions <MultiValuedProperty> <COMMON PARAMETERS>

    New-CsDialInConferencingAccessNumber -HostingProviderProxyFqdn <Fqdn> <COMMON PARAMETERS>

    COMMON PARAMETERS: -DisplayNumber <String> -LineURI <String> -PrimaryLanguage <String> -PrimaryUri <String> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-PassThru <SwitchParameter>] [-ScopeToSite <SwitchParameter>] [-SecondaryLanguages <MultiValuedProperty>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene creato un nuovo numero di accesso per conferenze telefoniche con accesso esterno con URI primario sip:RedmondDialIn@litwareinc.com. Oltre al parametro PrimaryUri, il comando include anche i parametri che configurano il numero di telefono visualizzato in Lync (DisplayNumber), il numero di telefono nel formato E.164 (LineUri), il pool di registrazione a cui è assegnato il nuovo numero (-Pool), la lingua principale del numero (PrimaryLanguage) e l'area a cui è assegnato il numero (Regions).

    New-CsDialInConferencingAccessNumber -PrimaryUri "sip:RedmondDialIn@litwareinc.com" -DisplayNumber "1-800-555-1234" -LineUri "tel:+18005551234" -Pool atl-cs-001.litwareinc.com -PrimaryLanguage "en-US" -Regions "Redmond"

## Esempio 2

Il comando mostrato nell'esempio 2 è una variazione del comando nell'esempio 1, con la sola differenza che il comando mostrato in questo esempio assegna anche due lingue secondarie (francese canadese e francese) al nuovo numero di accesso alla conferenza telefonica con accesso esterno. Per assegnare queste lingue secondarie, viene incluso il parametro SecondaryLanguages insieme a un elenco con valori delimitati da virgole contenente le lingue da assegnare (fr-CA e fr-FR).

    New-CsDialInConferencingAccessNumber -PrimaryUri "sip:RedmondDialIn@litwareinc.com" -DisplayNumber "1-800-555-1234" -LineUri "tel:+18005551234" -Pool atl-cs-001.litwareinc.com -PrimaryLanguage "en-US" -Regions "Redmond" -SecondaryLanguages "fr-CA", "fr-FR"

## Esempio 3

Nell'esempio 3 viene creato un nuovo numero di accesso per conferenze telefoniche con accesso esterno nell'ambito del sito in cui è contenuto il pool principale dell'oggetto contatto. A tale scopo, il comando include il parametro ScopeToSite.

    New-CsDialInConferencingAccessNumber -PrimaryUri "sip:RedmondDialIn@litwareinc.com" -DisplayNumber "1-800-555-1234" -LineUri "tel:+18005551234" -Pool atl-cs-001.litwareinc.com -PrimaryLanguage "en-US" -Regions "Redmond" -ScopeToSite

## Descrizione dettagliata

Le conferenze telefoniche con accesso esterno consentono agli utenti di utilizzare qualsiasi tipo di telefono, ad esempio una linea terrestre standard, un telefono cellulare o un telefono VoIP (Voice over Internet Protocol), per partecipare alla parte audio di una conferenza online. In questo modo è possibile partecipare alla riunione anche non disponendo di un computer o di una connessione Internet. Gli utenti dispongono delle funzionalità audio complete: possono parlare con altri partecipanti e ascoltare tutto. Non sono invece in grado di visualizzare diapositive condivise, trasmissioni video o altri elementi visivi.

Per offrire agli utenti le funzionalità di conferenza telefonica con accesso esterno, è necessario creare numeri di accesso alle conferenze telefoniche con accesso esterno, ovvero dei numeri telefonici che gli utenti chiamano per collegarsi alla riunione. I numeri di accesso alle conferenze telefoniche con accesso esterno vengono creati utilizzando il cmdlet **New-CsDialInConferencingAccessNumber**. Quando si crea un nuovo numero di accesso alle conferenze telefoniche con accesso esterno, si crea in realtà un nuovo oggetto contatto in Servizi di dominio Active Directory. L'oggetto contatto viene utilizzato per rappresentare il numero di accesso e tutte le relative proprietà.

Durante la creazione di un nuovo numero telefonico con accesso esterno, è necessario includere i seguenti parametri: PrimaryUri, LineURI, Pool, DisplayNumber, PrimaryLanguage e Regions. Tutti questi parametri e i rispettivi valori risultano abbastanza immediati, probabilmente con una sola eccezione, ovvero Regions. Quando si crea un nuovo numero di accesso, questo numero deve essere associato a una o più aree. A sua volta, un'area non può essere associata a un numero di conferenza telefonica ad accesso esterno, purché l'area non compaia almeno in un dial plan. Se un'area compare nella proprietà DialInConferencingRegion di almeno un dial plan, può essere associata a un numero di accesso. In caso contrario, non può essere associata a un numero di accesso. Ciò significa semplicemente che è necessario innanzitutto creare un dial plan e specificare un'area corrispondente per poter creare un numero di accesso a una conferenza telefonica con accesso esterno.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsDialInConferencingAccessNumber** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingAccessNumber"}

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
<td><p><em>DisplayNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono visualizzato negli inviti alle riunioni e nella pagina Web della conferenza telefonica con accesso esterno. È possibile formattare la proprietà DisplayNumber a propria discrezione, ad esempio 1-800-555-1234, 1-(800)-555-1234 oppure 1.800.555.1234.</p></td>
</tr>
<tr class="even">
<td><p><em>HostingProviderProxyFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del provider che esegue l'hosting del servizio di conferenza con accesso esterno.</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il numero effettivo della conferenza telefonica ad accesso esterno. ﻿Specificare il parametro LineURI utilizzando la seguente sintassi: il prefisso tel: seguito dal segno più (+), a sua volta seguito dal codice paese, dall'indicativo di località e dal numero di telefono. Ad esempio: tel:+18005551234. Spazi, trattini, parentesi e altri caratteri non sono consentiti.</p>
<p>I parametri LineURI devono essere univoci nell'ambito di Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Pool principale del nuovo oggetto contatto.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Lingua principale utilizzata per gli annunci delle conferenze telefoniche ad accesso esterno. La lingua deve essere configurata utilizzando uno dei codici lingua per conferenze telefoniche con accesso esterno disponibili, ad esempio en-US per l'inglese americano, fr-FR per il francese e così via. Per restituire un elenco dei codici lingua disponibili, al prompt di Windows PowerShell digitare il seguente comando:</p>
<p>Get-CsDialInConferencingLanguageList | Select-Object -ExpandProperty Languages.</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP univoco da assegnare al nuovo oggetto contatto. Quando si specifica il parametro PrimaryUri, è necessario includere il prefisso &quot;sip:&quot;, ad esempio -PrimaryUri &quot;sip:RedmondDialIn@litwareinc.com&quot;. Si noti che il prefisso sip: deve essere immesso con lettere minuscole.</p></td>
</tr>
<tr class="odd">
<td><p><em>Regions</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Aree dei dial plan associate al numero telefonico con accesso esterno. Se l'area non è inclusa in almeno un dial plan, non può essere associata a un numero di accesso per conferenze telefoniche con accesso esterno. Per specificare più aree, utilizzare un elenco separato da virgole: -Regions &quot;Northwest&quot;, &quot;Southwest&quot;</p></td>
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
<td><p>Nome visualizzato in Active Directory per il nuovo oggetto contatto. Si tratta del nome che verrà visualizzato anche in Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare attraverso la pipeline un oggetto contatto che rappresenta il nuovo numero di accesso alla conferenza telefonica ad accesso esterno. Per impostazione predefinita, il cmdlet <strong>New-CsDialInConferencingAccessNumber</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>ScopeToSite</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, il nuovo numero verrà assegnato allo stesso sito del pool principale dell'oggetto contatto. Se il parametro ScopeToSite non è incluso, il nuovo numero verrà assegnato all'ambito globale.</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Raccolta facoltativa di lingue che è possibile utilizzare per gli annunci delle conferenze telefoniche con accesso esterno. Le lingue secondarie devono essere configurate come un elenco di codici lingua delimitati da virgole; ad esempio, la sintassi riportata di seguito imposta il francese canadese e il francese come lingue secondarie: -SecondaryLanguages &quot;fr-CA&quot;, &quot;fr-FR&quot;.</p>
<p>Per un singolo numero di accesso possono esistere un massimo di quattro lingue secondarie.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant Skype for Business online per cui viene creato il nuovo numero di accesso per conferenze telefoniche con accesso esterno. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID tenant per ciascun tenant eseguendo questo comando:</p>
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

Nessuno. Il cmdlet **New-CsDialInConferencingAccessNumber** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsDialInConferencingAccessNumber** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.Xds.AccessNumber.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md)  
[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

