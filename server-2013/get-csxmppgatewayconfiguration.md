---
title: Get-CsXmppGatewayConfiguration
TOCTitle: Get-CsXmppGatewayConfiguration
ms:assetid: 4c9ee876-de89-420c-bda9-9901cef47799
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204869(v=OCS.15)
ms:contentKeyID: 49300483
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsXmppGatewayConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione dei gateway XMPP in uso nell'organizzazione. Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazione con standard aperto per lo scambio di messaggi tramite XML. I gateway XMPP consentono agli utenti di Lync Server 2013 di scambiare messaggi istantanei e informazioni sulla presenza con utenti di provider di messaggistica istantanea e presenza che utilizzano XMPP. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsXmppGatewayConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsXmppGatewayConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Nell'esempio 1 vengono restituite informazioni sulle impostazioni di gateway XMPP attualmente in uso nell'organizzazione. Poiché Lync Server 2013 supporta solo una singola raccolta globale di impostazioni dei gateway, non è necessario includere il parametro Identity per ottenere informazioni sulle impostazioni globali.

    Get-CsXmppGatewayConfiguration

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat.

Il gateway XMPP che consente a Lync 2013 di comunicare con gli utenti su una rete XMPP è stato rilasciato in origine come componente aggiuntivo di Microsoft Lync Server 2010. In Lync Server 2013 invece questa funzionalità è incorporata nel software. Gli utenti pertanto possono comunicare con gli utenti XMPP purché vengano eseguite le operazioni seguenti:

  -   
    Configurazione delle impostazioni del gateway XMPP.

  -   
    Configurazione dell'altra rete XMPP, ad esempio Google Talk, come partner XMPP consentito.

Si noti che in Lync Server 2013 è disponibile un solo insieme globale di impostazioni di configurazione XMPP. Non è possibile abilitare o disabilitare in modo selettivo XMPP per un sito o per un pool di registrazione specifico. In realtà non è possibile in assoluto abilitare o disabilitare XMPP, poiché questo protocollo è sempre abilitato. Se non si desidera che gli utenti comunichino con reti XMPP, rimuovere tutti i partner XMPP consentiti. Gli utenti possono comunicare con una rete XMPP solo se tale rete è stata configurata come partner consentito.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsXmppGatewayConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsXmppGatewayConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare valori con caratteri jolly per fare riferimento a una raccolta di impostazioni di configurazione dei gateway XMPP. Poiché è possibile disporre di una sola istanza globale di queste impostazioni, il parametro Filter non è necessario. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Filter &quot;g*&quot;</p>
<p>Questa sintassi recupera tutte le impostazioni di configurazione dei gateway XMPP la cui identità inizia con la lettera &quot;g&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione dei gateway XMPP. Dal momento che è possibile disporre di una sola istanza globale di tali impostazioni, non è necessario specificare un'identità nella chiamata al cmdlet <strong>Get-CsXmppGatewayConfiguration</strong>. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi ai gateway XMPP dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsXmppGatewayConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsXmppGatewayConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppGatewaySettings.

## Vedere anche

#### Ulteriori risorse

[Set-CsXmppGatewayConfiguration](set-csxmppgatewayconfiguration.md)

