---
title: New-CsXmppAllowedPartner
TOCTitle: New-CsXmppAllowedPartner
ms:assetid: 02f8525a-d8ec-49d8-805b-e76c5449c553
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204631(v=OCS.15)
ms:contentKeyID: 49299509
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsXmppAllowedPartner

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo partner consentito XMPP. Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni con standard aperto per lo scambio di messaggi tramite XML. Un partner consentito è un provider di messaggistica istantanea e informazioni sulla presenza i cui utenti sono stati autorizzati a scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsXmppAllowedPartner -Domain <String> <COMMON PARAMETERS>

    New-CsXmppAllowedPartner -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdditionalDomains <PSListModifier>] [-Confirm [<SwitchParameter>]] [-ConnectionLimit <UInt32>] [-Description <String>] [-EnableKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PartnerType <Federated | PublicVerified | PublicUnverified>] [-ProxyFqdn <String>] [-SaslNegotiation <Required | Optional | NotSupported>] [-SupportDialbackNegotiation <$true | $false>] [-TlsNegotiation <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo partner consentito XMPP: contoso.com. In questo esempio la proprietà PartnerType è impostata su "PublicVerified".

    New-CsXmppAllowedPartner -Identity "contoso.com" -PartnerType "PublicVerified"

## Esempio 2

Nell'esempio 2 viene creato un nuovo partner consentito XMPP con identità (Identity) fabrikam.com. Oltre al dominio radice (fabrikam.com), è inclusa la proprietà AdditionalDomains per consentire il supporto del dominio figlio research.fabrikam2.com.

    New-CsXmppAllowedPartner -Identity "fabrikam.com" -AdditionalDomains "research.fabrikam2.com"

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat.

Per consentire agli utenti di scambiare messaggi istantanei e informazioni sulla presenza con utenti su una rete XMPP, è necessario configurare la rete come partner consentito XMPP. È inoltre necessario assegnare agli utenti un criterio di accesso esterno che consenta l'accesso XMPP. Da progettazione, gli utenti sono autorizzati a comunicare con altri utenti su una rete XMPP riportata nell'elenco dei partner consentiti. Se non si desidera che gli utenti comunichino con utenti di una rete specifica, sarà necessario eliminare tale rete dall'elenco dei partner consentiti.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsXmppAllowedPartner"}

**Pannello di controllo di Lync Server:** per creare un nuovo partner consentito XMPP utilizzando il Pannello di controllo di Lync Server, fare clic su Accesso utenti esterni, Partner federati XMPP e quindi Nuovo.

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
<td><p>Dominio primario del partner consentito XMPP, ad esempio:</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>È possibile specificare il dominio primario utilizzando il parametro Domain o Identity. Non è possibile tuttavia utilizzare entrambi i parametri nello stesso comando.</p>
<p>Per specificare ulteriori domini, utilizzare il parametro AdditionalDomains.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Dominio primario del partner consentito XMPP, ad esempio:</p>
<p>-Identity &quot;fabrikam.com&quot;</p>
<p>È possibile specificare il dominio primario utilizzando il parametro Identity o Domain. Non è possibile tuttavia utilizzare entrambi i parametri nello stesso comando.</p>
<p>Per specificare ulteriori domini, utilizzare il parametro AdditionalDomains.</p></td>
</tr>
<tr class="odd">
<td><p><em>AdditionalDomains</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Ulteriori domini XMPP appartenenti al partner consentito. È possibile specificare più domini utilizzando le virgole per separare i nomi, ad esempio:</p>
<p>-AdditionalDomains &quot;fabrikam2.com&quot;,&quot;fabrikam3.com&quot;</p></td>
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
<td><p>Indica se il partner XMPP deve inviare periodicamente pacchetti &quot;keep-alive&quot; per verificare che la connessione sia ancora attiva.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>PartnerType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.PartnerType</p></td>
<td><p>Specifica la relazione tra Lync Server 2013 e il partner XMPP. I valori consentiti sono:</p>
<p>* Federated (il partner XMPP appartiene a un dominio federato)</p>
<p>* PublicVerified</p>
<p>* PublicUnverified</p>
<p>Il valore predefinito è PublicUnverified.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del server proxy utilizzato dal partner XMPP.</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>SupportDialbackNegotiation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se verrà supportata la negoziazione di richiamata. Con questo tipo di negoziazione, quando il server A contatta il server B, non viene stabilita immediatamente una comunicazione. Il server B infatti tenta innanzitutto di verificare l'identità del server A contattando il server DNS autorevole per il dominio a cui il server A dichiara di appartenere.</p>
<p>Si noti che la negoziazione di richiamata non è sicura quanto il protocollo SASL o TLS. Viene utilizzata principalmente in situazioni in cui non è possibile verificare l'identità di un server tramite i certificati.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>TlsNegotiation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.TlsNegotiation</p></td>
<td><p>Indica se è supportato il protocollo Transport Layer Security (TLS), utilizzato per crittografare flussi di dati tra server.</p>
<p>I valori consentiti sono:</p>
<p>* Required (deve essere supportata la negoziazione TLS)</p>
<p>* Optional (verrà utilizzato il protocollo TLS, se disponibile)</p>
<p>* NotSupported (la negoziazione TLS non sarà supportata). Il valore predefinito è Required.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsXmppAllowedPartner** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsXmppAllowedPartner** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)  
[Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)  
[Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

