---
title: Get-CsUCPhoneConfiguration
TOCTitle: Get-CsUCPhoneConfiguration
ms:assetid: 014bba9e-b5c4-477d-9273-c993e7a7ee9e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398070(v=OCS.15)
ms:contentKeyID: 49299485
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUCPhoneConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle opzioni di gestione disponibili per Lync Phone Edition. Tra queste sono incluse la modalità di sicurezza necessaria e la possibilità di scegliere se il telefono debba o meno bloccarsi dopo un determinato periodo di inattività. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUCPhoneConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUCPhoneConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce tutte le impostazioni di configurazione dei telefoni UC attualmente in uso nell'organizzazione. La chiamata del cmdlet **Get-CsUCPhoneConfiguration** senza ulteriori parametri restituisce sempre la raccolta completa delle impostazioni di configurazione dei telefoni.

    Get-CsUCPhoneConfiguration

## ESEMPIO 2

Nell'Esempio 2, vengono restituite solo le impostazioni di configurazione dei telefoni UC con Identity site:Redmond. Dal momento che i valori per l'identità (Identity) devono essere univoci, questo comando non restituirà mai più di una raccolta di impostazioni di configurazione del telefono.

    Get-CsUCPhoneConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le impostazioni dei telefoni UC configurate nell'ambito del sito. A tale scopo, viene chiamato il cmdlet **Get-CsUCPhoneConfiguration** con il parametro Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi alle impostazioni in cui la proprietà Identity (l'unica in base alla quale è possibile filtrare) inizia con il valore stringa "site:". Per definizione, qualsiasi impostazione in cui la proprietà Identity inizia con il valore stringa "site:" è stata configurata nell'ambito del sito.

    Get-CsUCPhoneConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 vengono restituite le impostazioni di configurazione dei telefoni UC in cui la modalità di sicurezza SIP è impostata su Media. La sicurezza SIP può essere impostata su Bassa, Media o Avanzata. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsUCPhoneConfiguration** senza alcun parametro aggiuntivo in modo da restituire una raccolta di tutte le impostazioni dei telefoni UC configurate per l'utilizzo nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà SIPSecurityMode è uguale a Medium.

    Get-CsUCPhoneConfiguration | Where-Object {$_.SIPSecurityMode -eq "Medium"}

## ESEMPIO 5

Nell'esempio 5 vengono restituite le impostazioni dei telefoni UC che soddisfano almeno uno dei criteri seguenti: 1) non viene applicato il blocco del telefono e/o 2) la lunghezza minima del codice PIN è inferiore a 6 cifre. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsUCPhoneConfiguration** per restituire una raccolta di tutte le impostazioni dei telefoni UC attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli elementi che soddisfano almeno uno dei criteri seguenti: 1) la proprietà EnforcePhoneLock è uguale a False e/o 2) la proprietà MinPhoneLength è minore di 6.

L'operatore -or indica al cmdlet **Where-Object** che deve selezionare le impostazioni che soddisfano uno o entrambi i criteri. Per selezionare le impostazioni che soddisfano entrambi i criteri (in questo caso, che indicano che non viene applicato il blocco del telefono e che la lunghezza del codice PIN è inferiore a 6), utilizzare l'operatore -and:

Where-Object {$\_.EnforcePhoneLock -eq $False -and $\_.MinPhonePinLength -lt 6}

    Get-CsUCPhoneConfiguration | Where-Object {$_.EnforcePhoneLock -eq $False -or $_.MinPhonePinLength -lt 6}

## Descrizione dettagliata

Lync Phone Edition rappresenta l'unione del telefono e di Lync Server. Lync Phone Edition utilizza un componente hardware speciale (cioè un telefono compatibile con Lync) in grado di funzionare come telefono VoIP. Questo componente hardware può inoltre fungere da endpoint di Lync: è possibile impostare il proprio stato corrente, verificare lo stato dei contatti di Lync, cercare nuovi contatti e svolgere gran parte delle altre attività che solitamente vengono svolte con Lync.

I cmdlet CsUCPhoneConfiguration consentono di gestire i propri telefoni di Lync Phone Edition. È ad esempio possibile definire la lunghezza minima del PIN utilizzato per accedere al telefono oppure se il telefono deve bloccarsi automaticamente dopo un periodo di inattività specificato.

Le impostazioni di configurazione dei telefoni possono essere applicate nell'ambito globale o a livello di sito. Le impostazioni applicate a livello di sito hanno la precedenza su quelle applicate nell'ambito globale. Il cmdlet **Get-CsUCPhoneConfiguration** consente di recuperare le informazioni sulle impostazioni correnti dei telefoni nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsUCPhoneConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUCPhoneConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per ottenere una o più raccolte di impostazioni di configurazione dei telefoni UC. Ad esempio, per ottenere una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter site:*. Per restituire una raccolta di tutte le impostazioni che contengono il valore stringa &quot;EMEA&quot; in Identity (l'unica proprietà su cui è possibile applicare il filtro), utilizzare la sintassi riportata di seguito: -Filter *EMEA*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di configurazione dei telefoni UC (unified communications) che si desidera ottenere. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per ottenere una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità (Identity). Se si desidera utilizzare i caratteri jolly, includere il parametro Filter.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsUCPhoneConfiguration</strong> restituirà una raccolta di tutte le impostazioni di configurazione dei telefoni UC utilizzate nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione dei telefoni UC dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsUCPhoneConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUCPhoneConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)  
[Remove-CsUCPhoneConfiguration](remove-csucphoneconfiguration.md)  
[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)

