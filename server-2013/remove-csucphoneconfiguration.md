---
title: Remove-CsUCPhoneConfiguration
TOCTitle: Remove-CsUCPhoneConfiguration
ms:assetid: 1b2d9601-3206-48d9-a846-4486b606aad0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398249(v=OCS.15)
ms:contentKeyID: 49299843
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUCPhoneConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione di Lync Phone Edition. Tra queste impostazioni sono incluse la modalità di sicurezza richiesta e la possibilità di scegliere se il telefono debba o meno bloccarsi automaticamente dopo un periodo di inattività specifico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsUCPhoneConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di rimuovere le impostazioni di configurazione del telefono per le comunicazioni unificate per il sito Redmond (-Identity site:Redmond). Quando le impostazioni vengono rimosse dall'ambito di un sito, i telefoni UC degli utenti di quel sito verranno gestiti in base alle impostazioni di configurazione globali.

    Remove-CsUCPhoneConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le impostazioni dei telefoni per le comunicazioni unificate configurate nell'ambito del sito. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsUCPhoneConfiguration** e il parametro Filter per restituire tutte le impostazioni configurate nell'ambito del sito. Il valore di filtro "site:\*" restituisce solo i dati relativi alle impostazioni la cui proprietà Identity (l'unica proprietà in base alla quale è possibile filtrare i dati) inizia con il valore stringa "site:". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsUCPhoneConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsUCPhoneConfiguration -Filter site:* | Remove-CsUCPhoneConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono rimosse tutte le impostazioni dei telefoni per le comunicazioni unificate che non applicano il blocco del telefono. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsUCPhoneConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni dei telefoni per le comunicazioni unificate attualmente in uso nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnforceLockProperty è uguale a False. Questa raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsUCPhoneConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsUCPhoneConfiguration | Where-Object {$_.EnforcePhoneLock -eq $False} | Remove-CsUCPhoneConfiguration

## ESEMPIO 4

Nell'esempio 4 vengono eliminate tutte le impostazioni di configurazione dei telefoni per le comunicazioni unificate per le quali la modalità di sicurezza SIP è bassa o media. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsUCPhoneConfiguration** per restituire una raccolta di tutte le impostazioni dei telefoni per le comunicazioni unificate configurate per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni per le quali la proprietà SIPSecurityMode è configurata su Low o Medium. A tale scopo, vengono selezionate le impostazioni per le quali la proprietà SIPSecurityMode è diversa da High. Sono previsti tre valori possibili per la proprietà SIPSecurityMode, ovvero Low, Medium e High. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsUCPhoneConfiguration**, che elimina tutte le impostazioni per le quali la proprietà SIPSecurityMode è diversa da High.

    Get-CsUCPhoneConfiguration | Where-Object {$_.SIPSecurityMode -ne "High"} | Remove-CsUCPhoneConfiguration

## Descrizione dettagliata

Lync Phone Edition rappresenta l'unione del telefono e di Lync Server. Lync Phone Edition utilizza un componente hardware speciale (ovvero un telefono compatibile con Lync) in grado di funzionare come telefono VoIP. Questo componente hardware può inoltre fungere da endpoint di Lync: è possibile impostare il proprio stato corrente, verificare lo stato dei contatti di Lync, cercare nuovi contatti e svolgere gran parte delle altre attività che solitamente vengono svolte con Lync.

Lync Server è fornito con una serie di cmdlet che consentono di gestire i telefoni Lync Phone Edition. È ad esempio possibile controllare aspetti quali la lunghezza minima del PIN utilizzato per accedere al telefono e se il telefono deve bloccarsi automaticamente dopo uno specifico periodo di inattività.

Le impostazioni di configurazione del telefono per le comunicazioni unificate possono essere applicate nell'ambito globale o nell'ambito del sito. Le impostazioni applicate nell'ambito del sito hanno la precedenza su quelle applicate nell'ambito globale. Quando si installa Lync Server, viene creato un unico insieme di impostazioni di configurazione del telefono per le comunicazioni unificate, che viene applicato nell'ambito globale. È tuttavia possibile utilizzare in qualsiasi momento il cmdlet **New-CsUCPhoneConfiguration** per creare una raccolta di impostazioni applicate nell'ambito del sito. Ciò consente di personalizzare la gestione dei telefoni per le comunicazioni unificate, in modo da rispondere alle specifiche esigenze di ogni singolo sito.

Le impostazioni create tramite il cmdlet **New-CsUCPhoneConfiguration** possono successivamente essere rimosse utilizzando il cmdlet **Remove-CsUCPhoneConfiguration**. Quando si rimuovono queste impostazioni da un sito, i telefoni con Lync Phone Edition in tale sito non vengono lasciati privi di gestione. Al contrario, vengono automaticamente inclusi nell'ambito delle impostazioni globali.

È possibile utilizzare il cmdlet **Remove-CsUCPhoneConfiguration** anche per le impostazioni globali. In tal caso, però, le impostazioni globali non verranno effettivamente rimosse perché non è possibile rimuovere le impostazioni globali dei telefoni per le comunicazioni unificate. In realtà, per le proprietà delle impostazioni globali verranno ripristinati i valori predefiniti. Ad esempio, se l'intervallo di tempo per il blocco del telefono è stato portato a 30 minuti, la "rimozione" delle impostazioni globali ripristinerà l'intervallo di tempo predefinito pari a 10 minuti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsUCPhoneConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUCPhoneConfiguration"}

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
<td><p>Identificatore univoco della raccolta di impostazioni di configurazione del telefono UC da rimuovere. Per eliminare una raccolta del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per rimuovere (ripristinare) la raccolta globale, utilizzare la seguente sintassi: -Identity global. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità di un criterio.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings. Il cmdlet **Remove-CsUCPhoneConfiguration** accetta le istanze dell'oggetto impostazioni dei telefoni per le comunicazioni unificate inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet rimuove invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)  
[New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)  
[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)

