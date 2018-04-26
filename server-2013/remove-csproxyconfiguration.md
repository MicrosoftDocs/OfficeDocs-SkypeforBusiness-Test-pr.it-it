---
title: Remove-CsProxyConfiguration
TOCTitle: Remove-CsProxyConfiguration
ms:assetid: 738f731c-4d62-4395-bdc3-3f5e5738f443
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398553(v=OCS.15)
ms:contentKeyID: 49300975
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsProxyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione del server proxy. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsProxyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare le impostazioni di configurazione proxy con identità service:EdgeServer:atl-edge-litwareinc.com.

    Remove-CsProxyConfiguration -Identity service:EdgeServer:atl-edge-011.litwareinc.com 

## ESEMPIO 2

Con l'esempio 2 vengono eliminate tutte le impostazioni di configurazione proxy applicate nell'ambito del servizio. Per eseguire questa operazione, il comando chiama per prima cosa il cmdlet **Get-CsProxyConfiguration** con il parametro Filter. Il valore del filtro "service:\*" garantisce la restituzione delle sole impostazioni proxy con un'identità che inizia con il valore stringa "service:". Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsProxyConfiguration**, che elimina ciascun elemento nella raccolta.

    Get-CsProxyConfiguration -Filter "service:*" | Remove-CsProxyConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione proxy che considerano tutti i client come client remoti. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsProxyConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione del server proxy attualmente in uso. La raccolta viene quindi inviata tramite pipe a **Where-Object**, che seleziona solo le impostazioni in cui la proprietà TreatAllClientsAsRemote è uguale a True. Questo sottoinsieme di impostazioni di configurazione proxy viene quindi inviato tramite pipe al cmdlet **Remove-CsProxyConfiguration**, che rimuove tutte le impostazioni della raccolta.

    Get-CsProxyConfiguration | Where-Object {$_.TreatAllClientsAsRemote -eq $True} | Remove-CsProxyConfiguration

## Descrizione dettagliata

Lync Server consente di gestire i server proxy tramite le impostazioni di configurazione dei server proxy. Queste impostazioni, che possono essere applicate sia nell'ambito globale che nell'ambito del servizio (anche se solo per il servizio server perimetrale e il servizio di registrazione), consentono di definire ad esempio quali protocolli di autenticazione devono essere utilizzati dagli endpoint client e se utilizzare la compressione sulle connessioni in ingresso e in uscita del server proxy. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni di configurazione dei server proxy. Come già indicato, è inoltre possibile creare ulteriori raccolte nell'ambito del servizio.

Qualsiasi nuova impostazione del server proxy creata può essere successivamente rimossa utilizzando il cmdlet **Remove-CsProxyConfiguration**. Il cmdlet **Remove-CsProxyConfiguration** può anche essere eseguito sulla raccolta globale. In questo caso, però, le impostazioni globali non vengono rimosse, perché Lync Server non consente di rimuovere le impostazioni globali. Tutte le proprietà nella raccolta globale saranno invece riportate ai valori predefiniti. Ad esempio, per impostazione predefinita le impostazioni del server proxy consentono ai client di utilizzare il protocollo Kerberos per l'autenticazione. È possibile modificare le impostazioni globali per disabilitare l'uso di Kerberos. Tuttavia, se si esegue il cmdlet **Remove-CsProxyConfiguration** sulla raccolta globale, la proprietà in questione (UseKerberosForClientToProxyAuth) viene riportata al valore predefinito e Kerberos viene nuovamente abilitato per l'uso come protocollo di autenticazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsProxyConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsProxyConfiguration"}

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
<td><p>Identificatore univoco per le impostazioni di configurazione del server proxy da rimuovere, ad esempio: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;.</p>
<p>È inoltre possibile eseguire il cmdlet <strong>Remove-CsProxyConfiguration</strong> sulle impostazioni globali. In tal caso, però, le impostazioni globali non saranno rimosse. Le proprietà nella raccolta globale saranno invece riportate ai valori predefiniti.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings. Il cmdlet **Remove-CsProxyConfiguration** accetta le istanze dell'oggetto impostazioni proxy inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsProxyConfiguration** consente invece di eliminare le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsProxyConfiguration](get-csproxyconfiguration.md)  
[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

