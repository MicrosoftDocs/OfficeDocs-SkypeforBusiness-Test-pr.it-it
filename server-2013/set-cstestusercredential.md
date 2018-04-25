---
title: Set-CsTestUserCredential
TOCTitle: Set-CsTestUserCredential
ms:assetid: e613fad9-e91b-4bce-a67d-b1c9860ab34d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205341(v=OCS.15)
ms:contentKeyID: 49302305
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTestUserCredential

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo utente test di nodi Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Microsoft System Center Operations Manager e Lync Server 2013 per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsTestUserCredential -Credential <PSCredential> <COMMON PARAMETERS>

    Set-CsTestUserCredential -Password <String> -UserName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -SipAddress <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 configura l'utente con l'indirizzo SIP sip:kenmyer@litwareinc.com come utente test del nodo Watcher. Notare che è anche necessario fornire il nome utente (nel formato nome di dominio\\nome utente) e la password dell'utente quando si configura un account come utente test del nodo Watcher.

    Set-CsTestUserCredential -SipAddress "sip:kenmyer@litwareinc.com" -UserName "litwareinc\kenmyer" -Password "07Apples"

## Esempio 2

Anche i comandi riportati nell'esempio precedente configurano l'utente con l'indirizzo SIP sip:kenmyer@litwareinc.com come utente test del nodo Watcher. In questo caso, tuttavia, viene utilizzato il parametro Credential anziché i parametri UserName e Password. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell per l'account litwareinc\\kenmyer. Tale oggetto credenziali viene quindi archiviato in una variabile denominata $x. Notare che è necessario fornire la password per l'account litwareinc\\kenmyer quando si crea l'oggetto credenziali. Il secondo comando nell'esempio utilizza quindi il parametro Credential e il valore del parametro $x per configurare le credenziali di test.

    $x = Get-Credential "litwareinc\kenmyer"
    
    Set-CsTestUserCredential -SipAddress "sip:kenmyer@litwareinc.com" -Credential $x

## Descrizione dettagliata

Se si utilizza System Center Operations Manager insieme a Lync Server 2013, è possibile configurare computer "nodi Watcher". I nodi Watcher sono computer che eseguono periodicamente e automaticamente transazioni sintetiche, ovvero cmdlet che verificano diverse funzionalità di Lync Server. Alcune transazioni sintetiche, ad esempio, verificano che gli utenti possano effettuare la registrazione a Lync Server, che possano scambiarsi messaggi istantanei e informazioni sulla presenza utilizzando Lync Server, che possano eseguire conferenze di collaborazione dati e condivisione applicazioni e che possano effettuare chiamate sulla rete PSTN (Public Switched Telephone Network). Come indicato, queste transazioni sintetiche vengono eseguite periodicamente. Se hanno esito negativo, inviano avvisi in cui viene notificato agli amministratori che è possibile che si stiano verificando problemi nel sistema.

Molte transazioni sintetiche richiedono utenti test. Non è possibile ad esempio verificare la capacità di due utenti di scambiarsi messaggi istantanei se non si dispone di due account utente e non si tenta di scambiare messaggi istantanei utilizzando tali account. Quando si configura un nodo Watcher, è necessario assegnare almeno due utenti test al nodo. Gli utenti test possono essere rappresentati da qualsiasi account utente di Active Directory valido abilitato per Lync Server 2013 e registrato come account test. Gli account vengono registrati come account test utilizzando il cmdlet **Set-CsTestUserCredential**. Se successivamente si decide di non utilizzare un account come account test, è possibile annullarne la registrazione utilizzando il cmdlet [Remove-CsTestUserCredential](remove-cstestusercredential.md). Questo cmdlet impedisce semplicemente che l'account venga utilizzato come account test di nodi Watcher e non elimina, disabilita o modifica l'account.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTestUserCredential"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsTestUserCredential** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Credential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di configurare credenziali di test utilizzando un oggetto credenziali di Windows PowerShell anziché i parametri Password e UserName. Ciò offre il vantaggio di assicurare che la password dell'utente sia mascherata quando la si digita sullo schermo.</p>
<p>Per utilizzare il parametro Credential è necessario innanzitutto creare un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong> e quindi archiviare l'oggetto risultante in una variabile. Ad esempio:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Tale variabile viene quindi utilizzata come valore di parametro per il parametro Credential.</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Password per l'account di cui si stanno impostando le credenziali di utente test. Notare che questa password verrà visualizzata sullo schermo in testo normale. Ad esempio:</p>
<p>-Password &quot;p@ssw0rd&quot;</p>
<p>Non è necessario utilizzare i parametri Password o UserName se si utilizza il parametro Credential.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'account di cui si stanno impostando le credenziali di utente test. Ad esempio:</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>UserName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome utente dell'account che si sta configurando per le credenziali di test. Il nome utente può essere il valore SamAccountName o Active Directory DisplayName, ad esempio:</p>
<p>-UserName &quot;Ken Myer&quot;</p>
<p>È anche possibile specificare UserName utilizzando il formato nome di dominio\nome utente. Ad esempio:</p>
<p>-UserName &quot;litwareinc\kenmyer&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsTestUserCredential** non accetta input inviato tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsTestUserCredential** modifica piuttosto le istanze esistenti dell'oggetto System.Management.Automation.PSCredential.

## Vedere anche

#### Ulteriori risorse

[Get-CsTestUserCredential](get-cstestusercredential.md)  
[Remove-CsTestUserCredential](remove-cstestusercredential.md)

