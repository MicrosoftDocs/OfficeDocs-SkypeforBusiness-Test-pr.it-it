---
title: New-CsMediaConfiguration
TOCTitle: New-CsMediaConfiguration
ms:assetid: 3b60c36f-f824-4948-aa46-6745b40b9641
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425881(v=OCS.15)
ms:contentKeyID: 49300252
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMediaConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni multimediali. Queste impostazioni possono essere utilizzate per specificare elementi quali il livello di crittografia supportato e la risoluzione video massima consentita. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsMediaConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableQoS <$true | $false>] [-EnableSiren <$true | $false>] [-EncryptionLevel <SupportEncryption | RequireEncryption | DoNotSupportEncryption>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxVideoRateAllowed <CIF250K | VGA600K | Hd720p15M>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **New-CsMediaConfiguration** per creare una nuova configurazione multimediale con identità site:Redmond1. Questa nuova configurazione prevede che entrambe le parti coinvolte in una conversazione multimediale utilizzino la crittografia. Tale requisito viene imposto aggiungendo il parametro EncryptionLevel e impostandone il valore su RequireEncryption.

    New-CsMediaConfiguration -Identity site:Redmond1 -EncryptionLevel RequireEncryption

## ESEMPIO 2

In questo esempio viene utilizzato il cmdlet **New-CsMediaConfiguration** per creare una nuova configurazione multimediale con identità MediationServer:pool0.litwareinc.com. In questa nuova configurazione il parametro EnableSiren è impostato su True e di conseguenza il codec Siren è abilitato per le chiamate che coinvolgono tale Mediation Server.

    New-CsMediaConfiguration -Identity MediationServer:pool0.litwareinc.com -EnableSiren $True

## Descrizione dettagliata

Questo cmdlet consente di creare una nuova raccolta di impostazioni che definiscono i comportamenti per azioni multimediali specifiche.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsMediaConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsMediaConfiguration"}

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
<td><p>Un identificatore univoco che specifica l'ambito a cui viene applicata la configurazione (sito o servizio). Una configurazione nell'ambito del sito deve essere immessa come site:&lt;nome sito&gt; (ad esempio, site:Redmond). Un servizio deve essere immesso come &lt;ruolo server&gt;:&lt;fqdn&gt;, ad esempio, MediationServer:pool0.litwareinc.com. Esisterà sempre una configurazione multimediale nell'ambito globale che non potrà essere eliminata, per cui non sarà possibile creare una nuova configurazione globale.</p>
<p>Le configurazioni multimediali nell'ambito del servizio possono essere create solo per il servizio A/V Conferencing, Mediation Server e il server applicazioni.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableQoS</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>QoS consente di monitorare la qualità dei segnali vocali in una rete.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSiren</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Per impostazione predefinita, il Mediation Server non effettua la negoziazione di Siren come possibile codec per le chiamate con altri client Lync. Se questo parametro è impostato su True, Siren viene incluso come possibile codec per l'utilizzo tra il Mediation Server e altri client Lync.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EncryptionLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.EncryptionLevel</p></td>
<td><p>Livello di crittografia tra dispositivi per comunicazioni unificate.</p>
<p>Valori validi:</p>
<p>SupportEncryption - verrà utilizzato il protocollo SRTP (Secure Real-Time Transport Protocol), se può essere negoziato.</p>
<p>RequireEncryption: è necessario negoziare il protocollo SRTP.</p>
<p>DoNotSupportEncryption: il protocollo SRTP non deve essere utilizzato.</p>
<p>Valore predefinito: RequireEncryption</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxVideoRateAllowed</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.MaxVideoRateAllowed</p></td>
<td><p>La velocità massima di trasferimento dei segnali video agli endpoint client.</p>
<p>Valori validi: Hd720p15M, VGA600K, CIF250K</p>
<p>Hd720p15M: alta definizione, con risoluzione 1280 x 720 e proporzioni 16:9.</p>
<p>VGA600K: VGA, con risoluzione 640 x 480, 25 fps e proporzioni 4:3.</p>
<p>CIF250K: formato video CIF (Common Intermediate Format), 15 fps con risoluzione 352 x 288.</p>
<p>Si noti che questi valori non fanno distinzione tra maiuscole e minuscole e vengono convertiti nel formato maiuscolo/minuscolo corretto in fase di creazione della configurazione.</p>
<p>Valore predefinito: VGA600K</p></td>
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

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings.

## Vedere anche

#### Ulteriori risorse

[Remove-CsMediaConfiguration](remove-csmediaconfiguration.md)  
[Set-CsMediaConfiguration](set-csmediaconfiguration.md)  
[Get-CsMediaConfiguration](get-csmediaconfiguration.md)

