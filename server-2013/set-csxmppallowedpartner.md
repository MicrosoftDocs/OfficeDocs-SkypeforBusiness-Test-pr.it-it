---
title: Set-CsXmppAllowedPartner
TOCTitle: Set-CsXmppAllowedPartner
ms:assetid: 12586746-fbea-44b1-b656-a98028c90552
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204686(v=OCS.15)
ms:contentKeyID: 49299736
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsXmppAllowedPartner

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un partner consentito XMPP esistente. Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazione con standard aperto per lo scambio di messaggi tramite XML. Un partner consentito è un provider di messaggistica istantanea e presenza i cui utenti possono scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsXmppAllowedPartner [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsXmppAllowedPartner [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdditionalDomains <PSListModifier>] [-Confirm [<SwitchParameter>]] [-ConnectionLimit <UInt32>] [-Description <String>] [-EnableKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-PartnerType <Federated | PublicVerified | PublicUnverified>] [-ProxyFqdn <String>] [-SaslNegotiation <Required | Optional | NotSupported>] [-SupportDialbackNegotiation <$true | $false>] [-TlsNegotiation <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 disabilita la negoziazione di richiamata per il partner consentito XMPP contoso.com. Per ottenere questo risultato, viene incluso il parametro SupportDialbackNegotiation, che viene impostato su False ($False).

    Set-CsXmppAllowedPartner -Identity "contoso.com" -SupportDialbackNegotiation $False

## Esempio 2

Nell'esempio la negoziazione Simple Authentication and Security Layer (SASL) è abilitata e obbligatoria per tutti i partner consentiti XMPP dell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsXmppAllowedPartner** per restituire una raccolta di tutti i partner consentiti XMPP. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsXmppAllowedPartner**, che imposta il valore della proprietà SaslNegotiation per ogni partner della raccolta su Required.

    Get-CsXmppAllowedPartner | Set-CsXmppAllowedPartner -SaslNegotiation "Required"

## Esempio 3

Nell'esempio 3 viene aggiunto un nuovo dominio figlio, na.contoso.com, al partner consentito XMPP contoso.com. Per ottenere questo risultato, viene incluso il parametro AdditionalDomains, insieme alla sintassi @{Add="na.contoso.com"}. Questa sintassi aggiunge na.contoso.com a tutti gli altri domini attualmente inclusi nella proprietà AdditionalDomains.

    Set-CsXmppAllowedPartner -Identity "contoso.com" -AdditionalDomains @{Add="na.contoso.com"}

## Esempio 4

Nell'esempio 4 viene rimosso il dominio europe.contoso.com dalla raccolta di domini aggiuntivi assegnati al partner consentito XMPP contoso.com. Per rimuovere questo dominio, viene incluso il parametro AdditionalDomains con valore @{Remove="europe.contoso.com"}. Questa sintassi rimuove Europe.contoso.com dalla proprietà AdditionalDomains senza effetti sugli altri domini eventualmente archiviati in AdditionalDomains.

    Set-CsXmppAllowedPartner -Identity "contoso.com" -AdditionalDomains @{Remove="europe.contoso.com"}

## Esempio 5

Il comando riportato nell'esempio 5 rimuove il supporto del dominio figlio per il partner consentito XMPP contoso.com. Per ottenere questo risultato, viene incluso il parametro AdditionalDomains con valore $Null. In questo modo vengono eliminati tutti i domini attualmente inclusi nella proprietà.

    Set-CsXmppAllowedPartner -Identity "contoso.com" -AdditionalDomains $Null

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat.

Per consentire agli utenti di scambiare messaggi istantanei e informazioni sulla presenza con utenti su una rete XMPP, è necessario configurare la rete come partner consentito XMPP. È inoltre necessario assegnare agli utenti un criterio di accesso esterno che consenta l'accesso XMPP. Da progettazione, gli utenti sono autorizzati a comunicare con altri utenti su una rete XMPP riportata nell'elenco dei partner consentiti. Se non si desidera che gli utenti comunichino con utenti di una rete specifica, sarà necessario eliminare tale rete dall'elenco dei partner consentiti.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsXmppAllowedPartner"}

**Pannello di controllo di Lync Server:** per modificare i valori delle proprietà di un partner consentito XMPP esistente utilizzando il Pannello di controllo di Lync Server, fare clic su Accesso utente esterno e su Partner federati XMPP. Fare quindi doppio clic sul partner da modificare.

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
<td><p><em>AdditionalDomains</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Ulteriori domini XMPP appartenenti al partner consentito.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifica il numero massimo di connessioni simultanee a un partner specifico consentite.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire testo aggiuntivo relativo al partner consentito XMPP. Description può includere ad esempio informazioni di contatto per il partner.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableKeepAlive</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il partner XMPP deve inviare periodicamente pacchetti &quot;keep-alive&quot; per verificare che la connessione sia ancora attiva. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del partner consentito XMPP da modificare, ad esempio fabrikam.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>PartnerType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.PartnerType</p></td>
<td><p>Specifica la relazione tra Lync Server 2013 e il partner XMPP. I valori consentiti sono:</p>
<p>* Federated (il partner XMPP appartiene a un dominio federato)</p>
<p>* PublicVerified</p>
<p>* PublicUnverified</p>
<p>Il valore predefinito è PublicUnverified.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del server proxy utilizzato dal partner XMPP.</p></td>
</tr>
<tr class="odd">
<td><p><em>SaslNegotiation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.SaslNegotiation</p></td>
<td><p>Indica se è supportato il protocollo Simple Authentication and Security Layer (SASL), utilizzato per l'autenticazione server.</p>
<p>I valori consentiti sono:</p>
<p>* Required (deve essere supportata la negoziazione SASL)</p>
<p>* Optional (verrà utilizzato il protocollo SASL, se disponibile)</p>
<p>* NotSupported (la negoziazione SASL non sarà supportata)</p>
<p>Il valore predefinito è Required.</p></td>
</tr>
<tr class="even">
<td><p><em>SupportDialbackNegotiation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se verrà supportata la negoziazione di richiamata. Con questo tipo di negoziazione, quando il server A contatta il server B, non viene stabilita immediatamente una comunicazione. Il server B infatti tenta innanzitutto di verificare l'identità del server A contattando il server DNS autorevole per il dominio a cui il server A dichiara di appartenere.</p>
<p>Si noti che la negoziazione di richiamata non è sicura quanto il protocollo SASL o TLS. Viene invece utilizzata principalmente in situazioni in cui non è possibile verificare l'identità di un server tramite i certificati.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>TlsNegotiation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.TlsNegotiation</p></td>
<td><p>Indica se è supportato il protocollo Transport Layer Security (TLS), utilizzato per crittografare flussi di dati tra server.</p>
<p>I valori consentiti sono:</p>
<p>* Required (deve essere supportata la negoziazione TLS)</p>
<p>* Optional (verrà utilizzato il protocollo TLS, se disponibile)</p>
<p>* NotSupported (la negoziazione TLS non sarà supportata)</p>
<p>Il valore predefinito è Required.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsXmppAllowedPartner** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsXmppAllowedPartner** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)  
[New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)  
[Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)

