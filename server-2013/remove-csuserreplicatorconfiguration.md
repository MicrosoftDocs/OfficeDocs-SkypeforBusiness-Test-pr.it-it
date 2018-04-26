---
title: Remove-CsUserReplicatorConfiguration
TOCTitle: Remove-CsUserReplicatorConfiguration
ms:assetid: 26c3a357-558f-406f-8df3-059911f771f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425738(v=OCS.15)
ms:contentKeyID: 49299979
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserReplicatorConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione di User Replicator. User Replicator recupera periodicamente da Active Directory informazioni dell'account utente aggiornate e sincronizza le nuove informazioni con i dati correnti dell'utente archiviati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsUserReplicatorConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono ripristinate le impostazioni di configurazione di User Replicator globali.

    Remove-CsUserReplicatorConfiguration -Identity global

## Descrizione dettagliata

Anche se Lync Server dispone di un proprio database di account utente e di dati degli account utente, Lync Server si basa comunque su Active Directory come fonte definitiva delle informazioni utente. Quando ad esempio viene creato un nuovo account utente Active Directory, è necessario fornire le informazioni di base relative all'account utente, ad esempio il nome visualizzato di Active Directory. Quando tuttavia un utente è abilitato per Lync Server, non è necessario specificare un nuovo nome visualizzato, in quanto in Lync Server viene utilizzato il nome visualizzato già archiviato in Active Directory.

Naturalmente, le informazioni degli account utente, incluso il nome visualizzato di Active Directory, sono soggette a modifica nel corso del tempo. Un utente di sesso femminile dopo il matrimonio potrebbe ad esempio cambiare il proprio cognome e, di conseguenza, è necessario modificare il nome visualizzato. Per garantire che il database di Lync Server e Active Directory rimangano sincronizzati, è necessario che Lync Server si connetta periodicamente ad Active Directory, recuperi gli aggiornamenti più recenti sugli account utente e modifichi il database di Lync Server di conseguenza. La sincronizzazione tra Active Directory e Lync Server viene eseguita da User Replicator.

Durante l'installazione di Lync Server viene automaticamente creato un insieme globale di impostazioni di configurazione per User Replicator. Per impostazione predefinita, tali impostazioni vengono utilizzate per la gestione di User Replicator a livello di organizzazione. La gestione di User Replicator consiste nell'identificare i domini con cui Lync Server deve eseguire la sincronizzazione, nonché nell'indicare la frequenza in base alla quale User Replicator controlla la disponibilità degli aggiornamenti per gli account utente in Active Directory. Per impostazione predefinita, User Replicator individua tutti i domini disponibili ed effettua la sincronizzazione con essi. Utilizzando la proprietà AdDomainNamingContextList, è tuttavia possibile limitare la sincronizzazione a un insieme specifico di domini, ovvero i domini contenuti nella proprietà AdDomainNamingContextList.

È inoltre possibile creare ulteriori raccolte nell'ambito del servizio, ma solo se si utilizza Lync Online.

Se in seguito è necessario apportare modifiche, è possibile utilizzare il cmdlet **Remove-CsUserReplicatorConfiguration** per rimuovere le impostazioni personalizzate create nell'ambito del servizio. Si noti che questo cmdlet può anche essere eseguito per le impostazioni di configurazione globali. In questo caso, tuttavia, le impostazioni globali non verranno rimosse, ma verranno ripristinati i valori predefiniti di tutte le proprietà della raccolta globale. Per User Replicator, ciò indica la rimozione dell'elenco dei domini che devono essere sincronizzati (provocando la sincronizzazione con tutti i domini individuabili) e l'impostazione del ciclo dell'intervallo di replica su 1 minuto.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsUserReplicatorConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserReplicatorConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione di User Replicator da rimuovere. Per rimuovere le impostazioni nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;. Si noti che è possibile rimuovere le impostazioni nell'ambito del servizio solo se si utilizza Lync Online. Per ripristinare le impostazioni globali, utilizzare la sintassi seguente: -Identity global. Non è consentito utilizzare caratteri jolly per specificare un'identità.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration. Il cmdlet **Remove-CsUserReplicatorConfiguration** accetta l'input da pipeline dell'oggetto configurazione di User Replicator.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsUserReplicatorConfiguration** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)  
[New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)  
[Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

