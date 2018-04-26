---
title: Set-CsLisServiceProvider
TOCTitle: Set-CsLisServiceProvider
ms:assetid: 3fe2878c-6ad2-4b7f-a844-e978c263163f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425911(v=OCS.15)
ms:contentKeyID: 49300316
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisServiceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea o modifica le informazioni sul servizio Web fornito dal provider del routing di rete Enhanced 9-1-1 (E9-1-1) per la verifica delle località. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLisServiceProvider -CertFileName <String> -Password <SecureString> -ServiceProviderName <String> -ValidationServiceUrl <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Uno dei parametri obbligatori quando si crea una voce per il servizio Web di un provider del routing di rete E9-1-1 è una stringa sicura contenente la password per accedere al file del certificato. Per questo motivo, la prima riga di questo esempio è una chiamata al cmdlet **Read-Host**. Il cmdlet **Read-Host** richiede un'immissione da parte dell'utente. Viene specificato il parametro AsSecureString, che visualizzerà come asterischi (\*) l'input mentre viene immesso. Il risultato di questo comando è stato assegnato alla variabile $p. Il risultato è una stringa sicura, ovvero una versione crittografata del testo immesso dall'utente. In altri termini, quando viene eseguito, questo comando richiede l'immissione della password per il servizio Web e archivia tale password nella variabile $p.

Una volta fornita la password, è possibile creare un oggetto in grado di accedere al servizio Web. Per ottenere questo risultato, viene utilizzato il cmdlet **Set-CsLisServiceProvider**. Vengono specificati numerosi parametri. Il primo è il nome del provider (in questo caso, E911Provider). Quindi viene specificato il valore https://www.911contoso.com/validation/ per la proprietà ValidationServiceUrl. Si noti che deve trattarsi di un "sito sicuro" e quindi avere il prefisso https invece che http. A questo punto, viene immesso il nome del file contenente il certificato utilizzato per accedere a questo servizio Web (C:\\MS-Contoso-Cert.pfx). Infine, per il parametro Password viene specificata la variabile $p (che contiene una stringa sicura con la password del servizio Web).

    $p = Read-Host -AsSecureString
    Set-CsLisServiceProvider -ServiceProviderName E911Provider -ValidationServiceUrl https://www.911contoso.com/validation/ -CertFileName C:\MS-Contoso-Cert.pfx -Password $p

## Descrizione dettagliata

In una implementazione di VoIP aziendale che prevede E9-1-1, le chiamate di emergenza devono passare attraverso un provider del routing di rete E9-1-1 in modo da poter essere poi correttamente instradate al punto PSAP (Public Safety Answering Point) appropriato. Negli Stati Uniti, un PSAP è un ente che si occupa di indirizzare le chiamate al servizio di emergenza più vicino, come, ad esempio, la polizia, i vigili del fuoco e il servizio ambulanze. Per effettuare questo servizio, il provider deve ricevere dall'organizzazione un elenco di località da verificare e convalidare sulla base dello stradario ufficiale. Questo cmdlet consente di creare o modificare le informazioni sul provider, inclusi il nome del provider, l'URL del servizio Web che l'organizzazione utilizzerà per inviare l'elenco di località e un certificato e una password per il servizio Web sicuro.

Non è possibile definire più di un provider di servizi per ogni implementazione E9-1-1. Questo cmdlet avrà esito negativo se non è in grado di risolvere l'URL e le informazioni di sicurezza per il servizio Web.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsLisServiceProvider** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisServiceProvider"}

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
<td><p><em>CertFileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome e il percorso completo del file del certificato. Questo file deve avere un'estensione PFX.</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Security.SecureString</p></td>
<td><p>Una stringa di sicurezza contenente la password necessaria per accedere al certificato nel file protetto da password. Per creare le stringhe di sicurezza, utilizzare il cmdlet <strong>ConvertTo-SecureString</strong> o il cmdlet <strong>Read-Host</strong> con il parametro AsSecureString.</p></td>
</tr>
<tr class="odd">
<td><p><em>ServiceProviderName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome del provider del routing di rete E9-1-1.</p></td>
</tr>
<tr class="even">
<td><p><em>ValidationServiceUrl</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'URL del servizio Web. Deve essere un URL sicuro che inizia con il prefisso https://.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Accetta input tramite pipeline da oggetti provider di servizi LIS (Location Information Server).

## Tipi restituiti

Questo cmdlet consente di creare o modificare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisServiceProvider](remove-cslisserviceprovider.md)  
[Get-CsLisServiceProvider](get-cslisserviceprovider.md)

