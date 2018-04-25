---
title: Remove-CsMediaConfiguration
TOCTitle: Remove-CsMediaConfiguration
ms:assetid: 8af2b8cb-4d58-4f8a-9acb-9b5104880bc9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398705(v=OCS.15)
ms:contentKeyID: 49301249
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMediaConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione multimediale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsMediaConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene utilizzato il cmdlet **Remove-CsMediaConfiguration** per eliminare la nuova raccolta di configurazioni multimediali con Identity site:Redmond1. Quando le impostazioni multimediali vengono rimosse dall'ambito del sito, il sito inizia automaticamente a utilizzare le impostazioni multimediali globali.

    Remove-CsMediaConfiguration -Identity site:Redmond1

## ESEMPIO 2

Nell'esempio 2 vengono utilizzati tre cmdlet (**Get-CsMediaConfiguration**, **Where-Object** e **Remove-CsMediaConfiguration**) per rimuovere tutte le raccolte di configurazioni multimediale che richiedono la crittografia per tutte le parti coinvolte nella conversazione. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsMediaConfiguration** per restituire tutte le raccolte di configurazioni multimediali dell'organizzazione. Le informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che applica un filtro per limitare i dati della pipeline alle raccolte in cui la proprietà EncryptionLevel è uguale a (-eq) RequireEncryption. L'insieme di dati filtrato viene infine passato al cmdlet **Remove-CsMediaConfiguration**, che elimina ogni elemento dell'insieme.

    Get-CsMediaConfiguration | Where-Object {$_.EncryptionLevel -eq "RequireEncryption"} | Remove-CsMediaConfiguration

## ESEMPIO 3

In questo esempio vengono rimosse tutte le configurazioni multimediali definite nell'ambito del servizio (ovvero la configurazione si applica a un servizio specifico). A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsMediaConfiguration** con il parametro Filter impostato su service:\*. Questo filtro recupera tutte le raccolte di configurazioni multimediali la cui identità (Identity) inizia con service:, ovvero tutte le raccolte nell'ambito del servizio. Il gruppo di raccolte viene quindi inviato tramite pipe al cmdlet **Remove-CsMediaConfiguration**, che le rimuove tutte.

    Get-CsMediaConfiguration -Filter service:* | Remove-CsMediaConfiguration

## Descrizione dettagliata

Questo cmdlet rimuove una raccolta di impostazioni multimediali. Queste impostazioni sono relative alle chiamate audio e video tra endpoint client.

Questo cmdlet può essere utilizzato anche per rimuovere le impostazioni multimediali globali. In questo caso, però, le impostazioni non vengono effettivamente rimosse; in realtà, vengono ripristinate ai loro valori predefiniti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsMediaConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsMediaConfiguration"}

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
<td><p>L'identificatore univoco delle impostazioni di configurazione multimediali che si desidera rimuovere. Questo identificatore specifica l'ambito a cui viene applicata la configurazione (globale, sito o servizio).</p></td>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings. Accetta input tramite pipeline da oggetti configurazione multimediale.

## Tipi restituiti

Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsMediaConfiguration](new-csmediaconfiguration.md)  
[Set-CsMediaConfiguration](set-csmediaconfiguration.md)  
[Get-CsMediaConfiguration](get-csmediaconfiguration.md)

