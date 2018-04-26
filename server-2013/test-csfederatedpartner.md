---
title: Test-CsFederatedPartner
TOCTitle: Test-CsFederatedPartner
ms:assetid: 1f56bf80-37b4-4520-b8a5-da0740a894a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398281(v=OCS.15)
ms:contentKeyID: 49299891
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsFederatedPartner

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la possibilità di connessione a un dominio federato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsFederatedPartner -Domain <String> -TargetFqdn <String> [-Certificate <X509Certificate2>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-ProxyFqdn <String>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di verificare la connessione tra il server proxy di accesso locale (accessproxy.litwareinc.com) e il dominio federato Fabrikam.com.

    Test-CsFederatedPartner -TargetFqdn accessproxy.litwareinc.com -Domain fabrikam.com

## ESEMPIO 2

Nell'esempio 2 viene illustrato come testare la connessione tra il dominio e il Servizio di notifica push di Lync Server. Per la riuscita del test è necessario aver configurato questo servizio come provider di hosting e aver aggiunto push.lync.com all'elenco dei domini consentiti. Per ulteriroi informazioni, vedere [Configurazione delle notifiche push in Lync Server 2013](lync-server-2013-configuring-for-push-notifications.md).

    Test-CsFederatedPartner -TargetFqdn accessproxy.litwareinco.com -Domain push.lync.com -ProxyFqdn sipfed.online.lync.com

## ESEMPIO 3

Nell'esempio 3 viene verificata la connettività per tutti i domini dell'elenco dei domini consentiti. A tale scopo, nel comando viene inizialmente utilizzato il cmdlet Get-CsAllowedDomain per recuperare una raccolta di tutti i domini consentiti. La raccolta viene quindi inviata tramite pipe al cmdlet ForEach-Object, che a sua volta esegue il cmdlet Test-CsFederatedPartner su ogni dominio della raccolta.

    Get-CsAllowedDomain | ForEach-Object {Test-CsFederatedPartner -TargetFqdn accessproxy.litwareinc.com -Domain $_.Identity}

## Descrizione dettagliata

**Test-CsFederatedPartner** consente di verificare la possibilità di connessione al dominio di un partner federato. ‏Per verificare la connettività ad un dominio, è necessario che tale dominio compaia nella raccolta dei domini (federati) consentiti. I domini possono essere aggiunti all'elenco dei domini consentiti utilizzando il cmdlet **New-CsAllowedDomain**.

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsFederatedPartner"}

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
<td><p><em>Domain</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio federato. Ad esempio: -Domain &quot;fabrikam.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del server proxy di accesso utilizzato dall'organizzazione per il traffico SIP federato. Il parametro TargetFqdn deve essere impostato sul lato interno del server proxy a cui è diretto il traffico SIP federato.</p></td>
</tr>
<tr class="odd">
<td><p><em>Certificate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Security.Cryptography.X509Certificates.X509Certificate2</p></td>
<td><p>Consente di fornire un certificato X509 per l'autenticazione quando si esegue la connessione al dominio federato.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando si specifica questo parametro, l'output dettagliato relativo all'esecuzione del cmdlet viene archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome di una variabile. Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando simile al seguente:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del server proxy di accesso utilizzato dall'organizzazione federata.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **Test-CsFederatedPartner** non accetta input tramite pipeline.

## Tipi restituiti

**Test-CsFederatedPartner** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Get-CsAllowedDomain](get-csalloweddomain.md)

