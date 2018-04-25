---
title: New-CsCpsConfiguration
TOCTitle: New-CsCpsConfiguration
ms:assetid: bc740858-0e00-48ae-883e-67b3b7a03528
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412919(v=OCS.15)
ms:contentKeyID: 49301811
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCpsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni del servizio Parcheggio di chiamata. Quest'ultimo è un servizio che consente a un utente di "parcheggiare" una chiamata telefonica in arrivo. Parcheggiare una chiamata significa trasferirla a un numero (o codice orbit) di uno specifico intervallo e metterla immediatamente in attesa. Chiunque (non solo la persona che ha in origine risposto alla chiamata) può riprendere la conversazione da qualsiasi telefono immettendo il numero corretto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsCpsConfiguration -Identity <XdsIdentity> [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nel comando riportato nell'esempio 1 il cmdlet **New-CsCpsConfiguration** viene utilizzato per creare una configurazione del servizio di parcheggio di chiamata per il sito Redmond. Questa configurazione verrà creata con i valori predefiniti, ad eccezione di EnableMusicOnHold. Il comando imposta questa proprietà su False, per cui il chiamante la cui chiamata è stata parcheggiata non sentirà alcuna musica durante l'attesa. Il valore di EnableMusicOnHold è True per impostazione predefinita, presupponendo che il servizio di parcheggio di chiamata sia stato distribuito.

    New-CsCpsConfiguration -Identity site:Redmond -EnableMusicOnHold $False

## ESEMPIO 2

Nel comando riportato nell'esempio 2 viene utilizzato il cmdlet **New-CsCpsConfiguration** per creare una configurazione del servizio di parcheggio di chiamata per il sito Redmond1. Per impostazione predefinita nessun valore OnTimeoutURI viene fornito per cui questo esempio aggiunge un valore per questo parametro. In questo caso, il parametro OnTimeoutURI è impostato su sip:davidegarghentini@litwareinc.com. Il valore passato a questo parametro deve iniziare con la stringa "sip:" e puntare a un utente o a un Response Group che riceverà le chiamate parcheggiate che non ricevono risposta dopo un numero specificato di tentativi di richiamata.

    New-CsCpsConfiguration -Identity site:Redmond -OnTimeoutURI sip:kenmyer@litwareinc.com

## ESEMPIO 3

Nel comando viene utilizzato il cmdlet **New-CsCpsConfiguration** per creare una configurazione del servizio di parcheggio di chiamata per il sito Redmond1. Per questo sito, MaxCallPickupAttempts è stato impostato su 2. Ciò significa che la chiamata squillerà due volte.

    New-CsCpsConfiguration -Identity site:Redmond -MaxCallPickupAttempts 2

## Descrizione dettagliata

Questo cmdlet è utilizzato per creare una nuova configurazione del servizio di parcheggio di chiamata. Quando viene installato il servizio di parcheggio di chiamata, per impostazione predefinita vengono configurate le impostazioni globali, che possono essere aggiornate ma non rimosse. (La "rimozione" delle impostazioni globali ripristina semplicemente i valori predefiniti). Pertanto, questo cmdlet è utilizzato per creare solamente impostazioni specifiche per il sito.

In una configurazione di questo servizio viene specificato quanto accade a una chiamata quando viene parcheggiata. Se ad esempio non si risponde a una chiamata parcheggiata entro un determinato periodo di tempo, la chiamata può essere automaticamente inoltrata a un'altra persona, quale un amministratore o un Response Group. Le chiamate possono essere configurate in modo da far squillare il telefono dopo un determinato periodo, affinché la chiamata non venga dimenticata. Il servizio di parcheggio di chiamata può inoltre essere configurato per riprodurre una musica di attesa per il chiamante mentre la chiamata risulta parcheggiata.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsCpsConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCpsConfiguration"}

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
<td><p>Il sito su cui vengono applicate queste impostazioni. Il sito deve essere immesso nel formato site:&lt;nomesito&gt;, ad esempio site:Redmond. Sarà sempre presente una configurazione nell'ambito globale che non può essere rimossa. Non è possibile pertanto ricreare una configurazione globale con questo cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>L'intervallo di tempo trascorso dopo il parcheggio di una chiamata prima che squilli nuovamente il telefono su cui si è risposto alla chiamata.</p>
<p>Il tempo deve essere immesso nel formato hh:mm:ss (hh = ore, mm = minuti, ss = secondi)</p>
<p>Valore predefinito: 00:01:30 (90 secondi); Valore minimo: 10 secondi (00:00:10); Valore massimo: 10 minuti (00:10:00)</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se viene riprodotta della musica per il chiamante mentre una chiamata è parcheggiata.</p>
<p>Lync Server viene fornito con un file predefinito per la musica di attesa. Per cambiare file (e cambiare quindi la musica che il chiamante sente mentre la chiamata è parcheggiata), è possibile utilizzare il cmdlet <strong>Set-CsCallParkServiceMusicOnHoldFile</strong>.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Il numero di volte che il telefono utilizzato per rispondere a una chiamata successivamente parcheggiata deve squillare prima che la chiamata venga inoltrata all'URI (Uniform Resource Identifier) di fallback. L'URI di fallback viene impostato con il parametro OnTimeoutURI.</p>
<p>Valore predefinito: 1; Valore minimo: 1; Valore massimo: 10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'indirizzo SIP dell'utente o del gruppo di risposta a cui saranno instradate le chiamate parcheggiate senza risposta. La chiamata parcheggiata sarà instradata dopo il numero di richiamate automatiche definito nel parametro MaxCallPickupAttempts. Se il parametro è impostato su NULL, il parametro OnTimeoutURI verrà ignorato e la chiamata parcheggiata verrà disconnessa dopo i tentativi di richiamata non riusciti.</p>
<p>I valori devono essere URI SIP che iniziano con la stringa sip:, ad esempio, sip:rgs1@litwareinc.com.</p></td>
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

Nessuno.

## Tipi restituiti

Questo cmdlet crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

