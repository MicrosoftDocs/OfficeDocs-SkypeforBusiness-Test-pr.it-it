---
title: Remove-CsClientVersionPolicyRule
TOCTitle: Remove-CsClientVersionPolicyRule
ms:assetid: 71a107c9-5499-460f-b4b8-08b368be9321
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398541(v=OCS.15)
ms:contentKeyID: 49300945
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionPolicyRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più regole dei criteri di versione client configurate per l'utilizzo nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsClientVersionPolicyRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare la regola per i criteri della versione client con Identity site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820. Poiché le identità devono essere univoche, il comando eliminerà al massimo una regola.

    Remove-CsClientVersionPolicyRule -Identity site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le regole dei criteri della versione client configurate per il sito Redmond. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClientVersionPolicyRule** insieme al parametro Filter. Il valore di filtro "site:Redmond/\*" restituisce solo i dati relativi alle regole la cui identità (Identity) inizia con il valore stringa "site:Redmond/". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsClientVersionPolicyRule**, che elimina ogni elemento della raccolta.

    Get-CsClientVersionPolicyRule -Filter "site:Redmond/*" | Remove-CsClientVersionPolicyRule

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le regole per i criteri della versione client attualmente disabilitate. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClientVersionPolicyRule** senza alcun parametro aggiuntivo in modo da ottenere una raccolta di tutte le regole di criteri attualmente in uso nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà Enabled è uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsClientVersionPolicyRule**, che elimina ogni elemento della raccolta.

    Get-CsClientVersionPolicyRule | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionPolicyRule

## Descrizione dettagliata

Le regole della versione client vengono utilizzate per stabilire quali applicazioni client sono autorizzate ad accedere a Lync Server. Quando un utente tenta di accedere a Lync Server, la relativa applicazione client invia un'intestazione SIP al server. Questa intestazione include informazioni dettagliate sull'applicazione, tra cui la versione principale, la versione secondaria e il numero di build del software. Le informazioni sulla versione vengono quindi verificate in base a una raccolta di regole della versione client per valutare se qualche regola sia applicabile a quella particolare applicazione. Ad esempio, si supponga che un utente tenti di accedere utilizzando Microsoft Office Communicator 2007 R2. Prima che l'accesso possa avere luogo, il sistema verificherà l'eventuale presenza di una regola della versione client applicabile a Office Communicator 2007 R2. Se la regola esiste, Lync Server eseguirà l'azione specificata dalla regola. L'azione deve essere una delle seguenti:

Allow. All'utente sarà consentito effettuare l'accesso.

AllowAndUpgrade. All'utente sarà consentito effettuare l'accesso e la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

AllowWithUrl. All'utente sarà consentito effettuare l'accesso e verrà visualizzato un messaggio che lo indirizzerà a un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Block. All'utente non sarà consentito effettuare l'accesso.

BlockAndUpgrade. All'utente non sarà consentito effettuare l'accesso, ma la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. L'utente potrà quindi tentare di effettuare l'accesso utilizzando la nuova applicazione client. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

BlockWithUrl. All'utente non sarà consentito effettuare l'accesso, ma verrà visualizzato un messaggio che lo indirizzerà ad un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Le regole della versione client sono raccolte nei criteri della versione client che possono essere configurati nell'ambito globale, nell'ambito del sito, nell'ambito del servizio (servizio di registrazione) o nell'ambito per utente. Il cmdlet **Remove-CsClientVersionPolicyRule** consente di eliminare una o più regole dei criteri client configurate per l'utilizzo nella propria organizzazione. Queste regole possono essere eliminate da uno qualunque dei propri criteri della versione client, incluso il criterio globale.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsClientVersionPolicyRule** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionPolicyRule"}

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
<td><p>Identificatore univoco della regola per i criteri della versione client da rimuovere. L'identità di una regola della versione client è costituita dall'ambito in cui la regola è stata configurata più un identificatore univoco globale (GUID). Ciò significa che una regola avrà un'identità simile alla seguente: site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule. Il cmdlet **Remove-CsClientVersionPolicyRule** accetta istanze dell'oggetto regola versione client inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsClientVersionPolicyRule** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md)  
[New-CsClientVersionPolicyRule](new-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

