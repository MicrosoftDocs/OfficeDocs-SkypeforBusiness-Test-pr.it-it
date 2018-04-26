---
title: Set-CsMediaConfiguration
TOCTitle: Set-CsMediaConfiguration
ms:assetid: 768bc273-5253-4569-895d-5b1127386b92
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398580(v=OCS.15)
ms:contentKeyID: 49301012
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMediaConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni multimediali. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsMediaConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMediaConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableQoS <$true | $false>] [-EnableSiren <$true | $false>] [-EncryptionLevel <SupportEncryption | RequireEncryption | DoNotSupportEncryption>] [-Force <SwitchParameter>] [-MaxVideoRateAllowed <CIF250K | VGA600K | Hd720p15M>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene modificata la raccolta di configurazioni multimediali con l'identità site:Redmond1. In particolare, il comando imposta il valore della proprietà MaxVideoRateAllowed su Hd720p15M. Si noti che il valore passato al parametro MaxVideoRateAllowed deve essere uno dei valori specificati nella descrizione del parametro. Si noti inoltre per i valori non viene applicata la distinzione tra maiuscole e minuscole. Il valore immesso qui come hd720p15m verrà convertito automaticamente nella forma appropriata, in questo caso Hd720p15M.

    Set-CsMediaConfiguration -Identity site:Redmond1 -MaxVideoRateAllowed hd720p15m

## ESEMPIO 2

Con questo esempio la raccolta di configurazioni multimediali con identità site:Redmond1 viene modificata in modo da utilizzare il valore DoNotSupportEncryption per EncryptionLevel. Questo valore non fa distinzione tra maiuscole e minuscole; il valore è stato immesso come donotsupportencryption, ma sarà considerato valido in quanto viene automaticamente convertito nella forma mista (DoNotSupportEncryption).

    Set-CsMediaConfiguration site:Redmond1 -EncryptionLevel donotsupportencryption

## Descrizione dettagliata

Questo cmdlet consente di modificare una raccolta di impostazioni che definiscono la configurazione multimediale. Queste azioni sono relative a chiamate audio e video tra endpoint client.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsMediaConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMediaConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableQoS</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>QoS consente di monitorare la qualità dei segnali vocali in una rete.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSiren</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Per impostazione predefinita, il Mediation Server non effettua la negoziazione di Siren come possibile codec per le chiamate tra se stesso e altri client Lync. Se questa impostazione è True, Siren verrà incluso come possibile codec per l'utilizzo tra il Mediation Server e altri client Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>EncryptionLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.EncryptionLevel</p></td>
<td><p>Livello di crittografia tra i dispositivi per comunicazioni unificate.</p>
<p>Valori validi:</p>
<p>SupportEncryption: viene utilizzato Secure Real-Time Transport Protocol (SRTP) se è possibile effettuare la negoziazione.</p>
<p>RequireEncryption: SRTP deve essere negoziato.</p>
<p>DoNotSupportEncryption: SRTP non deve essere utilizzato.</p>
<p>Per questo valore non viene fatta distinzione tra maiuscole e minuscole. Per informazioni dettagliate, vedere gli esempi in questo argomento.</p>
<p>Valore predefinito: RequireEncryption</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco delle impostazioni di configurazione multimediali che si desidera modificare. Questo identificatore specifica l'ambito a cui viene applicata la configurazione (globale, sito o servizio).</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>MediaSettings</p></td>
<td><p>Un'istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings. Per recuperare questo oggetto è possibile chiamare il cmdlet <strong>Get-CsMediaConfiguration</strong> con un'identità specifica. È quindi possibile assegnare nuovi valori alle proprietà dell'oggetto e poi salvare le modifiche passando l'oggetto al cmdlet <strong>Set-CsMediaConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxVideoRateAllowed</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.MaxVideoRateAllowed</p></td>
<td><p>La velocità massima di trasferimento dei segnali video agli endpoint client.</p>
<p>Valori validi: Hd720p15M, VGA600K, CIF250K</p>
<p>Hd720p15M - Alta definizione, con risoluzione 1280 x 720 e proporzioni 16:9.</p>
<p>VGA600K - VGA, con risoluzione 640 x 480, 25 fps e proporzioni 4:3.</p>
<p>CIF250K - Formato video CIF (Common Intermediate Format), 15 fps con risoluzione 352 x 288.</p>
<p>Questi valori non fanno distinzione tra maiuscole e minuscole e vengono convertiti nel formato maiuscolo/minuscolo corretto in fase di creazione della configurazione. Per informazioni dettagliate, vedere gli esempi in questo argomento.</p>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings. Consente di accettare l'input da pipeline di oggetti configurazione multimediale.

## Tipi restituiti

Il cmdlet **Set-CsMediaConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsMediaConfiguration](new-csmediaconfiguration.md)  
[Remove-CsMediaConfiguration](remove-csmediaconfiguration.md)  
[Get-CsMediaConfiguration](get-csmediaconfiguration.md)

