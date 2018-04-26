---
title: Test-CsMcxPushNotification
TOCTitle: Test-CsMcxPushNotification
ms:assetid: db81339b-f79a-418a-b29d-8596dff7a210
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690043(v=OCS.15)
ms:contentKeyID: 49302183
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsMcxPushNotification

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica il funzionamento del servizio notifica Push. Tale servizio (servizio notifica Push Apple e servizio notifica Push Microsoft) consente di inviare notifiche su eventi quali nuovi messaggi istantanei o nuovi messaggi in segreteria telefonica a dispositivi mobili come iPhone e Windows Phone, anche se l'applicazione Lync in tali dispositivi è attualmente sospesa o eseguita in background. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Test-CsMcxPushNotification -AccessEdgeFqdn <String> [-Certificate <X509Certificate2>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di testare il servizio notifica Push a cui si accede tramite il server perimetrale atl-edge-001.litwareinc.com.

    Test-CsMcxPushNotification -AccessEdgeFqdn "atl-edge-001.litwareinc.com"

## Descrizione dettagliata

Il servizio notifica Push Apple e il servizio notifica Push Lync Server consentono agli utenti con telefoni Apple iPhone o Windows Phone in cui è in esecuzione Lync di ricevere notifiche relative agli eventi di Lync anche quando Lync Server è sospeso o in esecuzione in background. Gli utenti possono ad esempio ricevere notifiche per eventi come i seguenti:

\- Inviti a una nuova sessione di conferenza o messaggistica istantanea

\- Nuovi messaggi istantanei

\- Nuovi messaggi in segreteria telefonica

Senza il servizio notifica Push, gli utenti riceverebbero queste notifiche solo quando Lync Server è in esecuzione come applicazione attiva e non è in background.

Il cmdlet Test-CsMcxPushNotification consente agli amministratori di verificare che il servizio notifica Push funzioni.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Test-CsMcxPushNotification** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p><em>AccessEdgeFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo dell'Access Edge Server utilizzato per la connessione al servizio notifica Push.</p></td>
</tr>
<tr class="even">
<td><p><em>Certificate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Security.Cryptography.X509Certificates.X509Certificate2</p></td>
<td><p>Consente di specificare un certificato X509 da utilizzare per l'autenticazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non irreversibile che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome della variabile.</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando analogo al seguente:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsMcxPushNotification** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsMcxPushNotification** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

