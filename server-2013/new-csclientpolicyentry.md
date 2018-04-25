---
title: New-CsClientPolicyEntry
TOCTitle: New-CsClientPolicyEntry
ms:assetid: e975d048-4911-4ae6-9446-2a6363726a4a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399046(v=OCS.15)
ms:contentKeyID: 49302325
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicyEntry

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge nuove opzioni ai criteri client di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsClientPolicyEntry -Name <String> -Value <String>

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 mostrano come aggiungere una nuova voce di criterio al criterio client globale. Nell'esempio viene infatti aggiunta a Lync una nuova opzione di feedback. L'esempio ha tuttavia solo finalità puramente dimostrative. Non presumere di poter eseguire questi comandi e aggiungere un'opzione di feedback analoga nella propria copia di Lync.

Per aggiungere la nuova voce di criterio, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsClientPolicyEntry** per creare una voce con nome OnlineFeedbackURL e valore http://www.litwareinc.com/feedback. L'oggetto voce di criterio risultante viene archiviato nella variabile denominata $x.

Nel secondo comando viene utilizzato il cmdlet **Get-CsClientPolicy** per creare un riferimento oggetto ($y) ai criteri client globali. Una volta creato il riferimento oggetto, viene utilizzato il metodo Add per aggiungere la nuova voce di criterio alla proprietà PolicyEntry. Se PolicyEntry presenta già una o più voci, il nuovo valore verrà semplicemente aggiunto alla fine di tale raccolta.

Nell'ultimo comando dell'esempio viene infine utilizzato il cmdlet **Set-CsClientPolicy** per scrivere le modifiche nei criteri globali effettivi. Se non si chiama il cmdlet **Set-CsClientPolicy**, le modifiche saranno presenti solo in memoria e scompariranno non appena si chiude la sessione di Windows PowerShell oppure si elimina la variabile $x.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    
    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.Add($x)
    
    Set-CsClientPolicy -Instance $y

## ESEMPIO 2

L'esempio 2 rappresenta una variazione dei comandi mostrati nell'esempio 1. In questo caso, tuttavia, la nuova voce di criterio sostituisce tutti gli elementi presenti nella proprietà PolicyEntry dei criteri globali. A tale scopo, con il primo comando dell'esempio viene creata una nuova voce di criterio archiviata in una variabile denominata $x. Nel secondo comando viene quindi utilizzato il cmdlet **Set-CsClientPolicy** per impostare su $x il valore della proprietà PolicyEntry. Al termine dell'esecuzione del comando, l'unico elemento nella proprietà PolicyEntry sarà la nuova voce. Tutti gli elementi contenuti in tale proprietà prima della chiamata del cmdlet **Set-CsClientPolicy** saranno stati sostituiti dalla nuova voce.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    Set-CsClientPolicy -Identity global -PolicyEntry $x

## ESEMPIO 3

Nell'esempio 3 viene mostrato come rimuovere una voce di criterio client dal criterio globale. A tale scopo, con il primo comando dell'esempio viene recuperato il criterio client globale e tali informazioni vengono archiviate in una variabile denominata $y.

Dopo che il criterio globale è stato richiamato, nel secondo comando viene utilizzato il metodo RemoveAt() per eliminare la prima voce di tale criterio. La voce di criterio da rimuovere è indicata dal relativo numero di indice. La prima voce ha come numero di indice 0, la seconda 1 e così via. La sintassi RemoveAt(0) significa perciò che verrà rimossa la prima voce di criterio.

Non appena la voce di criterio viene rimossa dall'istanza in memoria del criterio globale, viene chiamato il cmdlet **Set-CsClientPolicy** per scrivere tali modifiche nell'istanza effettiva del criterio client globale.

    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.RemoveAt(0)
    
    Set-CsClientPolicy -Instance $y 

## ESEMPIO 4

Con il comando mostrato nell'esempio 4 vengono rimosse tutte le voci di criterio client configurate per il criterio globale. A tale scopo, viene utilizzato il parametro PolicyEntry e il relativo valore viene impostato su null ($Null).

    Set-CsClientPolicy -Identity global -PolicyEntry $Null

## Descrizione dettagliata

I criteri client sono il principale meccanismo utilizzato da Lync Server per gestire software client quale Lync. Quando si crea o si configura un criterio client, sono disponibili numerose opzioni. È ad esempio possibile specificare se utilizzare o meno foto in Lync, se consentire o meno l'utilizzo di emoticon nei messaggi istantanei e se le trascrizioni delle sessioni di messaggistica istantanea devono essere salvate automaticamente da Lync. Tali opzioni riguardano molte delle impostazioni relative ai client che gli amministratori devono gestire.

Potrebbero, tuttavia, non essere incluse tutte le impostazioni che gli amministratori devono gestire. Per maggiore flessibilità ed estendibilità, i criteri client presentano quindi una proprietà denominata PolicyEntry che può essere impostata su più valori e consente agli amministratori di aggiungere nuove opzioni di gestione non chiamate esplicitamente nei criteri client. Ad esempio, prima del rilascio di Lync Server, i tester della versione beta hanno avuto la possibilità di aggiungere un'opzione di feedback in Lync. Tale opzione è stata aggiunta come nuova voce di criterio e creata utilizzando il cmdlet **New-CsClientPolicyEntry**.

Si noti che non è possibile creare arbitrariamente nuove voci di criterio né si deve presumere che tali voci possano gestire Lync o altre applicazioni client. Sarà invece necessario attendere da Microsoft la notifica dei nomi e dei valori utilizzabili per creare nuove voci di criterio client.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsClientPolicyEntry** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicyEntry"}

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
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della nuova voce di criterio. Ad esempio: -Name &quot;URLFeedbackOnline&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Value</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il valore da assegnare alla nuova voce di criterio. Ad esempio: -Value http://www.litwareinc.com/feedback.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet New-CsClientPolicyEntry non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsClientPolicyEntry** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Client.PolicyEntryType.

## Vedere anche

#### Ulteriori risorse

[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

