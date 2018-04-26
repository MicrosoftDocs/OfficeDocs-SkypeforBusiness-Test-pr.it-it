---
title: Get-CsXmppAllowedPartner
TOCTitle: Get-CsXmppAllowedPartner
ms:assetid: 6d031b38-325a-4196-998f-c473390f2055
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204981(v=OCS.15)
ms:contentKeyID: 49300904
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsXmppAllowedPartner

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui partner XMPP autorizzati a comunicare con l'organizzazione. Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni con standard aperto per lo scambio di messaggi tramite XML. I partner consentiti sono provider di messaggistica istantanea e informazioni sulla presenza che sono stati autorizzati a scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Lync Server 2013Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsXmppAllowedPartner [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsXmppAllowedPartner [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutti i partner consentiti XMPP configurati per l'utilizzo nell'organizzazione.

    Get-CsXmppAllowedPartner

## Esempio 2

Nell'esempio 2 vengono restituite informazioni su un singolo partner consentito XMPP, ovvero il partner con identità (Identity) xmpp.contoso.com.

    Get-CsXmppAllowedPartner -Identity "xmpp.contoso.com"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutti i partner consentiti XMPP la cui identità (Identity) termina con il valore stringa ".org", ad esempio xmpp.contoso.org e xmpp.fabrikam.org.

    Get-CsXmppAllowedPartner - Filter "*.org"

## Esempio 4

Il comando riportato nell'esempio 4 restituisce informazioni su tutti i partner consentiti XMPP per cui è necessaria la negoziazione Simple Authentication and Security Layer. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsXmppAllowedPartner** per restituire informazioni su tutti i partner XMPP consentiti. I partner restituiti vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo i partner in cui la proprietà SaslNegotiation è uguale a Required.

    Get-CsXmppAllowedPartner | Where-Object {$_.SaslNegotiation -eq "Required"}

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat.

Per consentire agli utenti di scambiare messaggi istantanei e informazioni sulla presenza con utenti su una rete XMPP, è necessario configurare la rete come partner consentito XMPP. È inoltre necessario assegnare agli utenti un criterio di accesso esterno che consenta l'accesso XMPP. Da progettazione, gli utenti sono autorizzati a comunicare con altri utenti su una rete XMPP riportata nell'elenco dei partner consentiti. Se non si desidera che gli utenti comunichino con utenti di una rete specifica, sarà necessario eliminare tale rete dall'elenco dei partner consentiti.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsXmppAllowedPartner"}

**Pannello di controllo di Lync Server:** per visualizzare informazioni sui partner consentiti XMPP nel Pannello di controllo di Lync Server, fare clic su Accesso utenti esterni e quindi su Partner federati XMPP.

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
<td><p>Consente di utilizzare caratteri jolly per specificare l'identità del partner o dei partner consentiti XMPP da restituire. Ad esempio, il valore di filtro &quot;*.org&quot; restituisce una raccolta di tutti i partner consentiti XMPP la cui identità (Identity)termina con il valore stringa &quot;.org&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del partner consentito XMPP da restituire, ad esempio fabrikam.com. Se non si specifica né questo parametro né il parametro Filter, vengono restituiti tutti i partner consentiti XMPP configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi ai partner consentiti XMPP dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsXmppAllowedPartner** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsXmppAllowedPartner** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)  
[Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)  
[Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

