---
title: Remove-CsPinPolicy
TOCTitle: Remove-CsPinPolicy
ms:assetid: 60bebb77-4181-4c5c-9c0e-dd1ece71f1d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398431(v=OCS.15)
ms:contentKeyID: 49300735
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPinPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il criterio PIN specificato. L'autenticazione tramite PIN e i criteri PIN consentono agli utenti di accedere a Lync Server immettendo il proprio PIN anziché il nome utente e la password. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsPinPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimosso il criterio PIN per utente con identità (Identity) RedmondUsersPinPolicy.

    Remove-CsPinPolicy -Identity RedmondUsersPinPolicy

## ESEMPIO 2

Il comando riportato nell'esempio 2 rimuove tutti i criteri PIN configurati nell'ambito del sito. A tale scopo, viene utilizzato il cmdlet **Get-CsPinPolicy** con il parametro Filter per restituire una raccolta di tutti i criteri la cui identità (Identity) inizia con i caratteri "site:". Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPinPolicy**, che elimina tutti i criteri nella raccolta.

    Get-CsPinPolicy -Filter "site:*" | Remove-CsPinPolicy

## ESEMPIO 3

Nell'esempio 3 vengono utilizzati i cmdlet **Get-CsPinPolicy**, **Where-Object** e **Remove-CsPinPolicy** per eliminare tutti i criteri PIN in cui la proprietà AllowCommonPatterns è impostata su True. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsPinPolicy** per ottenere una raccolta di tutti i criteri PIN configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui AllowCommonPatterns è uguale a True. La raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsPinPolicy**, che elimina tutti i criteri nella raccolta.

    Get-CsPinPolicy | Where-Object {$_.AllowCommonPatterns -eq $True} | Remove-CsPinPolicy

## ESEMPIO 4

Il comando riportato nell'esempio 4 elimina tutti i criteri PIN configurati negli ambiti del sito e per utente. A tale scopo, viene utilizzato il cmdlet **Get-CsPinPolicy** per ottenere una raccolta di tutti i criteri PIN configurati per l'utilizzo nell'organizzazione e quindi l'intera raccolta viene inviata tramite pipe al cmdlet **Remove-CsPinPolicy**. Si noti che in questa raccolta saranno inclusi anche i criteri globali. I criteri globali però non verranno eliminati e per tutte le relative proprietà verranno ripristinati i valori predefiniti.

    Get-CsPinPolicy | Remove-CsPinPolicy

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. In genere, l'accesso al sistema o la partecipazione a una conferenza richiedono l'immissione del nome utente e della password. Tale operazione può rappresentare un problema se si utilizza un telefono privo di tastierino alfanumerico. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché un nome utente e una password.

In Lync Server vengono utilizzati i criteri PIN per gestire le proprietà di autenticazione tramite PIN. È ad esempio possibile specificare una lunghezza minima per un PIN, nonché stabilire se sono accettabili i PIN che utilizzano "formati comuni", come cifre consecutive (ad esempio il PIN 123456). Oltre al criterio PIN globale, creato automaticamente quando si installa Lync Server, è possibile creare criteri PIN personalizzati applicabili nell'ambito del sito o per utente.

Il cmdlet **Remove-CsPinPolicy** consente di rimuovere i criteri per il PIN configurati nell'ambito del sito o per utente. Quando si rimuove un criterio nell'ambito del sito o nell'ambito per utente, il criterio verrà eliminato e non sarà più disponibile per l'utilizzo. Inoltre, tutti gli utenti a cui sono stati assegnati quei criteri erediteranno automaticamente il criterio successivo nella gerarchia dei criteri (globale, sito, servizio, per utente). Ad esempio, se si rimuove un criterio a livello di sito, tutti gli utenti a cui era stato assegnato quel criterio avranno le proprie impostazioni per il PIN gestite dal criterio globale.

Il cmdlet **Remove-CsPinPolicy** può anche essere eseguito per i criteri globali. In questo caso tuttavia i criteri non verranno rimossi, poiché non è possibile eliminare i criteri globali. Per tutte le proprietà dei criteri globali verranno invece ripristinati i valori predefiniti. Si supponga ad esempio di aver configurato i criteri globali in modo da utilizzare un PIN con una lunghezza minima di 11 cifre. Se si rimuovono i criteri globali, per la lunghezza minima del PIN verrà ripristinato il valore predefinito di 5 cifre.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsPinPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPinPolicy"}

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
<td><p>Identificatore univoco assegnato al criterio al momento della sua creazione. È possibile assegnare i criteri relativi ai PIN in ambito globale, del sito o per utente. Per fare riferimento all'istanza globale, utilizzare la seguente sintassi: -Identity global. Per fare riferimento a un criterio nell'ambito del sito, utilizzare la seguente sintassi: -Identity site:Redmond. Per fare riferimento a un criterio nell'ambito per utente, utilizzare una sintassi simile alla seguente: -Identity RedmondPINPolicy.</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy. Il cmdlet **Remove-CsPinPolicy** accetta l'input da pipeline dell'oggetto criterio PIN.

## Tipi restituiti

Il cmdlet **Remove-CsPinPolicy** non restituisce alcun oggetto o valore. Rimuove invece una o più istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

