---
title: New-CsFileTransferFilterConfiguration
TOCTitle: New-CsFileTransferFilterConfiguration
ms:assetid: 3d1050fb-5df9-4186-94b9-8ef8a9103958
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425897(v=OCS.15)
ms:contentKeyID: 49300281
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsFileTransferFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova configurazione di filtro per il trasferimento di file. Le configurazioni di filtro per il trasferimento file sono utilizzate per impedire a un utente di trasferire determinati tipi di file (ad esempio i file con estensione vbs o ps1) utilizzando un client Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsFileTransferFilterConfiguration -Identity <XdsIdentity> [-Action <BlockAll | Block>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Extensions <PSListModifier>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **New-CsFileTransferFilterConfiguration** per creare una nuova configurazione di filtro per il trasferimento di file di messaggistica istantanea con identità site:Redmond. Dal momento che non sono stati specificati altri parametri, la configurazione verrà creata utilizzando i valori predefiniti.

    New-CsFileTransferFilterConfiguration -Identity site:Redmond

## ESEMPIO 2

In questo comando viene utilizzato il cmdlet **New-CsFileTransferFilterConfiguration** per creare una nuova configurazione di filtro per il trasferimento di file con identità site:Redmond. Dal momento che è stato specificato il parametro Extensions, la nuova configurazione includerà tutti i valori predefiniti e in più l'estensione di file .ps1. Questa nuova estensione viene aggiunta utilizzando il parametro Extensions e il modificatore di elenco Add seguito dall'estensione da aggiungere. Si noti che è necessario includere il punto come parte dell'estensione di file. Per aggiungere più estensioni, è sufficiente separarle con le virgole: @{Add=".ps1",".ps2",".ps3"}

    New-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Add=".ps1"}

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il cmdlet **New-CsFileTransferFilterConfiguration** per creare una nuova configurazione di filtro per il trasferimento di file con identità site:Redmond. Questo esempio è simile all'esempio 2, ma in questo caso come modificatore di elenco è stato utilizzato Replace anziché Add. Ciò significa che il gruppo completo di estensioni verrà sostituito dalle due estensioni specificate: .vbs e .ps1. In questo caso, i soli file bloccati nel sito Redmond saranno quelli con estensione .vbs e .ps1.

    New-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Replace=".vbs",".ps1"}

## ESEMPIO 4

Nell'esempio 4 viene illustrato l'utilizzo del parametro InMemory per creare una configurazione di filtro per il trasferimento di file che inizialmente risiede solo in memoria. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsFileTransferFilterConfiguration** e il parametro InMemory per creare una nuova configurazione di filtro per il trasferimento di file con identità site:Redmond. A questo punto, le nuove impostazioni esistono solo in memoria e agli utenti presso il sito Redmond vengono ancora applicate le impostazioni globali di filtro per il trasferimento di file.

Nel secondo comando il valore della proprietà Action per questa istanza in memoria viene impostato su BlockAll. Il terzo comando dell'esempio infine utilizza il cmdlet **Set-CsFileTransferFilterConfiguration** per creare la nuova raccolta di impostazioni e applicarle al sito Redmond.

Si noti che è possibile eseguire la stessa operazione in un unico passaggio utilizzando il seguente comando:

    New-CsFileTransferFilterConfiguration -Identity site:Redmond -Action "BlockAll"
    $x = New-CsFileTransferFilterConfiguration -Identity site:Redmond -InMemory 
    $x.Action = "BlockAll"
    Set-CsFileTransferFilterConfiguration -Instance $x

## Descrizione dettagliata

Quando si invia un messaggio istantaneo, gli utenti possono allegare e inviare file agli altri partecipanti alla conversazione. È possibile configurare Lync Server in modo tale che i file con determinate estensioni, in genere le estensioni che caratterizzano tipi di file potenzialmente dannosi, non possano essere inviati tramite un client Lync Server.

Quando si installa Lync Server, viene creata automaticamente nell'ambito globale una configurazione del filtro di trasferimento file. Per impostazione predefinita, questa configurazione globale si applica a tutti gli utenti dell'organizzazione. È inoltre possibile utilizzare il cmdlet **New-CsFileTransferFilterConfiguration** per creare configurazioni di filtro per il trasferimento di file personalizzate per singoli siti. Se per un determinato sito è già disponibile una configurazione, le relative impostazioni di trasferimento file verranno applicate a tutti gli utenti del sito. Se per un sito non è disponibile alcuna raccolta di questo tipo, verranno applicate le impostazioni globali.

Si noti che non è possibile creare una nuova configurazione del filtro di trasferimento file nell'ambito globale; tuttavia, è possibile utilizzare il cmdlet **Set-CsFileTransferFilterConfiguration** per modificare le impostazioni globali. Similmente, non è possibile creare una nuova configurazione per un sito che dispone già di una configurazione; se si tenta di eseguire questa operazione, il comando avrà esito negativo.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsFileTransferFilterConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdministrator. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsFileTransferFilterConfiguration"}

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
<td><p>Identificatore univoco da assegnare alla configurazione del filtro di trasferimento file. L'identità della nuova configurazione è costituita dal prefisso &quot;site:&quot; seguito dal nome del sito. Ad esempio, per creare una nuova configurazione per il sito Redmond, utilizzare la seguente sintassi: -Identity site:Redmond.</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileFilterAction</p></td>
<td><p>Determina l'azione da intraprendere quando il filtro di trasferimento file è abilitato. Se è impostato su BlockAll, il trasferimento dei file sarà proibito, indipendentemente dall'estensione del file in questione. Se è impostato su Block (valore predefinito), il trasferimento dei file verrà consentito a meno che l'estensione del file in questione non sia presente nell'elenco di estensioni proibite specificate per la proprietà Extensions.</p>
<p>Per consentire il trasferimento di tutte le tipologie di file in modo che gli utenti possano scambiare qualsiasi tipo di file, indipendentemente dall'estensione, impostare la proprietà Enabled di questo criterio su False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Abilita o disabilita il filtro per il trasferimento dei file. Se questo parametro è impostato su True, i file con le estensioni specificate (o tutti i file, a seconda del valore specificato per la proprietà Action) non possono essere trasferiti utilizzando un client Lync Server. Se questo parametro è impostato su False, è possibile trasferire qualsiasi file.</p>
<p>Valore predefinito: True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Extensions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco delle estensioni di file che verranno bloccate. Se si tenta di utilizzare un client Lync Server per trasferire un file la cui estensione corrisponde a una di quelle presenti nell'elenco, il trasferimento verrà bloccato e il file non verrà trasferito. L'elenco viene ignorato se Action è impostato su BlockAll (sono bloccati tutti i trasferimenti di file) o se Enabled è impostato su False (non è bloccato alcun trasferimento di file).</p>
<p>Per impostazione predefinita, nella proprietà Extensions sono incluse le seguenti estensioni: .ade, .adp, .app, .asp, .bas, .bat, .cer, .chm, .cmd, .com, .cpl, .crt, .csh, .exe, .fxp, .grp, .hlp, .hta, .inf, .ins, .isp, .its, .js, .jse, .ksh, .lnk, .mad, .maf, .mag, .mam, .maq, .mar., mas., .mat, .mau, .mav, .maw, .mda, .mdb. .mde, .mdt, .mdw, .mdz, .msc, .msi, .msp, .mst, .ocx, .ops, .pcd, .pif, .pl, .pnp, .prf, .prg, .pst, .reg, .scf, .scr, .sct, .shb, .shs, .tmp, .url, .vb, .vbe, .vbs, .vsd, .vsmacros, .vss, .vst, .vsw, .ws, .wsc. .wsf, .wsh</p></td>
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

Il cmdlet **New-CsFileTransferFilterConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsFileTransferFilterConfiguration](remove-csfiletransferfilterconfiguration.md)  
[Set-CsFileTransferFilterConfiguration](set-csfiletransferfilterconfiguration.md)  
[Get-CsFileTransferFilterConfiguration](get-csfiletransferfilterconfiguration.md)

