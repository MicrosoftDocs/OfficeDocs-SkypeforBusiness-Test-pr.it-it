---
title: Request-CsCertificate
TOCTitle: Request-CsCertificate
ms:assetid: 24e8ba6f-6023-4c03-a594-5b40784fd16a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425723(v=OCS.15)
ms:contentKeyID: 49299956
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Request-CsCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di richiedere certificati da utilizzare con i server che eseguono Lync Server e i ruoli del server. Consente inoltre di verificare lo stato delle richieste di certificato esistenti e, se necessario, di annullarne una o tutte. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Request-CsCertificate -New <SwitchParameter> -Type <CertType[]> [-AllSipDomain <SwitchParameter>] [-CA <String>] [-CaAccount <String>] [-CaPassword <String>] [-City <String>] [-ClientEKU <$true | $false>] [-ComputerFqdn <Fqdn>] [-Country <String>] [-DomainName <String>] [-FriendlyName <String>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-KeyAlg <RSA | ECDH_P256 | ECDH_P384 | ECDH_P521>] [-KeySize <Int32>] [-Organization <String>] [-OU <String>] [-Output <String>] [-PrivateKeyExportable <$true | $false>] [-State <String>] [-Template <String>] <COMMON PARAMETERS>

    Request-CsCertificate -List <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Retrieve <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Clear <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 crea una nuova richiesta di certificato: si mette in contatto con CA atl-ca-001.litwareinc.com\\myca e richiede un nuovo certificato WebServicesExternal.

    Request-CsCertificate -New -Type WebServicesExternal -CA "atl-ca-001.litwareinc.com\myca"

## ESEMPIO 2

Nell'esempio 2 vengono elencate tutte le richieste di certificati in sospeso effettuate utilizzando il cmdlet **Request-CsCertificate**.

    Request-CsCertificate -List

## ESEMPIO 3

Nell'Esempio 3 viene utilizzato il parametro Output per creare una richiesta di certificato offline.

    Request-CsCertificate -New -Type WebServicesExternal -Output C:\Certificates\WebServicesExternal.cer

## ESEMPIO 4

L'esempio 4 è un esempio più dettagliato e realistico dell'utilizzo del cmdlet Request-CsCertificate. Questo esempio richiede un certificato da utilizzare con Lync Server Standard Edition.

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Standard Edition Certficate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-cs-001.litwareinc.com,atl-ext.litwareinc.com"

## ESEMPIO 5

Nell'Esempio 5, viene richiesto un certificato del pool da utilizzare con la versione Enterprise Edition di Lync Server

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Enterprise Edition Pool Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "pool1.litwareinc.com,pool1int.litwareinc.com,pool1ext.litwareinc.com"

## ESEMPIO 6

Nell'esempio 6 viene mostrato come richiedere un certificato per il server perimetrale (server perimetrale) interno.

    Request-CsCertificate -New -Type Internal -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Internal Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com, ap.litwareinc.com"

## ESEMPIO 7

L'Esempio 7 è una variazione del comando riportato nell'Esempio 6, in questo caso, tuttavia, si richiede un certificato per un server perimetrale esterno.

    Request-CsCertificate -New -Type AccessEdgeExternal,DataEdgeExternal,AudioVideoAuthentication -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "External Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com,ap.litwareinc.com,dp.litwareinc.com,atl-edge-001"

## Descrizione dettagliata

In Lync Server i certificati vengono utilizzati come mezzo per verificare le identità di server e ruoli del server. Un server perimetrale (server perimetrale) ad esempio si basa sui certificati per verificare che il computer con cui sta comunicando sia realmente un Front End Server e viceversa. Per implementare completamente Lync Server, è necessario che ai ruoli del server appropriati siano assegnati i certificati appropriati.

Un modo per richiedere i certificati da utilizzare con Lync Server è quello di utilizzare il cmdlet **Request-CsCertificate**. Anche se è possibile utilizzare altri strumenti standard di Windows per richiedere i certificati da utilizzare con Lync Server, uno dei vantaggi principali offerti dal cmdlet **Request-CsCertificate** è rappresentato dal fatto che il cmdlet analizzerà la topologia prima di contattare l'autorità di certificazione (CA). In base all'analisi, il cmdlet **Request-CsCertificate** richiederà automaticamente un certificato con i campi del nome soggetto e del nome alternativo del soggetto appropriati.

Il cmdlet **Request-CsCertificate** è stato progettato per richiedere i certificati da utilizzare specificamente con Lync Server. Non è stato progettato per essere uno strumento di gestione dei certificati generico.

Oltre che per richiedere nuovi certificati, questo cmdlet può essere utilizzato per esaminare le eventuali richieste di certificati in sospeso, purché tali richieste siano state effettuate mediante il cmdlet **Request-CsCertificate**. Il cmdlet **Request-CsCertificate** può essere utilizzato inoltre per eliminare richieste di certificati in sospeso, purché tali richieste siano state effettuate mediante il cmdlet.

Mentre si tenta di recuperare le richieste di certificati, si potrebbe ricevere un messaggio di errore in presenza di richieste revocate. Il cmdlet **Request-CsCertificate** attualmente supporta solo i tipi di richiesta seguenti: Issued, Denied e Pending. Se si riscontrano problemi dovuti a un certificato revocato, utilizzare un comando simile al seguente per eliminare la richiesta revocata (dove 224 rappresenta l'ID della richiesta di certificato revocata):

Request-CsCertificate –Clear –RequestID 224

Dopo di che si dovrebbe essere in grado di recuperare le richieste di certificato.

Utenti autorizzati a utilizzare questo cmdlet: il cmdlet **Request-CsCertificate** può essere utilizzato localmente da un amministratore locale che disponga dei diritti per l'autorità di certificazione specificata. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Request-CsCertificate"}

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
<td><p><em>Clear</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, elimina qualsiasi richiesta di certificato in sospeso effettuata utilizzando il cmdlet <strong>Request-CsCertificate</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>List</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, elenca qualsiasi richiesta di certificato in sospeso effettuata utilizzando il cmdlet <strong>Request-CsCertificate</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>New</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, indica che si desidera richiedere un nuovo certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>Retrieve</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, recupera qualsiasi richiesta di certificato in sospeso effettuata utilizzando il cmdlet <strong>Request-CsCertificate</strong> e tenta di completare l'operazione e di importare il certificato richiesto.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo di certificato richiesto. Di seguito sono elencati alcuni tipi di certificati:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (solo Microsoft Lync Online 2010)</p>
<p>ProvisionService (solo Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Ad esempio, questa sintassi richiede un nuovo certificato Default: -Type Default.</p>
<p>È possibile specificare più tipi in un singolo comando separando i tipi di certificato con virgole:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>AllSipDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando si specifica questo parametro, tutti i domini SIP vengono aggiunti automaticamente al campo Nome alternativo soggetto dei certificati. Se invece non si specifica questo parametro, solo il dominio SIP primario viene aggiunto per impostazione predefinita. È tuttavia possibile specificare domini aggiuntivi utilizzando il parametro DomainName.</p></td>
</tr>
<tr class="odd">
<td><p><em>CA</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) dell'Autorità di certificazione (CA). Ad esempio: -CA &quot;atl-ca-001.litwareinc.com\myca&quot;. Per ottenere un elenco di Autorità di certificazione note, digitare quanto segue nel prompt di Windows PowerShell e premere INVIO:</p>
<p>certutil</p>
<p>La proprietà Config restituita da Certutil indica il percorso dell'Autorità di certificazione.</p></td>
</tr>
<tr class="even">
<td><p><em>CaAccount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'account dell'utente che richiede il nuovo certificato, nel formato nome_dominio\nome_utente. Ad esempio: -CaAccount &quot;litwareinc\kenmyer&quot;. Se non viene specificato, il cmdlet <strong>Request-CsCertificate</strong> utilizzerà le credenziali dell'utente che ha eseguito l'accesso durante la richiesta del nuovo certificato.</p></td>
</tr>
<tr class="odd">
<td><p><em>CaPassword</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Password per l'utente che richiede il nuovo certificato (specificata utilizzando il parametro CaAccount).</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Città in cui verrà distribuito il certificato.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientEKU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo parametro su True se è necessario utilizzare il certificato per l'autenticazione client. Questo tipo di autenticazione è obbligatorio se si desidera che gli utenti siano in grado di scambiare messaggi istantanei con utenti che dispongono di account AOL. La parte EKU del nome del parametro è l'abbreviazione di &quot;utilizzo chiavi avanzato&quot;; il campo dell'utilizzo chiavi avanzato elenca gli utilizzi validi per il certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del computer per il quale viene richiesto il certificato. Quando è presente, questo parametro fa in modo che il cmdlet <strong>Request-CsCertificate</strong> si connetta all'archivio di gestione centrale per individuare il computer specificato. È sempre necessario utilizzare il nome del computer quando si richiede un certificato, anche se si richiede un certificato per il pool. Il cmdlet <strong>Request-CsCertificate</strong> aggiungerà automaticamente il nome del pool al nome soggetto per tutti i certificati ottenuti utilizzando questo cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Paese/area geografica in cui verrà distribuito il certificato.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Elenco separato da virgole di nomi di dominio completi che devono essere aggiunti al campo Nome alternativo soggetto del certificato. Ad esempio:</p>
<p>-DomainName &quot;atl-cs-001.litwareinc.com, atl-cs-002.litwareinc.com,atl-cs-003.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>FriendlyName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome assegnato all'utente che semplifica l'identificazione del certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Request-CsCertificate</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del controller di dominio in cui vengono archiviate le impostazioni globali. Se le impostazioni globali vengono archiviate nel contenitore di sistema in Servizi di dominio Active Directory questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali vengono archiviate nel contenitore di configurazione, è possibile utilizzare qualsiasi controller di dominio e questo parametro può essere omesso.</p></td>
</tr>
<tr class="even">
<td><p><em>KeyAlg</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.X509Certificates.KeyAlgorithmIdentifier</p></td>
<td><p>Indica il tipo di algoritmo di crittografia da utilizzare nella creazione delle chiavi pubbliche e private per il nuovo certificato. Tra gli algoritmi della chiave validi compaiono:</p>
<p>RSA</p>
<p>ECDH_P256</p>
<p>ECDH_P384</p>
<p>ECDH_P521</p></td>
</tr>
<tr class="odd">
<td><p><em>KeySize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Indica la dimensione (in bit) della chiave privata utilizzata dal certificato. Le dimensioni di chiave maggiori sono più sicure, ma richiedono un maggiore overhead per essere decodificate.</p>
<p>Dimensioni di chiave valide sono 1024, 2048 e 4096. Ad esempio: -KeySize 2048.</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'organizzazione che richiede il nuovo certificato. Ad esempio: -Organization &quot;Litwareinc&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Unità organizzativa di Active Directory per il computer che verrà assegnata al nuovo certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>Output</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file del certificato. Se si vuole creare una richiesta di certificato offline utilizzare il parametro Output e specificare un percorso file per la richiesta di certificato, ad esempio: -Output C:\Certificates\NewCertificate.pfx. Creerà un file di richiesta certificato che può essere inviato come posta elettronica ad una autorità di certificazione per essere elaborato.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo parametro su True se si desidera rendere esportabile la chiave privata del certificato. Quando una chiave privata è esportabile, è possibile copiare il certificato ed utilizzarlo su più computer.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero identificativo associato alla richiesta di certificato. Il parametro RequestID consente di elencare, recuperare o eliminare un singolo certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Stato degli Stati Uniti in cui verrà distribuito il certificato. Ad esempio: -State WA.</p></td>
</tr>
<tr class="odd">
<td><p><em>Template</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il modello di certificato da utilizzare quando viene generato il nuovo certificato, ad esempio: -Template &quot;WebServer&quot;. È necessario installare il modello richiesto sull'Autorità di certificazione. Si noti che il valore immesso deve essere il nome del modello e non il nome visualizzato del modello.</p></td>
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

Nessuno. Il cmdlet **Request-CsCertificate** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Request-CsCertificate** invece consente di gestire le istanze dell'oggetto Microsoft.Rtc.Management.Deployment.CertificateReference.

## Vedere anche

#### Ulteriori risorse

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

