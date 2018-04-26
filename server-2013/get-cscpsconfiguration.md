---
title: Get-CsCpsConfiguration
TOCTitle: Get-CsCpsConfiguration
ms:assetid: d81ee8fe-d02b-4f60-a4d5-6aa84f65d156
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398948(v=OCS.15)
ms:contentKeyID: 49302146
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCpsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sul servizio Parcheggio di chiamata. Quest'ultimo è un servizio che consente a un utente di "parcheggiare" una chiamata telefonica in arrivo. Parcheggiare una chiamata significa trasferirla a un numero (o codice orbit) di uno specifico intervallo e quindi metterla immediatamente in attesa. Chiunque (non solo la persona che ha in origine risposto alla chiamata) può riprendere la conversazione da qualsiasi telefono nel sistema immettendo il numero corretto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCpsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene recuperata una raccolta di tutte le configurazioni del servizio Parcheggio di chiamata definite per l'utilizzo nell'organizzazione.

    Get-CsCpsConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono recuperate solo le configurazioni del servizio Parcheggio di chiamata con valore Identity site:Redmond1.

    Get-CsCpsConfiguration -Identity site:Redmond1

## ESEMPIO 3

Nell'esempio 3 il parametro Filter viene utilizzato per restituire tutte le configurazioni del servizio Parcheggio di chiamata che sono state impostate nell'ambito del sito. La stringa con carattere jolly site:\* indica al cmdlet **Get-CsCpsConfiguration** di restituire solo le impostazioni in cui il valore Identity inizia con il valore stringa site:.

    Get-CsCpsConfiguration -Filter site:*

## ESEMPIO 4

Come nell'esempio 3, in questo esempio viene utilizzato il parametro Filter per recuperare un sottoinsieme di tutte le configurazioni del servizio Parcheggio di chiamata definite. In questo caso, viene applicato un filtro basato sulla stringa \*:re\* che restituisce le configurazioni del servizio Parcheggio di chiamata per tutti i siti con nomi che iniziamo con le lettere "re", come ad esempio Redmond1, Redmond 2 e RemoteComputer.

    Get-CsCpsConfiguration -Filter *:re*

## ESEMPIO 5

Nell'esempio 5 vengono restituite tutte le impostazioni del servizio Parcheggio di chiamata che non riproducono musica quando un chiamante viene messo in attesa. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsCpsConfiguration** per recuperare tutte le impostazioni del servizio Parcheggio di chiamata configurate per l'utilizzo nell'organizzazione. La raccolta vene quindi inviata tramite pipe al cmdlet **Where-Object** che applica un filtro per limitare i dati restituiti agli elementi in cui la proprietà EnableMusicOnHold è uguale a (-eq) False.

    Get-CsCpsConfiguration | Where-Object {$_.EnableMusicOnHold -eq $False}

## Descrizione dettagliata

Questo cmdlet consente di recuperare una o più configurazioni del servizio Parcheggio di chiamata. Una configurazione di tale servizio specifica cosa succede a una chiamata quando viene parcheggiata. Se ad esempio non si risponde a una chiamata parcheggiata entro un determinato periodo, la chiamata può essere automaticamente inoltrata a un'altra persona quale un amministratore o un gruppo di risposta. Le chiamate possono anche essere configurate in modo da far squillare il telefono dopo un determinato periodo di tempo, affinché la chiamata non venga dimenticata. Il servizio Parcheggio di chiamata può inoltre essere configurato per riprodurre una musica di attesa per il chiamante mentre la chiamata risulta parcheggiata.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsCpsConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCpsConfiguration"}

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
<td><p>Consente di eseguire una ricerca con caratteri jolly per recuperare solo le configurazioni con valori Identity che corrispondono alla stringa con caratteri jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco della configurazione del servizio Parcheggio di chiamata che si desidera recuperare. Questo identificatore sarà Global o site:&lt;nome sito&gt;, dove &lt;nome sito&gt; corrisponde al nome del sito a cui si applica la configurazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative al servizio Parcheggio di chiamata dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Recupera uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

