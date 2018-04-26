---
title: Get-CsClientPolicy
TOCTitle: Get-CsClientPolicy
ms:assetid: c8e1cb96-2bf7-447c-b41c-d896fe85e349
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398830(v=OCS.15)
ms:contentKeyID: 49301967
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui criteri client configurati per l'utilizzo nell'organizzazione. I criteri client consentono di stabilire, tra l'altro, le funzionalità di Lync disponibili per gli utenti. È ad esempio possibile decidere di consentire solo ad alcuni utenti di trasferire i file, negando questo diritto ad altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsClientPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene chiamato il cmdlet **Get-CsClientPolicy** senza includere altri parametri. In questo modo viene restituita una raccolta di tutti i criteri client configurati per l'utilizzo all'interno dell'organizzazione.

    Get-CsClientPolicy

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il cmdlet **Get-CsClientPolicy** per restituire i criteri client per utente con valore Identity SalesPolicy. Poiché le identità sono univoche, questo comando non restituirà mai più di un elemento.

    Get-CsClientPolicy -Identity SalesPolicy

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per restituire tutti i criteri client configurati nell'ambito per utente. Il valore di filtro "tag:\*" indica al cmdlet **Get-CsClientPolicy** di restituire solo i criteri con valore Identity che inizia con il valore stringa "tag:".

    Get-CsClientPolicy -Filter "tag:*"

## ESEMPIO 4

Nell'esempio 4 viene restituita una raccolta di tutti i criteri client in cui la proprietà DisableSavingIM è impostata su True. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsClientPolicy** senza alcun parametro per restituire una raccolta di tutti i criteri client configurati per l'utilizzo all'interno dell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente i criteri con proprietà DisableSavingIM uguale a True.

    Get-CsClientPolicy | Where-Object {$_.DisableSavingIM -eq $True}

## ESEMPIO 5

Nell'esempio 5 vengono restituiti solo i criteri client che soddisfano due requisiti: la proprietà DisableSavingIM deve essere impostata su True, mentre la proprietà EnableIMAutoArchiving deve essere impostata su False. A tale scopo, nel comando viene chiamato innanzitutto il cmdlet **Get-CsClientPolicy** per restituire una raccolta di tutti i criteri client configurati per l'utilizzo all'interno dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri che soddisfano entrambi i seguenti requisiti: DisableSavingIM deve essere uguale a True ed EnableIMAutoArchiving deve essere uguale a False. L'operatore -and indica al cmdlet **Where-Object** di selezionare solo gli oggetti che soddisfano tutti i requisiti specificati.

    Get-CsClientPolicy | Where-Object {$_.DisableSavingIM -eq $True -and $_.EnableIMAutoArchiving -eq $False}

## ESEMPIO 6

L'esempio 6 è una variazione del comando mostrato nell'esempio 5. Tuttavia, in questo caso, i criteri vengono selezionati finché soddisfano almeno uno dei seguenti requisiti: la proprietà DisableSavingIM è uguale a True e/o la proprietà EnableIMAutoArchiving è uguale a False. Per eseguire questa attività, nel comando viene chiamato innanzitutto il cmdlet **Get-CsClientPolicy** per restituire una raccolta di tutti i criteri client configurati per l'utilizzo all'interno dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri che soddisfano almeno uno dei seguenti requisiti: DisableSavingIM è uguale a True e/o EnableIMAutoArchiving è uguale a False. L'operatore -or indica al cmdlet **Where-Object** di selezionare qualsiasi oggetto che soddisfi almeno una delle condizioni specificate.

## Descrizione dettagliata

In Lync Server i criteri client sostituiscono le impostazioni di Criteri di gruppo in uso nelle versioni precedenti del prodotto. In Microsoft Office Communicator 2007 e Microsoft Office Communicator 2007 R2 la funzionalità Criteri di gruppo viene utilizzata per definire le azioni consentite agli utenti in Communicator e in altri client. Alcune impostazioni di Criteri di gruppo ad esempio stabiliscono se gli utenti possono o meno salvare una trascrizione delle rispettive sessioni di messaggistica istantanea, se possono o meno inserire emoticon o testo formattato nei messaggi istantanei e se nelle informazioni sulla presenza vengono incorporate le informazioni di Microsoft Outlook.

Nonostante l'utilità di Criteri di gruppo, questa tecnologia presenta tuttavia alcuni limiti se applicata a Lync Server. Da un lato la funzionalità Criteri di gruppo è progettata per essere applicata in base al dominio o all'unità organizzativa e rende pertanto difficile assegnare i criteri a un gruppo di utenti più selezionato, ad esempio a tutti gli utenti che lavorano in un reparto specifico o a tutti quelli in possesso di una qualifica particolare. Dall'altro la funzionalità Criteri di gruppo viene applicata solo agli utenti che accedono al dominio e che effettuano l'accesso tramite un computer. Non viene applicata invece agli utenti che accedono al sistema su Internet o utilizzando un telefono cellulare. Ciò significa che lo stesso utente può avere esperienze diverse a seconda del dispositivo e della postazione utilizzati per l'accesso.

Per risolvere queste incongruenze, in Lync Server vengono utilizzati i criteri di gestione client anziché Criteri di gruppo. I criteri client vengono applicati ogni volta che un utente accede al sistema, indipendentemente dalla postazione e dal tipo di dispositivo utilizzati per l'accesso. I criteri client, analogamente ad altri criteri di Lync Server, possono inoltre essere facilmente assegnati a gruppi selezionati di utenti. È anche possibile creare criteri personalizzati da assegnare a un singolo utente.

I criteri client possono essere configurati in ambito globale, di sito e per utente. Il cmdlet **Get-CsClientPolicy** consente di restituire informazioni su tutti i criteri client che sono stati configurati per l'utilizzo all'interno dell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsClientPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientPolicy"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly quando si indicano uno o più criteri da restituire. A esempio, per restituire tutti i criteri configurati nell'ambito del sito, utilizzare questa sintassi: -Filter &quot;site:*&quot;. Per restituire una raccolta di tutti i criteri per utente, utilizzare la seguente sintassi: -Filter &quot;tag:*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco dei criteri client da restituire. Per fare riferimento al criterio globale, utilizzare la seguente sintassi: -Identity global. Per fare riferimento a un criterio del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per fare riferimento a un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity SalesDepartmentPolicy.</p>
<p>Se si omette questo parametro, verranno restituiti tutti i criteri client configurati per utilizzo all'interno dell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi ai criteri client dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClientPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsClientPolicy** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsClientPolicy](grant-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Remove-CsClientPolicy](remove-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

