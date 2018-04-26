---
title: Set-CsProxyConfiguration
TOCTitle: Set-CsProxyConfiguration
ms:assetid: 2eb74d25-05b5-4901-aa92-eeda2f351e25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425796(v=OCS.15)
ms:contentKeyID: 49300061
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsProxyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione dei server proxy. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsProxyConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AcceptClientCompression <$true | $false>] [-AcceptServerCompression <$true | $false>] [-AllowPartnerPollingSubscribes <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisableNtlmFor2010AndLaterClients <$true | $false>] [-DnsCacheRecordCount <UInt32>] [-EnableLoggingAllMessageBodies <$true | $false>] [-EnableWhiteSpaceKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-LoadBalanceEdgeServers <$true | $false>] [-LoadBalanceInternalServers <$true | $false>] [-MaxClientCompressionCount <UInt32>] [-MaxClientMessageBodySizeKb <UInt32>] [-MaxKeepAliveInterval <UInt32>] [-MaxServerCompressionCount <UInt32>] [-MaxServerMessageBodySizeKb <UInt32>] [-OutgoingTlsCount <UInt32>] [-Realm <IRealmChoice>] [-RequestServerCompression <$true | $false>] [-TreatAllClientsAsRemote <$true | $false>] [-UseCertificateForClientToProxyAuth <$true | $false>] [-UseKerberosForClientToProxyAuth <$true | $false>] [-UseNtlmForClientToProxyAuth <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 tutte le impostazioni di configurazione dei proxy con identità (Identity) service:EdgeServer:atl-edge-001.litwareinc.com vengono modificate per accettare la compressione del server. A tale scopo, vengono chiamati il cmdlet **Set-CsProxyConfiguration** e il parametro AcceptServerCompression e il valore di quest'ultimo viene impostato su True.

    Set-CsProxyConfiguration -Identity service:EdgeServer:atl-edge-001.litwareinc.com -AcceptServerCompression $True

## ESEMPIO 2

Nell'esempio 2 vengono individuate tutte le impostazioni di configurazione dei proxy che accettano la compressione del server e quindi vengono modificate queste impostazioni per accettare anche la compressione del client. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsProxyConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di proxy in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà AcceptServerCompression è uguale a True. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsProxyConfiguration**, che imposta su True la proprietà AcceptClientCompression di ogni elemento della raccolta.

    Get-CsProxyConfiguration | Where-Object {$_.AcceptServerCompression -eq $True} | Set-CsProxyConfiguration -AcceptClientCompression $True

## ESEMPIO 3

Nell'esempio 3 viene mostrato come modificare tutte le impostazioni di proxy configurate nell'ambito del servizio. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsProxyConfiguration** e include il parametro Filter. Il valore di filtro "service:\*" garantisce che vengano restituite solo le impostazioni che hanno un'identità che inizia con il valore stringa "service:". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsProxyConfiguration**, che imposta su False la proprietà UseNtlmForClientToProxyAuth di ogni elemento della raccolta.

    Get-CsProxyConfiguration -Filter service:* | Set-CsProxyConfiguration -UseNtlmForClientToProxyAuth $False

## Descrizione dettagliata

Lync Server consente di gestire i server proxy tramite le impostazioni di configurazione dei server proxy. Queste impostazioni, che possono essere applicate sia nell'ambito globale che nell'ambito del servizio (anche se solo per il servizio server perimetrale e il servizio di registrazione), consentono di definire ad esempio quali protocolli di autenticazione devono essere utilizzati dagli endpoint client e se utilizzare la compressione sulle connessioni in ingresso e in uscita del server proxy. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni di configurazione dei server proxy. Come già indicato, è inoltre possibile creare ulteriori raccolte nell'ambito del servizio.

Il cmdlet **Set-CsProxyConfiguration** offre la possibilità di modificare le proprietà di una raccolta di impostazioni di configurazione del server proxy.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsProxyConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsProxyConfiguration"}

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
<td><p><em>AcceptClientCompression</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server proxy accetta tutte le richieste di compressione in entrata provenienti dagli endpoint client.</p></td>
</tr>
<tr class="even">
<td><p><em>AcceptServerCompression</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server proxy accetta tutte le richieste di compressione in entrata provenienti da altri server.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPartnerPollingSubscribes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, le applicazioni partner possono eseguire periodicamente il polling del servizio per ricercare cambiamenti di stato. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableNtlmFor2010AndLaterClients</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, gli utenti che accedono da Lync devono utilizzare il protocollo Kerberos per l'autenticazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>DnsCacheRecordCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di record che possono essere presenti nella cache di record DNS. Il valore predefinito è 3000.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLoggingAllMessageBodies</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Lync Server registrerà il contenuto di tutti i messaggi istantanei. Per motivi di privacy, il contenuto dei messaggi in genere viene eliminato e nei file di log vengono incluse solo informazioni sugli endpoint di comunicazione.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableWhiteSpaceKeepAlive</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (il valore predefinito), il server proxy si aspetta l'invio periodico da parte dei client di un messaggio contenente solo spazi (un messaggio vuoto senza contenuto) per segnalare che la connessione è ancora attiva.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione del server proxy da modificare. Per modificare le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per modificare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service: EdgeServer:atl-edge-001.litwareinc.com&quot;.</p>
<p>Se questo parametro non viene incluso, il cmdlet <strong>Set-CsProxyConfiguration</strong> modificherà automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ProxySettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>LoadBalanceEdgeServers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà utilizzato il bilanciamento del carico software per le richieste per i server perimetrali. Il valore predefinito è True ($True).</p></td>
</tr>
<tr class="odd">
<td><p><em>LoadBalanceInternalServers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà utilizzato il bilanciamento del carico software per le richieste per le funzioni di registrazione e per altri server interni. Il valore predefinito è True ($True).</p></td>
</tr>
<tr class="even">
<td><p><em>MaxClientCompressionCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di connessioni client-server che è possibile comprimere in un momento specifico; una volta superato questo limite, le connessioni non vengono compresse. Il valore della compressione può essere impostato su qualsiasi numero intero compreso tra 0 e 65535, inclusi. Il valore predefinito è 15000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxClientMessageBodySizeKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La dimensione massima consentita (in kilobyte) per il corpo del messaggio inviato da un endpoint client. Il valore predefinito è 128 e indica che i messaggi di dimensioni maggiori di 128 KB verranno rifiutati. La dimensione del corpo del messaggio client può essere impostata su qualsiasi numero intero compreso fra 64 e 256, inclusi.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxKeepAliveInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifica quanti minuti possono trascorrere prima che il server verifichi la validità della connessione con il client. Il valore predefinito è 20 minuti.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxServerCompressionCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di connessioni server-server che è possibile comprimere in un momento specifico; una volta superato questo limite, le connessioni non vengono compresse. Il valore della compressione server può essere impostato su qualsiasi numero intero compreso tra 0 e 65535, inclusi. Il valore predefinito è 1024.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxServerMessageBodySizeKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La dimensione massima consentita (in kilobyte) per il corpo del messaggio inviato da un altro server. Il valore predefinito è 5000 e indica che i messaggi di dimensioni maggiori di 5000 KB verranno rifiutati. La dimensione del corpo del messaggio server può essere impostata su qualsiasi numero intero compreso fra 1000 e 20000, inclusi.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutgoingTlsCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifica il numero massimo di connessioni Transport Layer Security (TLS) che possono essere utilizzate per ciascun server interno. Il numero minimo di connessioni TLS è 1 mentre il numero massimo è 4. Per impostazione predefinita, OutgoingTlsCount è impostato su 4.</p></td>
</tr>
<tr class="even">
<td><p><em>Realm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.IRealmChoice</p></td>
<td><p>Indica se le credenziali di sicurezza vengono elaborate dall'area di autenticazione predefinita del server proxy (servizi di comunicazione SIP ) o da un'area di autenticazione personalizzata. Le aree di autenticazione personalizzate devono essere specificate (e create) utilizzando il cmdlet <strong>New-CsSipProxyCustom</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestServerCompression</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server proxy richiede di utilizzare la compressione per tutte le connessioni in uscita verso altri server.</p></td>
</tr>
<tr class="even">
<td><p><em>TreatAllClientsAsRemote</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il server proxy funziona come se tutte le connessioni client fossero connessioni esterne che passano attraverso il server server perimetrale. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCertificateForClientToProxyAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), agli endpoint client è consentita l'autenticazione tramite certificati.</p></td>
</tr>
<tr class="even">
<td><p><em>UseKerberosForClientToProxyAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), gli endpoint client sono autorizzati a utilizzare il protocollo Kerberos per l'autenticazione. Anche se è un protocollo più sicuro di NTLM, Kerberos non può essere utilizzato se il client appartiene a un'area di autenticazione diversa da quella del server.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseNtlmForClientToProxyAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (il valore predefinito), gli endpoint client sono autorizzati a utilizzare il protocollo NTLM per l'autenticazione. Anche se è un protocollo meno sicuro di Kerberos, NTLM può essere utilizzato se il client appartiene a un dominio diverso da quello del server. Lo stesso non vale per l'autenticazione Kerberos.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings. Il cmdlet **Set-CsProxyConfiguration** accetta le istanze dell'oggetto impostazioni proxy inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsProxyConfiguration** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsProxyConfiguration](get-csproxyconfiguration.md)  
[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)

