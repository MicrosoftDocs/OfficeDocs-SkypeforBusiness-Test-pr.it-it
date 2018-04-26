---
title: Get-CsTestUserCredential
TOCTitle: Get-CsTestUserCredential
ms:assetid: 2af8d526-005c-40fb-957c-5b2ee5bce432
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204759(v=OCS.15)
ms:contentKeyID: 49300014
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTestUserCredential

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano che un utente è stato configurato come utente di test di nodi Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Lync Server 2013 e Microsoft System Center Operations Manager per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsTestUserCredential -SipAddress <String>

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni sull'utente sip:kenmyer@litwareinc.com, purché sia stato configurato come utente di test di nodi Watcher. Se l'utente non è stato configurato come utente di test, il cmdlet **Get-CsTestUserCredential** restituirà un errore.

    Get-CsTestUserCredential -SipAddress "sip:kenmyer@litewareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 restituiscono un elenco di tutti gli utenti configurati come utenti di test di nodi Watcher. A tale scopo, il primo comando dell'esempio imposta il valore della variabile $ErrorActionPreference dell'interfaccia della riga di comando di Windows PowerShell su "SilentlyContinue". In questo modo si evita la visualizzazione di messaggi di errore che vengono altrimenti visualizzati se il cmdlet **Get-CsTestUserCredential** tenta di restituire informazioni su un utente non configurato come utente di test di nodi Watcher.

Con la visualizzazione dei messaggi di errore bloccata, il secondo comando dell'esempio utilizza il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti abilitati per Lync Server 2013. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet **ForEach-Object** esegue un ciclo in ogni account utente della raccolta, utilizzando il cmdlet **Get-CsTestUserCredential** su ogni account per verificare se l'utente è stato configurato come utente di test. In caso affermativo, verranno visualizzate le informazioni sull'utente, altrimenti non verrà visualizzato alcun dato.

L'ultimo comando dell'esempio reimposta il valore di $ErrorActionPreference su "Continue".

    $ErrorActionPreference = "SilentlyContinue"
    Get-CsUser | ForEach-Object {Get-CsTestUserCredential -SipAddress $_.SipAddress}
    $ErrorActionPreference = "Continue"

## Descrizione dettagliata

Se si utilizza System Center Operations Manager insieme a Lync Server 2013, è possibile configurare computer "nodo Watcher". I nodi Watcher sono computer che eseguono periodicamente e automaticamente transazioni sintetiche, ovvero cmdlet che verificano diverse funzionalità di Lync Server. Alcune transazioni sintetiche ad esempio verificano che gli utenti possano effettuare la registrazione in Lync Server, che possano scambiarsi messaggi istantanei e informazioni sulla presenza utilizzando Lync Server, che possano condurre conferenze di collaborazione dati e condivisione applicazioni e che possano effettuare chiamate sulla rete PSTN (Public Switched Telephone Network). Come indicato, queste transazioni sintetiche vengono eseguite periodicamente. Se hanno esito negativo, inviano avvisi in cui viene notificato agli amministratori che è possibile che si stiano verificando problemi nel sistema.

Molte transazioni sintetiche richiedono utenti test. Non è possibile ad esempio verificare la capacità di due utenti di scambiarsi messaggi istantanei se non si dispone di due account utente e non si tenta di scambiare messaggi istantanei utilizzando tali account. Quando si configura un nodo Watcher, è necessario assegnare almeno due utenti test al nodo. Gli utenti test possono essere rappresentati da qualsiasi account utente di Active Directory valido abilitato per Lync Server 2013 e registrato come account test. Gli account vengono registrati come account test utilizzando il cmdlet [Set-CsTestUserCredential](set-cstestusercredential.md). Se successivamente si decide di non utilizzare un account come account test, è possibile annullarne la registrazione utilizzando il cmdlet [Remove-CsTestUserCredential](remove-cstestusercredential.md). Questo cmdlet impedisce semplicemente che l'account venga utilizzato come account test di nodi Watcher. Non elimina, disabilita o modifica l'account.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTestUserCredential"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsTestUserCredential** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indirizzo SIP dell'account in cui vengono ricercate le credenziali di utente test, ad esempio:</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>È necessario includere il parametro SipAddress quando viene chiamato il cmdlet <strong>Get-CsTestUserCredential</strong>, altrimenti verrà richiesto di immettere l'indirizzo.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTestUserCredential** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsTestUserCredential** restituisce istanze dell'oggetto System.Management.Automation.PSCredential.

## Vedere anche

#### Ulteriori risorse

[Remove-CsTestUserCredential](remove-cstestusercredential.md)  
[Set-CsTestUserCredential](set-cstestusercredential.md)

