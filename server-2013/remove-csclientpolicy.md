---
title: Remove-CsClientPolicy
TOCTitle: Remove-CsClientPolicy
ms:assetid: 2beb1557-8397-493e-be87-910ce01ba8f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425772(v=OCS.15)
ms:contentKeyID: 49300033
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un criterio client esistente. I criteri client consentono di stabilire, tra l'altro, le funzionalità di Lync disponibili per gli utenti. È ad esempio possibile decidere di consentire solo ad alcuni utenti di trasferire i file, negando questo diritto ad altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsClientPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsClientPolicy** per eliminare il criterio client con Identity SalesPolicy.

    Remove-CsClientPolicy -Identity SalesPolicy

## ESEMPIO 2

Nell'esempio 2 vengono utilizzati i cmdlet **Get-CsClientPolicy** e **Remove-CsClientPolicy** per eliminare tutti i criteri client configurati nell'ambito per utente. Il comando utilizza il cmdlet **Get-CsClientPolicy** e il parametro Filter per restituire una raccolta di tutti i criteri client configurati nell'ambito per utente. Il valore di filtro "tag:\*" fa in modo che il cmdlet **Get-CsClientPolicy** restituisca solo i dati relativi ai criteri client la cui identità inizia con il valore stringa "tag:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsClientPolicy**, che rimuove ogni criterio della raccolta.

    Get-CsClientPolicy -Filter "tag:*" | Remove-CsClientPolicy

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i criteri client in cui la proprietà EnableAppearOffline è impostata su True. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsClientPolicy** senza parametri aggiuntivi. Viene così restituita una raccolta di tutti i criteri client configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà EnableAppearOffline è uguale a True. Questa raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsClientPolicy**, che elimina ogni criterio della raccolta.

    Get-CsClientPolicy | Where-Object {$_.EnableAppearOffline -eq $True} | Remove-CsClientPolicy

## Descrizione dettagliata

In Lync Server i criteri client sostituiscono le impostazioni di Criteri di gruppo in uso nelle versioni precedenti del prodotto. In Microsoft Office Communicator 2007 e Microsoft Office Communicator 2007 R2 la funzionalità Criteri di gruppo viene utilizzata per definire le azioni consentite agli utenti in Communicator e in altri client. Alcune impostazioni di Criteri di gruppo ad esempio stabiliscono se gli utenti possono o meno salvare una trascrizione delle rispettive sessioni di messaggistica istantanea, se possono o meno inserire emoticon o testo formattato nei messaggi istantanei e se nelle informazioni sulla presenza vengono incorporate le informazioni di Microsoft Outlook.

Per quanto utile, la tecnologia di Criteri di gruppo tuttavia presenta limitazioni se applicata a Lync Server. Da un lato, Criteri di gruppo è stato concepito per essere applicato per singolo dominio o per singola unità organizzativa e pertanto risulta difficile applicare i criteri a un gruppo di utenti specifici, ad esempio tutti gli utenti che lavorano in un determinato reparto o tutti gli utenti con una determinata qualifica. Dall'altro, Criteri di gruppo viene applicato solo agli utenti che accedono al dominio tramite un computer e non agli utenti che accedono a Lync Server da Internet o che accedono al sistema utilizzando un telefono cellulare. Ciò significa che lo stesso utente può avere un'esperienza diversa in base al dispositivo e al luogo da cui esegue l'accesso.

Per ovviare a questi problemi, in Lync Server vengono utilizzati criteri client anziché Criteri di gruppo. I criteri client vengono applicati ogni volta che un utente accede al sistema, indipendentemente dal dispositivo e dal luogo da cui viene eseguito l'accesso. I criteri client, così come altri criteri di Lync Server, possono inoltre essere applicati a gruppi di utenti selezionati. È anche possibile creare un criterio personalizzato che viene assegnato a un singolo utente.

È possibile configurare i criteri client nell'ambito globale, del sito o per utente. I criteri configurati nell'ambito del sito o per utente possono essere successivamente eliminati utilizzando il cmdlet **Remove-CsClientPolicy**. Il cmdlet **Remove-CsClientPolicy** può inoltre essere eseguito per il criterio globale. In questo caso, il criterio globale però non verrà rimosso, in quanto i criteri globali non possono essere eliminati. Tutte le proprietà del criterio globale verranno invece reimpostate sui valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsClientPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientPolicy"}

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
<td><p>Identificatore univoco del criterio client da rimuovere. Per &quot;rimuovere&quot; il criterio globale, utilizzare la seguente sintassi: -Identity global. Si noti che non è possibile eliminare un criterio globale. Ciò che accade è che per tutte le proprietà di quel criterio globale verranno ripristinati i valori predefiniti. Per eliminare criteri del sito, usare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per eliminare criteri per utente, usare una sintassi simile alla seguente: -Identity &quot;SalesDepartmentPolicy&quot;. Non è possibile utilizzare caratteri jolly quando si specifica l'identità di un criterio.</p></td>
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
<td><p>Se questo parametro è presente, il criterio verrà rimosso automaticamente anche se è attualmente assegnato a un utente. Se questo parametro non è presente, il cmdlet <strong>Remove-CsClientPolicy</strong> non rimuoverà automaticamente un criterio per utente che è assegnato ad almeno un utente. Verrà invece visualizzato un messaggio che richiede di confermare la rimozione del criterio. Per procedere con l'operazione e rimuovere il criterio, è necessario rispondere affermativamente (premendo il tasto Y).</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy. Il cmdlet **Remove-CsClientPolicy** accetta le istanze dell'oggetto criterio client inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsClientPolicy** non restituisce alcun valore. Il cmdlet invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientPolicy](get-csclientpolicy.md)  
[Grant-CsClientPolicy](grant-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

