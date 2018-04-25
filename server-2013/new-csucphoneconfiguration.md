---
title: New-CsUCPhoneConfiguration
TOCTitle: New-CsUCPhoneConfiguration
ms:assetid: 633a593e-565d-4c04-affb-589502050212
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398445(v=OCS.15)
ms:contentKeyID: 49300776
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUCPhoneConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni utilizzate per gestire Lync Phone Edition. Queste impostazioni consentono di configurare elementi come la modalità di sicurezza richiesta e di specificare se il telefono deve essere bloccato automaticamente dopo un determinato periodo di inattività. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsUCPhoneConfiguration -Identity <XdsIdentity> [-CalendarPollInterval <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnforcePhoneLock <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LoggingLevel <Off | Low | Medium | High>] [-MinPhonePinLength <Byte>] [-PhoneLockTimeout <TimeSpan>] [-SIPSecurityMode <Low | Medium | High>] [-Voice8021p <Byte>] [-VoiceDiffServTag <Byte>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni dei telefoni UC per il sito Redmond. In questo esempio sono inclusi due parametri facoltativi insieme al parametro obbligatorio Identity: CalendarPollInterval, che imposta il tempo di polling del calendario su 10 minuti (00 ore: 10 minuti: 00 secondi), e LoggingLevel, che imposta il livello di registrazione dei telefoni UC su Medium. Quando viene completato il comando, vengono applicate le nuove impostazioni al sito Redmond e i telefoni UC degli utenti in tale sito saranno governati dalle nuove impostazioni. Questo comando avrà esito negativo se il sito Redmond include già una raccolta di impostazioni dei telefoni UC.

    New-CsUCPhoneConfiguration -Identity site:Redmond -CalendarPollInterval "00:10:00" -LoggingLevel "Medium"

## ESEMPIO 2

Con l'esempio 2 viene dimostrato l'uso del parametro InMemory, che consente di creare un nuovo set di impostazioni del telefono UC esistenti solo in memoria. Queste impostazioni vengono memorizzate nella variabile $x. Dopo la creazione di questa raccolta virtuale è possibile modificare le impostazioni solo in memoria utilizzando comandi simili a quelli mostrati nelle righe 2 e 3 dell'esempio: nella riga 2, la proprietà CalendarPollInterval viene impostata su 10 minuti (00 ore: 10 minuti: 00 secondi), mentre nella riga 3 la proprietà LoggingLevel viene impostata su Medium.

Dopo aver completato la modifica dei valori delle proprietà, è possibile utilizzare il cmdlet **Set-CsUCPhoneConfiguration** per trasformare le impostazioni virtuali archiviate in $x in una raccolta effettiva di impostazioni applicate al sito Redmond. Con l'utilizzo del parametro InMemory, le impostazioni non vengono applicate finché non viene chiamato il cmdlet **Set-CsUCPhoneConfiguration**. Se questo cmdlet non viene chiamato, le impostazioni virtuali scompariranno quando si termina la sessione di Windows PowerShell o se si elimina la variabile $x.

    $x = New-CsUCPhoneConfiguration -Identity site:Redmond -InMemory
    $x.CalendarPollInterval = "00:10:00" 
    $x.LoggingLevel = "Medium"
    Set-CsUCPhoneConfiguration -Instance $x

## Descrizione dettagliata

Lync Phone Edition rappresenta l'unione del telefono e di Lync Server. Lync Phone Edition utilizza un componente hardware speciale (ovvero un telefono compatibile con Lync Phone Edition) in grado di funzionare come telefono VoIP. Questo componente hardware può inoltre fungere da endpoint di Lync: è possibile impostare il proprio stato corrente, verificare lo stato dei contatti di Lync, cercare nuovi contatti e svolgere gran parte delle altre attività che solitamente vengono svolte con Lync.

Lync Server viene fornito con una serie di cmdlet che consentono di gestire i telefoni Lync Phone Edition. È ad esempio possibile controllare aspetti quali la lunghezza minima del PIN utilizzato per accedere al telefono e se il telefono deve bloccarsi automaticamente dopo uno specifico periodo di inattività.

Le impostazioni di configurazione del telefono per le comunicazioni unificate possono essere applicate nell'ambito globale o nell'ambito del sito. Le impostazioni applicate nell'ambito del sito hanno la precedenza su quelle applicate nell'ambito globale. Quando si installa Lync Server, viene creato un unico insieme di impostazioni di configurazione del telefono per le comunicazioni unificate, che viene applicato nell'ambito globale. Tuttavia, in qualsiasi momento è possibile utilizzare il cmdlet **New-CsUCPhoneConfiguration** per creare una raccolta di impostazioni applicate nell'ambito del sito. Ciò consente di personalizzare la gestione dei telefoni per le comunicazioni unificate, in modo da rispondere alle specifiche esigenze di ogni singolo sito.

Il cmdlet **New-CsUCPhoneConfiguration** consente di creare nell'ambito del sito nuove impostazioni del telefono per le comunicazioni unificate. Può esistere una sola raccolta di impostazioni per sito. Si supponga ad esempio di creare una raccolta di impostazioni con identità (Identity) site:Redmond e che al sito Redmond sia già assegnato un set di impostazioni del telefono per le comunicazioni unificate. In tal caso, il comando avrà esito negativo. È necessario invece eseguire una delle due operazioni seguenti: rimuovere le impostazioni esistenti e quindi utilizzare il cmdlet **New-CsUCPhoneConfiguration** per creare una nuova raccolta di impostazioni oppure utilizzare semplicemente il cmdlet **Set-CsUCPhoneConfiguration** per modificare le impostazioni esistenti.

Non è possibile creare una nuova raccolta di impostazioni nell'ambito globale. L'unica operazione che è possibile eseguire nell'ambito globale è utilizzare il cmdlet **Set-CsUCPhoneConfiguration** per modificare le impostazioni esistenti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsUCPhoneConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUCPhoneConfiguration"}

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
<td><p>Rappresenta l'identificatore univoco da assegnare alla nuova raccolta di impostazioni di configurazione del telefono per le comunicazioni unificate. Poiché è possibile creare nuove raccolte solo nell'ambito del sito, l'identità avrà sempre il prefisso &quot;site:&quot; seguito dal nome del sito, come, ad esempio, &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>CalendarPollInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica con quale frequenza il dispositivo per le comunicazioni unificate recupera informazioni dal calendario di Outlook. Il valore deve essere specificato utilizzando il formato ore:minuti:secondi. Per impostare ad esempio l'intervallo di tempo su 1 ora, ovvero l'intervallo massimo consentito, utilizzare la sintassi seguente: -CalendarPollInterval &quot;01:00:00&quot;. Il valore predefinito è 3 minuti (00:03:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnforcePhoneLock</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se i telefoni per le comunicazioni unificate vengono bloccati automaticamente dopo il numero di minuti specificato da PhoneLockTimeout. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>LoggingLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LoggingLevel</p></td>
<td><p>Consente la registrazione sul dispositivo UC. I valori validi sono Disattivato, Basso, Medio e Alto. Il valore predefinito è Disattivato.</p>
<p></p></td>
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
<p>Questa impostazione viene applicata solo alle reti in cui gli switch e i bridge supportano lo standard 802.1p. Il valore minimo per questa proprietà è 0 e il valore massimo è 7. Il valore predefinito è 0.</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceDiffServTag</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Byte</p></td>
<td><p>Specifica la rappresentazione decimale dell'indicazione di priorità DSCP (DiffServ Code Point) a 6 bit, che definisce l'opzione PHB (Per Hop Behavior) per i pacchetti IP passati dai telefoni per le comunicazioni unificate gestiti da questo server.</p>
<p>Questo valore deve essere compreso tra 0 e 63, inclusi. Il valore predefinito è 40.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p>
<p></p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsUCPhoneConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet crea istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)  
[Remove-CsUCPhoneConfiguration](remove-csucphoneconfiguration.md)  
[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)

