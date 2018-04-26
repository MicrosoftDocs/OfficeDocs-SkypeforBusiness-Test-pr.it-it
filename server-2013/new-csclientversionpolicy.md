---
title: New-CsClientVersionPolicy
TOCTitle: New-CsClientVersionPolicy
ms:assetid: 8c95493a-ce18-49eb-937f-7348743fcbb4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398709(v=OCS.15)
ms:contentKeyID: 49301271
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio di versione client. I criteri di questo tipo consentono di specificare quali versioni di client (ad esempio Microsoft Office Communicator 2007 R2) saranno in grado di accedere al sistema Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsClientVersionPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Rules <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'Esempio 1, viene creato un nuovo criterio della versione client per il sito Redmond. Poiché non vengono specificati parametri (oltre all'obbligatorio Identity) il nuovo criterio conterrà tutti i valori predefiniti per un criterio di versione client.

    New-CsClientVersionPolicy -Identity site:Redmond

## ESEMPIO 2

Il comando riportato nell'esempio 2 crea un nuovo criterio di versione client per ogni sito dell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsSite** senza alcun parametro. In questo modo, viene restituita una raccolta di tutti i siti nella topologia. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che estrae la proprietà Identity di ogni sito. Queste identità vengono inviate tramite pipe al cmdlet **ForEach-Object**, che crea un nuovo criterio di versione client per ogni sito della raccolta.

    Get-CsSite | Select-Object Identity | ForEach-Object {New-CsClientVersionPolicy -Identity ("site:" + $_.Identity)}

## Descrizione dettagliata

I criteri di versione client rappresentano una raccolta di regole di versione client. Tali regole, a loro volta, vengono utilizzate per stabilire a quali applicazioni client è consentito l'accesso a Lync Server. Quando un utente tenta di accedere a Lync Server, la sua applicazione client invia un'intestazione SIP al server. In questa intestazione sono contenute informazioni dettagliate sull'applicazione, inclusi versione principale, versione secondaria e numero di build del software. In seguito, le informazioni sulla versione contenute nell'intestazione SIP vengono controllate a fronte di una raccolta di regole della versione client per verificare se alcune di queste regole si riferiscono a quella particolare applicazione. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. La regola ad esempio potrebbe indicare a Lync Server di consentire l'accesso, di bloccarlo o di autorizzarlo e quindi di aggiornare l'applicazione client all'ultima versione, ad esempio da Communicator 2007 R2 a Lync 2013, senza intervento dell'utente.

I criteri di versione client, che possono essere applicati all'ambito globale, all'ambito del sito, all'ambito del servizio (solo per il servizio di registrazione) o all'ambito del singolo utente, offrono notevole flessibilità nel determinare quali applicazioni client è possibile utilizzare per accedere al sistema. Ad esempio, come regola generale si potrebbe voler impedire agli utenti di accedere a Lync Server utilizzando Communicator 2007 R2. Ciò potrebbe essere necessario in quanto le vecchie applicazioni client non supportano le stesse caratteristiche e funzionalità di Lync. A causa di conflitti hardware o software, potrebbe tuttavia esistere un gruppo di utenti che non possono eseguire l'aggiornamento a Lync Server. In questo caso, è possibile creare una regola separata e un criterio di versione client corrispondente per consentire a tali utenti di eseguire l'accesso da Communicator 2007 R2.

Si noti, tuttavia, che agli utenti anonimi vengono applicati solo i criteri globali. Ciò avviene in quanto gli utenti anonimi non sono associati a un sito o a un servizio e non è pertanto possibile assegnare loro un criterio per utente.

È possibile creare nuovi criteri della versione client utilizzando il cmdlet **New-CsClientVersionPolicy**. Questi nuovi criteri possono essere creati in ambito di sito, in ambito di servizio (solo servizio di registrazione) ed in ambito per utente.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsClientVersionPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionPolicy\\b"}

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
<td><p>Identificatore univoco del criterio da creare. Per creare un criterio nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per creare un criterio nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;. Il servizio di registrazione è il solo servizio che può ospitare un criterio di versione client.</p>
<p>I criteri possono essere creati anche nell'ambito per utente. Per creare un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity &quot;SalesDepartmentPolicy&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di fornire del testo esplicativo per il criterio. Ad esempio, potrebbero essere indicati gli utenti ai quali deve essere assegnato il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Rules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di regole per i criteri di versione client. Le regole vengono facilmente aggiunte o rimosse da un criterio utilizzando i cmdlet <strong>New-CsClientVersionPolicyRule</strong> e <strong>Remove-CsClientVersionPolicyRule</strong>. Per aggiungere una regola nel momento in cui si crea il nuovo criterio, creare la regola e archiviare il relativo valore in una variabile, ad esempio $x. È possibile utilizzare una sintassi simile alla seguente per creare un nuovo criterio:</p>
<p>New-CsClientVersionPolicy –Identity &quot;RedmondClientVersionPolicy&quot; –Rules @{Add=$x}</p></td>
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

Nessuno. Il cmdlet **Get-CsClientVersionPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsClientVersionPolicy** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[Grant-CsClientVersionPolicy](grant-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

