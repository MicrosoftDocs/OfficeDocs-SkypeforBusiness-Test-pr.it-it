---
title: Set-CsCpsConfiguration
TOCTitle: Set-CsCpsConfiguration
ms:assetid: 9c2c0ad1-12f8-47b6-a7ec-60d91c9685bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412721(v=OCS.15)
ms:contentKeyID: 49301447
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCpsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni del servizio Parcheggio di chiamata. Quest'ultimo è un servizio che consente a un utente di "parcheggiare" una chiamata telefonica in arrivo. Parcheggiare una chiamata significa trasferirla a un numero (o codice orbit) di uno specifico intervallo e quindi metterla immediatamente in attesa. Chiunque (non solo la persona che ha in origine risposto alla chiamata) può riprendere la conversazione da qualsiasi telefono immettendo il numero corretto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCpsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare la configurazione del servizio Parcheggio di chiamata con Identity site:Redmond1 impostando su 2 il numero massimo di volte che una chiamata parcheggiata può far squillare il telefono che risponde. Per ottenere questo risultato, viene incluso il parametro MaxCallPickupAttempts e il suo valore viene impostato su 2.

    Set-CsCpsConfiguration -Identity site:Redmond1 -MaxCallPickupAttempts 2

## ESEMPIO 2

Il comando riportato nell'esempio 2 è una variante del comando riportato nell'esempio 1. In questo caso però il valore della proprietà MaxCallPickupAttempts viene impostato su 2 per tutte le configurazioni del servizio Parcheggio di chiamata e non solo per una. A tale scopo, viene utilizzato il cmdlet **Get-CsCpsConfiguration** per recuperare una raccolta di tutte le impostazioni del servizio Parcheggio di chiamata in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsCpsConfiguration**, che imposta il valore 2 per la proprietà MaxCallPickupAttempts di ogni singolo elemento della raccolta.

    Get-CsCpsConfiguration | Set-CsCpsConfiguration -MaxCallPickupAttempts 2

## ESEMPIO 3

In questo esempio, la configurazione del servizio Parcheggio di chiamata per il sito Redmond1 viene modificata impostando su 45 secondi il valore della proprietà CallPickupTimeoutThreshold, cioè l'intervallo di tempo che deve trascorrere prima che una chiamata parcheggiata faccia squillare di nuovo il telefono.

    Set-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:00:45

## Descrizione dettagliata

Questo cmdlet consente di modificare la configurazione di un servizio Parcheggio di chiamata esistente. La configurazione di un servizio Parcheggio di chiamata indica cosa succede a una chiamata quando viene parcheggiata. Ad esempio, se non si risponde a una chiamata parcheggiata entro un determinato periodo, la chiamata può essere automaticamente inoltrata a un'altra persona, ad esempio un amministratore, o a un gruppo di risposta. Le chiamate possono essere configurate in modo da far squillare il telefono dopo un determinato periodo, affinché la chiamata non venga dimenticata. Inoltre, il servizio Parcheggio di chiamata può essere configurato per riprodurre una musica di attesa per il chiamante mentre la chiamata risulta parcheggiata.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsCpsConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCpsConfiguration"}

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
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>TimeSpan</p></td>
<td><p>L'intervallo di tempo trascorso dopo il parcheggio di una chiamata prima che squilli nuovamente il telefono su cui si è risposto alla chiamata.</p>
<p>Il tempo deve essere immesso in formato hh:mm:ss (hh = ore, mm = minuti, ss = secondi)</p>
<p>Valore minimo: 10 secondi (00:00:10); Valore massimo: 10 minuti (00:10:00)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Consente di stabilire se, mentre una chiamata è parcheggiata, viene riprodotta della musica per il chiamante.</p>
<p>Lync Server viene fornito con un file predefinito per la musica di attesa. Per cambiare file (e cambiare quindi la musica che il chiamante sente mentre la chiamata è parcheggiata), è possibile utilizzare il cmdlet <strong>Set-CsCallParkServiceMusicOnHoldFile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificatore univoco della configurazione da modificare. Identity specifica l'ambito di applicazione della configurazione, vale a dire Global o un sito specifico (nel formato site:&lt;nomeSito&gt;, ad esempio site:Redmond).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>CallParkServiceSettings</p></td>
<td><p>Riferimento a un oggetto di configurazione del servizio Parcheggio di chiamata di tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Per recuperare questo oggetto, è necessario utilizzare il cmdlet <strong>Get-CsCpsConfiguration</strong>. L'oggetto può quindi essere modificato e le modifiche possono essere salvate passando di nuovo l'oggetto al cmdlet <strong>Set-CsCpsConfiguration</strong> in questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Il numero di volte che il telefono utilizzato per rispondere a una chiamata successivamente parcheggiata deve squillare prima che la chiamata venga inoltrata all'URI (Uniform Resource Identifier) di fallback. L'URI di fallback viene impostato con il parametro OnTimeoutURI.</p>
<p>Valore minimo: 1; Valore massimo: 10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP dell'utente o del gruppo di risposta a cui saranno instradate le chiamate parcheggiate senza risposta. La chiamata parcheggiata sarà instradata dopo il numero di richiamate automatiche definito nel parametro MaxCallPickupAttempts. Se questo parametro viene impostato su Null, OnTimeoutURI verrà ignorato e la chiamata parcheggiata verrà disconnessa dopo un tentativo di richiamata non riuscito.</p>
<p>I valori devono essere URI SIP che iniziano con la stringa sip:, ad esempio sip:rgs1@litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Accetta input tramite pipeline da oggetti configurazione del servizio Parcheggio di chiamata.

## Tipi restituiti

Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

