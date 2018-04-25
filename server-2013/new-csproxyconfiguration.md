---
title: New-CsProxyConfiguration
TOCTitle: New-CsProxyConfiguration
ms:assetid: 5133470e-1d77-4958-8844-a091336b2a3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398335(v=OCS.15)
ms:contentKeyID: 49300522
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsProxyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione dei server proxy. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsProxyConfiguration -Identity <XdsIdentity> [-AcceptClientCompression <$true | $false>] [-AcceptServerCompression <$true | $false>] [-AllowPartnerPollingSubscribes <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisableNtlmFor2010AndLaterClients <$true | $false>] [-DnsCacheRecordCount <UInt32>] [-EnableLoggingAllMessageBodies <$true | $false>] [-EnableWhiteSpaceKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LoadBalanceEdgeServers <$true | $false>] [-LoadBalanceInternalServers <$true | $false>] [-MaxClientCompressionCount <UInt32>] [-MaxClientMessageBodySizeKb <UInt32>] [-MaxKeepAliveInterval <UInt32>] [-MaxServerCompressionCount <UInt32>] [-MaxServerMessageBodySizeKb <UInt32>] [-OutgoingTlsCount <UInt32>] [-Realm <IRealmChoice>] [-RequestServerCompression <$true | $false>] [-TreatAllClientsAsRemote <$true | $false>] [-UseCertificateForClientToProxyAuth <$true | $false>] [-UseKerberosForClientToProxyAuth <$true | $false>] [-UseNtlmForClientToProxyAuth <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione dei server proxy per il servizio EdgeServer:atl-edge-001.litwareinc.com. Queste nuove impostazioni utilizzano tutti i valori delle proprietà del server proxy predefinito, ad eccezione dei due valori seguenti: RequestServerCompression, che è impostato su True, e MaxClientMessageBodySizeKb, che è impostato su 256. Si noti che il comando avrà esito negativo se le impostazioni del server proxy sono già state configurate per il servizio EdgeServer:atl-edge-001.litwareinc.com.

    New-CsProxyConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com" -RequestServerCompression $True -MaxClientMessageBodySizeKb 256

## ESEMPIO 2

Con i comandi riportati nell'esempio 2 viene illustrato come creare una raccolta di impostazioni dei server proxy presenti, inizialmente, solo in memoria. A tale scopo, il primo comando chiama il cmdlet **New-CsProxyConfiguration** con due parametri: Identity, che indica l'identità delle impostazioni, e InMemory, che indica che le nuove impostazioni devono essere create solo in memoria. L'oggetto risultante viene archiviato nella variabile $x.

Dopo la creazione di queste impostazioni virtuali, i comandi 2 e 3 consentono di modificare i valori rispettivamente delle proprietà RequestServerCompression e MaxClientMessageBodySizeKb. Il comando 4 infine viene utilizzato per trasformare le impostazioni di configurazione dei server proxy virtuali in una raccolta di impostazioni effettiva, applicata al servizio EdgeServer:atl-edge-001.litwareinc.com. Questo ultimo comando è obbligatorio. Se non si chiama il cmdlet **Set-CsProxyConfiguration**, a EdgeServer:atl-edge-001.litwareinc.com non verrà applicata alcuna impostazione e le impostazioni virtuali verranno eliminate non appena si termina la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsProxyConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com" -InMemory
    $x.RequestServerCompression = $True 
    $x.MaxClientMessageBodySizeKb = 256
    Set-CsProxyConfiguration -Instance $x

## Descrizione dettagliata

Lync Server consente di gestire i server proxy in uso tramite le impostazioni di configurazione dei server proxy. Tali impostazioni, che possono essere applicate sia nell'ambito globale che nell'ambito del servizio (anche se soltanto per i servizi server perimetrale e di registrazione), consentono di controllare elementi quali i protocolli di autenticazione che possono essere utilizzati dagli endpoint client e se verrà utilizzata o meno la compressione per le connessioni dei server proxy in ingresso e in uscita. Quando si installa Lync Server, viene automaticamente creata una raccolta globale di impostazioni di configurazione dei server proxy. Come fatto notare, è inoltre possibile creare ulteriori raccolte nell'ambito del servizio. Queste nuove raccolte vengono create tramite il cmdlet **New-CsProxyConfiguration**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsProxyConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsProxyConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione del server proxy da creare. Le impostazioni di configurazione del server proxy possono essere create unicamente nell'ambito del servizio e solo per i servizi server perimetrale e di registrazione. Non è possibile creare le impostazioni nell'ambito globale; analogamente, non è consentito creare impostazioni nell'ambito del servizio nel caso in cui il servizio in questione ospiti già una raccolta di impostazioni del server proxy. Se ad esempio il servizio Registrar:atl-cs-001.litwareinc.com ospita già impostazioni di server proxy, il comando che tenta di creare nuove impostazioni per tale servizio avrà esito negativo.</p>
<p>Per specificare l'identità delle nuove impostazioni per il server proxy, utilizzare la sintassi: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>AcceptClientCompression</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server proxy accetta tutte le richieste di compressione in entrata provenienti dagli endpoint client.</p></td>
</tr>
<tr class="odd">
<td><p><em>AcceptServerCompression</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server proxy accetta tutte le richieste di compressione in entrata provenienti da altri server.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPartnerPollingSubscribes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, le applicazioni partner possono eseguire periodicamente il polling del servizio per ricercare cambiamenti di stato. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableNtlmFor2010AndLaterClients</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, gli utenti che accedono da Lync devono utilizzare il protocollo Kerberos per l'autenticazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>DnsCacheRecordCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di record che possono essere presenti nella cache di record DNS. Il valore predefinito è 3000.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLoggingAllMessageBodies</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Microsoft Lync Server registrerà il contenuto di tutti i messaggi istantanei. Per motivi di privacy, il contenuto dei messaggi in genere viene eliminato e nei file di log vengono incluse solo informazioni sugli endpoint di comunicazione.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableWhiteSpaceKeepAlive</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), nel server proxy è previsto l'invio periodico da parte dei client di un messaggio contenente solo spazi (messaggio vuoto senza contenuto) per indicare che la connessione è ancora attiva.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<td><p>Indica se le credenziali di sicurezza vengono elaborate dall'area di autenticazione del server proxy predefinita (Servizio di comunicazioni SIP) o da un'area di autenticazione personalizzata. Le aree di autenticazione personalizzate devono essere specificate, e create, tramite l'utilizzo del cmdlet <strong>New-CsSipProxyCustom</strong>.</p></td>
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
<td><p>Se impostato su True, il server proxy funziona come se tutte le connessioni client fossero connessioni esterne che attraversano server perimetrale che esegue il servizio Access Edge. Il valore predefinito è False.</p></td>
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
<td><p>Se impostato su True (valore predefinito), agli endpoint client è consentita l'autenticazione tramite il protocollo NTLM. Sebbene NTLM sia un protocollo meno sicuro di Kerberos, può essere utilizzato anche se il client fa parte di un dominio differente rispetto a quello del server, Questa condizione non vale per l'autenticazione Kerberos.</p></td>
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

Nessuno. Il cmdlet **New-CsProxyConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsProxyConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsProxyConfiguration](get-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

