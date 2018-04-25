---
title: Remove-CsClientVersionPolicy
TOCTitle: Remove-CsClientVersionPolicy
ms:assetid: 2fd9ca4c-8b4f-41f0-b051-5b486376008c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425801(v=OCS.15)
ms:contentKeyID: 49300078
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il criterio di versione client specificato. I criteri di versione client consentono di specificare quali client (ad esempio Microsoft Office Communicator 2007 R2) saranno in grado di accedere al sistema Lync Server in uso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsClientVersionPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare il criterio della versione client per il sito Redmond.

    Remove-CsClientVersionPolicy -Identity site:Redmond

## ESEMPIO 2

Nell'Esempio 2, vengono eliminati tutti i criteri della versione client configurati nell'ambito del singolo utente. Per eseguire questa operazione, il comando utilizza prima il cmdlet **Get-CsClientVersionPolicy** e il parametro Filter; il valore del filtro "tag:\*" restituisce solo i dati relativi ai criteri configurati nell'ambito del singolo utente. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsClientVersionPolicy** che elimina ogni elemento della raccolta.

    Get-CsClientVersionPolicy -Filter tag:* | Remove-CsClientVersionPolicy

## Descrizione dettagliata

I criteri di versione client rappresentano una raccolta di regole di versione client. Tali regole, a loro volta, vengono utilizzate per stabilire a quali applicazioni client è consentito l'accesso a Lync Server. Quando un utente tenta di accedere a Lync Server, la sua applicazione client invia un'intestazione SIP al server. In questa intestazione sono contenute informazioni dettagliate sull'applicazione, inclusi versione principale, versione secondaria e numero di build del software. In seguito, le informazioni sulla versione contenute nell'intestazione SIP vengono controllate a fronte di una raccolta di regole della versione client per verificare se alcune di queste regole si riferiscono a quella particolare applicazione. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. La regola ad esempio potrebbe indicare a Lync Server di consentire l'accesso, di bloccarlo o di autorizzarlo e quindi di aggiornare l'applicazione client all'ultima versione, ad esempio da Communicator 2007 R2 a Lync 2013, senza intervento dell'utente.

I criteri di versione client che è possibile applicare all'ambito globale, del sito, del servizio (solo per il servizio di registrazione) o per utente offrono notevole flessibilità nel determinare quali applicazioni client è possibile utilizzare per accedere al sistema. Si supponga ad esempio di voler impedire come regola generale agli utenti di accedere a Lync Server utilizzando Communicator 2007 R2 poiché Communicator 2007 R2 non supporta le stesse funzionalità e caratteristiche di Lync 2013. Tuttavia, a causa di conflitti hardware o software, è presente un gruppo di utenti che non possono eseguire l'aggiornamento a Lync 2013. In questo caso, è possibile creare una regola separata e un corrispondente criterio di versione client per consentire a tali utenti di accedere al sistema utilizzando Communicator 2007 R2.

È possibile creare nuovi criteri utilizzando il cmdlet **New-CsClientVersionPolicy**. Questi criteri personalizzati possono essere rimossi successivamente utilizzando il cmdlet **Remove-CsClientVersionPolicy**. Quando si rimuove un criterio della versione client, gli utenti a cui era applicato quel criterio ereditano automaticamente il criterio successivo nella gerarchia di gestione. Ad esempio, se si elimina un criterio per utente, agli utenti verrà automaticamente applicato il criterio del servizio appropriato. Se non esiste alcun criterio del servizio, agli utenti verrà applicato il criterio del sito appropriato. Se non esiste alcun criterio del sito, agli utenti verrà applicato il criterio globale.

Si noti che vi sarà sempre un criterio globale e che a tutti gli utenti verrà pertanto applicato un criterio della versione client. Sebbene sia possibile eseguire il cmdlet **Remove-CsClientVersionPolicy** per il criterio globale, in realtà il criterio non verrà eliminato. Tutte le regole dei criteri verranno invece reimpostate sui valori predefiniti.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsClientVersionPolicy** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionPolicy\\b"}

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
<td><p>Identificatore univoco del criterio da eliminare. Per rimuovere un criterio configurato nell'ambito del sito, utilizzare una sintassi analoga alla seguente: -Identity &quot;site:Redmond&quot;. Per rimuovere un criterio configurato nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;. Il servizio di registrazione è il solo servizio che può ospitare un criterio della versione client.</p>
<p>I criteri possono essere rimossi anche nell'ambito per utente. Per eliminare criteri per utente, utilizzare una sintassi simile alla seguente: -Identity &quot;SalesDepartmentPolicy&quot;.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy. Il cmdlet **Remove-CsClientVersionPolicy** accetta le istanze da pipeline dell'oggetto criteri delle versioni client.

## Tipi restituiti

Il cmdlet **Remove-CsClientVersionPolicy** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[Grant-CsClientVersionPolicy](grant-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

