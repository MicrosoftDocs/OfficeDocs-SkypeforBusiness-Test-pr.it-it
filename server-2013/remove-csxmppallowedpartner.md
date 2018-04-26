---
title: Remove-CsXmppAllowedPartner
TOCTitle: Remove-CsXmppAllowedPartner
ms:assetid: 858a07a3-891e-4678-b989-6339b0978427
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205055(v=OCS.15)
ms:contentKeyID: 49301206
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsXmppAllowedPartner

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un partner consentito XMPP esistente. Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni con standard aperto per lo scambio di messaggi tramite XML. Un partner consentito è un provider di messaggistica istantanea e informazioni sulla presenza i cui utenti possono scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsXmppAllowedPartner -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene eliminato il partner consentito XMPP con l'identità "contoso.com".

    Remove-CsXmppAllowedPartner -Identity "contoso.com"

## Esempio 2

Il comando riportato nell'esempio 2 elimina tutti i partner consentiti XMPP. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsXmppAllowedPartner** per restituire una raccolta di tutti i partner consentiti XMPP attualmente in uso nell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsXmppAllowedPartner**, che elimina ogni partner della raccolta.

    Get-CsXmppAllowedPartner | Remove-CsXmppAllowedPartner

## Esempio 3

Nell'esempio 3 vengono eliminati tutti i partner consentiti XMPP di tipo PublicUnverified. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsXmppAllowedPartner** per restituire una raccolta di tutti i partner consentiti. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i partner in cui la proprietà PartnerType è uguale a "PublicUnverified". I partner che soddisfano questo criterio vengono quindi inviati tramite pipe al cmdlet **Remove-CsXmppAllowedPartner**, che li elimina.

    Get-CsXmppAllowedPartner | Where-Object {$_.PartnerType -eq "PublicUnverified"} | Remove-CsXmppAllowedPartner

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat.

Per consentire agli utenti di scambiare messaggi istantanei e informazioni sulla presenza con utenti su una rete XMPP, è necessario configurare la rete come partner consentito XMPP. È inoltre necessario assegnare agli utenti un criterio di accesso esterno che consenta l'accesso XMPP. Da progettazione, gli utenti sono autorizzati a comunicare con altri utenti su una rete XMPP riportata nell'elenco dei partner consentiti. Se non si desidera che gli utenti comunichino con utenti di una rete specifica, sarà necessario eliminare tale rete dall'elenco dei partner consentiti.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsXmppAllowedPartner"}

**Pannello di controllo di Lync Server:** per rimuovere un partner consentito XMPP utilizzando il Pannello di controllo di Lync Server, fare clic su Accesso utenti esterni e quindi su Partner federati XMPP. Selezionare il partner da rimuovere, fare clic su Modifica e quindi su Elimina.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del partner consentito XMPP da eliminare. Ad esempio:</p>
<p>-Identity &quot;fabrikam.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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

Il cmdlet **Remove-CsXmppAllowedPartner** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsXmppAllowedPartner** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)  
[New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)  
[Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

