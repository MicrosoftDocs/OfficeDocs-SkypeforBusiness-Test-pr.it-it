---
title: Set-CsXmppGatewayConfiguration
TOCTitle: Set-CsXmppGatewayConfiguration
ms:assetid: 2b90d563-a3fe-45bd-81da-210a7459411b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204769(v=OCS.15)
ms:contentKeyID: 49300023
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsXmppGatewayConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni di configurazione dei gateway XMPP in uso nell'organizzazione. Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazione con standard aperto per lo scambio di messaggi tramite XML. I gateway XMPP consentono agli utenti di Lync Server 2013 di scambiare messaggi istantanei e informazioni sulla presenza con utenti di provider di servizi di messaggistica istantanea e presenza che utilizzano XMPP. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsXmppGatewayConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsXmppGatewayConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-ConnectionLimit <UInt32>] [-DialbackPassphrase <String>] [-EnableLoggingAllMessageBodies <$true | $false>] [-Force <SwitchParameter>] [-KeepAliveInterval <UInt32>] [-PartnerConnectionLimit <UInt32>] [-StreamEstablishmentTimeout <UInt32>] [-StreamInactivityTimeout <UInt32>] [-SubscriptionRefreshInterval <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene modificata la proprietà ConnectionLimit della raccolta globale di impostazioni dei gateway XMPP.

    Set-CsXmppGatewayConfiguration -Identity "global" -ConnectionLimit 1200

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat.

Il gateway XMPP che consente a Lync 2013 di comunicare con gli utenti su una rete XMPP è stato rilasciato in origine come componente aggiuntivo di Microsoft Lync Server 2010. In Lync Server 2013 invece questa funzionalità è incorporata nel software. Gli utenti pertanto possono comunicare con gli utenti XMPP purché vengano eseguite le operazioni seguenti:

  -   
    Configurazione delle impostazioni del gateway XMPP.

  -   
    Configurazione dell'altra rete XMPP, ad esempio Google Talk, come partner XMPP consentito.

Si noti che in Lync Server 2013 è disponibile un solo insieme globale di impostazioni di configurazione XMPP. Non è possibile abilitare o disabilitare in modo selettivo XMPP per un sito o per un pool di registrazione specifico. In realtà non è possibile in assoluto abilitare o disabilitare XMPP, poiché questo protocollo è sempre abilitato. Se non si desidera che gli utenti comunichino con reti XMPP, rimuovere tutti i partner XMPP consentiti. Gli utenti possono comunicare con una rete XMPP solo se tale rete è stata configurata come partner consentito.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsXmppGatewayConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsXmppGatewayConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero totale di connessioni simultanee consentite per tutti partner XMPP. Il valore predefinito è 1000.</p></td>
</tr>
<tr class="odd">
<td><p><em>DialbackPassphrase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Password utilizzata per la connessione a un partner XMPP su una connessione di richiamata TCP. Con la richiamata TCP, il partner contatta il gateway XMPP e quindi riaggancia. Il gateway XMPP richiama il partner e la sessione di comunicazione ha inizio.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLoggingAllMessageBodies</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Lync Server 2013 registrerà il contenuto di tutti i messaggi istantanei. Per motivi di privacy, il contenuto dei messaggi in genere viene eliminato e nei file di log vengono incluse solo informazioni sugli endpoint di comunicazione.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione dei gateway XMPP da modificare. Poiché è possibile disporre di una sola istanza globale di queste impostazioni, non è necessario specificare un'identità quando viene chiamato il cmdlet <strong>Set-CsXmppGatewayConfiguration</strong>. Se lo si preferisce, è comunque possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepAliveInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di secondi che possono trascorrere prima che il partner debba inviare un messaggio &quot;keep-alive&quot;. Questo tipo di messaggio verifica semplicemente che la connessione sia ancora attiva. Se questo intervallo di tempo scade prima della ricezione di un messaggio keep-alive, la connessione verrà chiusa. Il valore predefinito è 300 secondi.</p></td>
</tr>
<tr class="odd">
<td><p><em>PartnerConnectionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero totale di connessioni simultanee consentite per un singolo partner XMPP. Il valore predefinito è 20.</p></td>
</tr>
<tr class="even">
<td><p><em>StreamEstablishmentTimeout</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di secondi allocati per consentire al partner XMPP di stabilire un flusso XMPP. Se viene superato questo periodo di timeout, la connessione verrà terminata automaticamente. Il valore predefinito è 60 secondi.</p></td>
</tr>
<tr class="odd">
<td><p><em>StreamInactivityTimeout</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di secondi in cui un flusso XMPP può essere inattivo prima che la connessione venga terminata automaticamente. Il valore predefinito è 600 secondi (10 minuti).</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriptionRefreshInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di secondi che possono trascorrere prima che il partner debba aggiornare la sottoscrizione relativa alla presenza. Il valore predefinito è 28800 secondi (8 ore).</p></td>
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

Il cmdlet **Set-CsXmppGatewayConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppGatewaySettings inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsXmppGatewayConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppGatewaySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsXmppGatewayConfiguration](get-csxmppgatewayconfiguration.md)

