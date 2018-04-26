---
title: Remove-CsTestUserCredential
TOCTitle: Remove-CsTestUserCredential
ms:assetid: 49290251-276d-41d5-bcfd-077018d74f59
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204870(v=OCS.15)
ms:contentKeyID: 49300418
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTestUserCredential

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove l'utente specificato dall'insieme di utenti configurati come utenti di test di nodi Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Lync Server 2013 e Microsoft System Center Operations Manager per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsTestUserCredential -SipAddress <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove l'utente con indirizzo SIP sip:kenmyer@litwareinc.com dalla raccolta di utenti configurati come utenti test di nodi Watcher.

    Remove-CsTestUserCredential "sip:kenmyer@litwareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 rimuovono tutti gli utenti configurati come utenti di test di nodi Watcher. Si noti che questa operazione non comporta l'eliminazione degli account utente, ma solo dello stato di utenti di test di nodi Watcher. A tale scopo, il primo comando dell'esempio imposta il valore della variabile ErrorActionPreference di Windows PowerShell su "SilentlyContinue". In questo modo si evita la visualizzazione di un messaggio di errore che verrebbe altrimenti visualizzato ogni volta che il cmdlet **Remove-CsTestUserCredential** tenta di rimuovere le credenziali di test dall'utente che è stato configurato come utente di test di nodi Watcher.

Dopo l'eliminazione della visualizzazione dei messaggi di errore, il secondo comando dell'esempio utilizza il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti che sono stati abilitati per Lync Server 2013. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet **ForEach-Object** esegue un ciclo tra gli account utente della raccolta, eseguendo il cmdlet **Remove-CsTestUserCredential** per ogni account in modo da rimuovere l'utente come utente di test di nodi Watcher.

L'ultimo comando dell'esempio reimposta il valore di $ErrorActionPreference su "Continue".

    $ErrorActionPreference = "SilentlyContinue"
    
    Get-CsUser | ForEach-Object {Remove-CsTestUserCredential -SipAddress $_.SipAddress}
    
    $ErrorActionPreference = "Continue"

## Descrizione dettagliata

Se si utilizza System Center Operations Manager insieme a Lync Server 2013, è possibile configurare computer "nodo Watcher". I nodi Watcher sono computer che eseguono periodicamente e automaticamente transazioni sintetiche, ovvero cmdlet che verificano diverse funzionalità di Lync Server. Alcune transazioni sintetiche ad esempio verificano che gli utenti possano effettuare la registrazione in Lync Server, che possano scambiarsi messaggi istantanei e informazioni sulla presenza utilizzando Lync Server, che possano condurre conferenze di collaborazione dati e condivisione applicazioni e che possano effettuare chiamate sulla rete PSTN (Public Switched Telephone Network). Come indicato, queste transazioni sintetiche vengono eseguite periodicamente. Se hanno esito negativo, inviano avvisi in cui viene notificato agli amministratori che è possibile che si stiano verificando problemi nel sistema.

Molte transazioni sintetiche richiedono utenti di test. Non è possibile ad esempio verificare la capacità di due utenti di scambiarsi messaggi istantanei se non si dispone di una coppia di account utente e si tenta di scambiare messaggi istantanei utilizzando tali account. Quando si configura un nodo Watcher, è necessario assegnare almeno due utenti di test al nodo. Gli utenti di test possono essere rappresentati da qualsiasi account utente di Active Directory valido abilitato per Lync Server 2013 e registrato come account di test. Gli account vengono registrati come account di test utilizzando il cmdlet [Set-CsTestUserCredential](set-cstestusercredential.md). Se successivamente si decide di non utilizzare un account come account di test, è possibile annullarne la registrazione utilizzando il cmdlet **Remove-CsTestUserCredential**. Questo cmdlet impedisce semplicemente che l'account venga utilizzato come account di test di nodi Watcher. Non elimina, disabilita o modifica l'account.

Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTestUserCredential"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsTestUserCredential** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>SipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'account di cui vengono rimosse le credenziali di utente test, ad esempio:</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p></td>
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

Nessuno. Il cmdlet **Remove-CsTestUserCredential** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsTestUserCredential** invece elimina le istanze esistenti dell'oggetto System.Management.Automation.PSCredential.

## Vedere anche

#### Ulteriori risorse

[Get-CsTestUserCredential](get-cstestusercredential.md)  
[Set-CsTestUserCredential](set-cstestusercredential.md)

