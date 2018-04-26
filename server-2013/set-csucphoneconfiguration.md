---
title: Set-CsUCPhoneConfiguration
TOCTitle: Set-CsUCPhoneConfiguration
ms:assetid: f77456aa-992a-47d2-bdc7-5e3cbbfb6926
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413042(v=OCS.15)
ms:contentKeyID: 49302517
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUCPhoneConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare le opzioni di gestione disponibili per Lync Phone Edition. Tra queste sono incluse la modalità di sicurezza necessaria e la possibilità di scegliere se il telefono debba o meno bloccarsi dopo un determinato periodo di inattività. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUCPhoneConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUCPhoneConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CalendarPollInterval <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnforcePhoneLock <$true | $false>] [-Force <SwitchParameter>] [-LoggingLevel <Off | Low | Medium | High>] [-MinPhonePinLength <Byte>] [-PhoneLockTimeout <TimeSpan>] [-SIPSecurityMode <Low | Medium | High>] [-Voice8021p <Byte>] [-VoiceDiffServTag <Byte>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 si imposta la modalità di protezione SIP delle impostazioni globali del telefono per le comunicazioni unificate su Medio.

    Set-CsUCPhoneConfiguration -Identity global -SIPSecurityMode "Medium"

## ESEMPIO 2

Nell'esempio 2 vengono modificate le impostazioni del telefono per le comunicazioni unificate configurate per il sito di Redmond. In questo caso, la proprietà PhoneLockTimeout viene impostata su 30 minuti includendo il parametro PhoneLockTimeout e il valore di parametro "00:30:00" (00 ore: 30 minuti: 00 secondi).

    Set-CsUCPhoneConfiguration -Identity site:Redmond -PhoneLockTimeout "00:30:00"

## ESEMPIO 3

L'esempio 3 rappresenta una variazione del comando mostrato nell'esempio 2. In questo caso, tuttavia, la proprietà PhoneLockTimeout viene modificata per tutte le impostazioni del telefono per le comunicazioni unificate configurate nell'ambito del sito. Per questo scopo, viene inizialmente chiamato il cmdlet **Get-CsUCPhoneConfiguration**. Il parametro Filter e il valore del filtro "site:\*" limitano i dati restituiti alle impostazioni del telefono configurate nell'ambito del sito. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsUCPhoneConfiguration**, che utilizza il parametro PhoneLockTimeout e il valore di parametro "00:30:00" (00 ore: 30 minuti: 00 secondi) per impostare il valore di timeout per il blocco del telefono per ogni elemento della raccolta su 30 minuti.

    Get-CsUCPhoneConfiguration -Filter "site:*" | Set-CsUCPhoneConfiguration -PhoneLockTimeout "00:30:00"

## ESEMPIO 4

Nell'esempio 4 vengono configurate le proprietà EnforcePhoneLock e PhoneLockTimeout per tutte le impostazioni del telefono per le comunicazioni unificate in cui la modalità di sicurezza SIP è impostata su Bassa o Media. Per eseguire questa attività, viene prima utilizzato il cmdlet **Get-CsUCPhoneConfiguration** per restituire tutte le impostazioni di configurazione del telefono per le comunicazioni unificate nell'organizzazione. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che utilizza solo le impostazioni in cui la proprietà SIPSecurityMode è diversa da Alta. Poiché la sicurezza SIP può essere impostata solo su Bassa, Media o Alta, questa clausola selezionerà tutte le impostazioni in cui SIPSecurityMode è impostato su Bassa o Media. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsUCPhoneConfiguration**, che utilizza i parametri EnforcePhoneLock e PhoneLockTimeout per modificare le proprietà di blocco del telefono e di timeout per il blocco.

    Get-CsUCPhoneConfiguration | Where-Object {$_.SIPSecurityMode -ne "High"} | Set-CsUCPhoneConfiguration -EnforcePhoneLock $True -PhoneLockTimeout "00:30:00"

## ESEMPIO 5

Nell'esempio 5, il valore di timeout per il blocco del telefono è impostato su 10 minuti per tutte le impostazioni del telefono per le comunicazioni unificate in cui la proprietà PhoneLockTimeout ha un valore inferiore a 10 minuti. In questo modo, il valore di 10 minuti diventa il timeout minimo per il blocco del telefono in tutta l'organizzazione. Per questo scopo, viene prima utilizzato il cmdlet **Get-CsUCPhoneConfiguration** per restituire una raccolta di tutte le impostazioni del telefono per le comunicazioni unificate in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che sceglie solo le impostazioni in cui la proprietà PhoneLockTimeout è inferiore a 10 minuti (00 ore: 10 minuti: 00 secondi). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsUCPhoneConfiguration**, che imposta il valore PhoneLockTimeout per ogni elemento della raccolta su 10 minuti.

    Get-CsUCPhoneConfiguration | Where-Object {$_.PhoneLockTimeout -lt "00:10:00"} | Set-CsUCPhoneConfiguration -PhoneLockTimeout "00:10:00"

## Descrizione dettagliata

Lync Phone Edition rappresenta l'unione del telefono e di Lync Server. Lync Phone Edition utilizza un componente hardware speciale, ovvero un telefono compatibile con Lync, in grado di funzionare come telefono VoIP (Voice over Internet Protocol). Questo componente hardware può inoltre fungere da endpoint di Lync: è possibile impostare lo stato corrente, verificare lo stato dei contatti di Lync, cercare nuovi contatti e svolgere gran parte delle altre attività che solitamente vengono svolte con Lync.

I cmdlet **CsUCPhoneConfiguration** consentono di utilizzare le impostazioni di configurazione per la gestione dei telefoni che eseguono Lync Server. Ad esempio, è possibile controllare aspetti quali la lunghezza minima del PIN (Personal Identification Number) utilizzato per accedere al telefono e se il telefono deve bloccarsi automaticamente dopo uno specifico periodo di inattività.

Le impostazioni di configurazione del telefono per le comunicazioni unificate possono essere applicate all'ambito globale o all'ambito del sito. Quando si installa inizialmente Lync Server, viene creato un singolo set di impostazioni di configurazione del telefono per le comunicazioni unificate e viene applicato all'ambito globale. Tuttavia, in qualsiasi momento è possibile utilizzare il cmdlet **New-CsUCPhoneConfiguration** per creare una raccolta di impostazioni applicate all'ambito del sito. In questo modo la gestione del telefono per le comunicazioni unificate può essere adattata alle esigenze specifiche di ogni singolo sito.

Oltre a creare nuove raccolte di impostazioni del telefono per le comunicazioni unificate, è possibile utilizzare il cmdlet **Set-CsUCPhoneConfiguration** per modificare i valori delle proprietà per una raccolta esistente. Ad esempio, la registrazione è disabilitata per impostazione predefinita per i telefoni per le comunicazioni unificate. Per abilitare la registrazione a livello globale, è possibile utilizzare il cmdlet **Set-CsUCPhoneConfiguration** per modificare il valore della proprietà LoggingLevel della raccolta globale su True.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsUCPhoneConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUCPhoneConfiguration"}

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
<td><p><em>CalendarPollInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica con quale frequenza il dispositivo per le comunicazioni unificate recupera informazioni dal calendario di Outlook. Il valore deve essere specificato utilizzando il formato ore:minuti:secondi; ad esempio, per impostare l'intervallo di tempo su 1 ora, ovvero l'intervallo massimo consentito, utilizzare la sintassi seguente: -CalendarPollInterval &quot;01:00:00&quot;. Il valore predefinito è 3 minuti (00:03:00).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnforcePhoneLock</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se i telefoni per le comunicazioni unificate vengono bloccati automaticamente dopo il numero di minuti specificato da PhoneLockTimeout. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Rappresenta l'identificatore univoco assegnato alla raccolta di impostazioni di configurazione del telefono per le comunicazioni unificate. Utilizzare la sintassi di seguito per fare riferimento alle impostazioni globali: -Identity global. Per fare riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare caratteri jolly per specificare un'identità.</p>
<p>Se questo parametro viene omesso, il cmdlet <strong>Set-CsUCPhoneConfiguration</strong> modificherà le impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto UcPhoneSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>LoggingLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LoggingLevel</p></td>
<td><p>Consente la registrazione nel dispositivo per le comunicazioni unificate. I valori validi sono Disattivato, Basso, Medio e Alto. Il valore predefinito è Disattivato.</p></td>
</tr>
<tr class="even">
<td><p><em>MinPhonePinLength</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Byte</p></td>
<td><p>Specifica il numero minimo di cifre richiesto per i PIN (Personal Identification Number).</p>
<p>Valore minimo: 4</p>
<p>Valore massimo: 15</p>
<p>Valore predefinito: 6</p></td>
</tr>
<tr class="odd">
<td><p><em>PhoneLockTimeout</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica il periodo di tempo, in minuti, in cui un telefono per le comunicazioni unificate può restare inattivo prima che venga automaticamente attivato il blocco.</p>
<p>Il valore deve essere inferiore a 01:00:00 (1 ora). Il valore predefinito è 00:10:00 (10 minuti).</p></td>
</tr>
<tr class="even">
<td><p><em>SIPSecurityMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.SIPSecurityMode</p></td>
<td><p>Specifica il livello di sicurezza che il server applica alle sessioni SIP avviate mediante un telefono per le comunicazioni unificate.</p>
<p>I valori validi sono:</p>
<p>Bassa (consente qualsiasi tipo di autorizzazione o trasporto).</p>
<p>Media (è necessario NTLM o Kerberos per l'autenticazione degli utenti).</p>
<p>Alta (è necessario NTLM o Kerberos per l'autenticazione degli utenti e TLS per le connessioni SIP).</p>
<p>Il valore predefinito è High.</p></td>
</tr>
<tr class="odd">
<td><p><em>Voice8021p</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Byte</p></td>
<td><p>Specifica il valore della priorità utente (il valore 802.1p) per il traffico vocale nella distribuzione di Lync Server.</p>
<p>Questa impostazione viene applicata solo nelle reti in cui i commutatori e i bridge supportano lo standard 802.1p. Il valore minimo per questa proprietà è 0 e il valore massimo è 7. Il valore predefinito è 0.</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceDiffServTag</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Byte</p></td>
<td><p>Specifica la rappresentazione decimale dell'indicazione di priorità DSCP (DiffServ Code Point) a 6 bit che definisce l'opzione PHB (Per Hop Behavior) per i pacchetti IP passati dai telefoni per le comunicazioni unificate gestiti da questo server.</p>
<p>Questo valore deve essere compreso tra 0 e 63, inclusi. Il valore predefinito è 40.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings. Il cmdlet **Set-CsUCPhoneConfiguration** accetta istanze inviate tramite pipe dell'oggetto delle impostazioni del telefono per le comunicazioni unificate.

## Tipi restituiti

Il cmdlet **Set-CsUCPhoneConfiguration** non restituisce un valore o un oggetto. Il cmdlet configura invece istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)  
[New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)  
[Remove-CsUCPhoneConfiguration](remove-csucphoneconfiguration.md)

