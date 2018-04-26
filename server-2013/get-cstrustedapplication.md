---
title: Get-CsTrustedApplication
TOCTitle: Get-CsTrustedApplication
ms:assetid: e6623931-3bac-4146-92a9-4465396e9fe6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399025(v=OCS.15)
ms:contentKeyID: 49302292
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le impostazioni di un'applicazione attendibile. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTrustedApplication [-ApplicationId <String>] [-TrustedApplicationPoolFqdn <String>] <COMMON PARAMETERS>

    Get-CsTrustedApplication [-Identity <ExternalApplicationIdentity>] <COMMON PARAMETERS>

    Get-CsTrustedApplication [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate le informazioni relative a tutte le applicazioni attendibili definite all'interno della distribuzione di Lync Server.

    Get-CsTrustedApplication

## ESEMPIO 2

Nell'esempio 2 viene recuperata l'applicazione attendibile con Identity TrustPool.litwareinc.com/urn:application:tapp2. Si noti che è possibile omettere il prefisso urn:application: in quanto il cmdlet **Get-CsTrustedApplication** lo aggiunge automaticamente e recupera l'applicazione corretta.

    Get-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2

## ESEMPIO 3

Nell'esempio 3 vengono recuperate tutte le applicazioni attendibili con identità che corrispondono alla stringa con caratteri jolly specificata come valore Filter. In tal caso, con un valore Filter di \*trust\*, il comando consente di recuperare tutte le applicazioni attendibili con la stringa "trust" all'interno del parametro Identity. La stringa può essere contenuta in qualsiasi parte del parametro Identity, del nome di dominio completo del pool o dell'ID dell'applicazione. Pertanto, questo comando consente di recuperare le applicazioni attendibili con identità quali TrustedPool.litwareinc.com/urn:application:application1, Pool1.litwareinc.com/urn:application:trustedapp e Pool1.litwareinc.com/urn:application:trust.

    Get-CsTrustedApplication -Filter *trust*

## ESEMPIO 4

Nell'esempio 4 vengono restituiti gli stessi risultati dell'esempio 2 (in cui era stato specificato soltanto il parametro Identity). L'unica differenza tra i due esempi è rappresentata dal fatto che nell'esempio 2 viene recuperata l'applicazione attendibile in base al parametro Identity che è costituito dal nome di dominio completo del pool attendibile seguito dall'ID dell'applicazione. In questo esempio, invece, l'ID dell'applicazione e il nome di dominio completo del pool attendibile vengono immessi come valori di due parametri diversi: ApplicationId e TrustedApplicationPoolFqdn.

    Get-CsTrustedApplication -ApplicationId tapp2 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com

## ESEMPIO 5

Nell'esempio 5 vengono recuperate le applicazioni attendibili nel pool TrustPool.litwareinc.com. Nell'esempio viene innanzitutto richiamato il cmdlet **Get-CsTrustedApplication** che consente di restituire una raccolta di tutte le applicazioni attendibili definite all'interno della distribuzione di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, grazie al quale la raccolta viene esaminata elemento per elemento in modo da trovare gli elementi il cui valore della proprietà TrustedApplicationPoolFqdn è uguale a (-eq) TrustPool.litwareinc.com.

    Get-CsTrustedApplication | Where-Object {$_.TrustedApplicationPoolFqdn -eq "TrustPool.litwareinc.com"}

## Descrizione dettagliata

Un'applicazione attendibile è un'applicazione sviluppata da terzi cui viene assegnato lo stato di attendibile per essere eseguita come parte di Lync Server, sebbene non sia una parte integrata del prodotto. Il cmdlet consente di recuperare le impostazioni di Globally Routable User Agent URI (GRUU) e della porta per una o più applicazioni attendibili.

Quando si utilizza questo cmdlet per recuperare una singola applicazione attendibile, è necessario fornire un valore per il parametro Identity. Il valore Identity è il nome di dominio completo (FQDN) del pool in cui l'applicazione è disponibile seguito da una barra (/) e dall'ID dell'applicazione. Ad esempio, TrustPool.litwareinc.com/tapp2, in cui TrustPool.litwareinc.com è il nome di dominio completo del pool e tapp2 è l'ID dell'applicazione. Se si recupera un'applicazione richiamando questo cmdlet, verrà visualizzato un ID simile al seguente: TrustPool.litwareinc.com/urn:application:tapp2. Si noti il prefisso urn:application: prima del nome dell'applicazione (tapp2). Tale prefisso è parte dell'identità ma non è richiesto quando si specifica il valore del parametro Identity.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsTrustedApplication** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplication\\b"}

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
<td><p><em>ApplicationId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'applicazione. Può eventualmente, ma non necessariamente, includere il prefisso dell'ID dell'applicazione. I valori ApplicationId urn:application:tapp1 e tapp1 ad esempio restituiranno entrambi la stessa applicazione. Se si fornisce un valore per ApplicationId, non è possibile fornire un valore per il parametro Identity. Tuttavia, è necessario fornire un valore per il parametro TrustedApplicationPoolFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una stringa con caratteri jolly che consente di recuperare le applicazioni attendibili in base ai valori Identity corrispondenti alla stringa con caratteri jolly fornita. Le identità sono costituite da un nome di dominio completo del pool dell'applicazione attendibile seguito da una barra (/) e dall'ID dell'applicazione attendibile. Il valore Filter corrisponderà a qualsiasi parte dell'identità, del nome di dominio completo o dell'ID dell'applicazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>L'identificatore univoco dell'applicazione attendibile che si desidera recuperare. I valori Identity devono essere immessi nel formato &lt;FQDN pool&gt;/&lt;ID applicazione&gt;, dove FQDN pool è il nome di dominio completo del pool in cui risiede l'applicazione e ID applicazione è il nome dell'applicazione. Se si specifica un valore per Identity, non è possibile specificare ApplicationID o TrustedApplicationPoolFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo del pool dell'applicazione attendibile in cui l'applicazione risiede. Se si fornisce un valore per TrustedApplicationPoolFqdn, non è possibile fornire un valore per il parametro Identity. Tuttavia, è necessario fornire un valore per il parametro ApplicationID.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di restituire un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayTrustedApplication.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplication](new-cstrustedapplication.md)  
[Remove-CsTrustedApplication](remove-cstrustedapplication.md)  
[Set-CsTrustedApplication](set-cstrustedapplication.md)

