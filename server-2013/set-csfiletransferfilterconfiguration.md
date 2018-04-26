---
title: Set-CsFileTransferFilterConfiguration
TOCTitle: Set-CsFileTransferFilterConfiguration
ms:assetid: 2697d3a0-d920-4a1d-9adc-7a8c754d8977
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425736(v=OCS.15)
ms:contentKeyID: 49299964
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsFileTransferFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta di impostazioni di configurazione del filtro di trasferimento file. Le impostazioni del filtro di trasferimento file sono utilizzate per impedire a un utente di trasferire determinati tipi di file (ad esempio i file con estensione vbs o ps1) utilizzando i client Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsFileTransferFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsFileTransferFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <BlockAll | Block>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Extensions <PSListModifier>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene disabilitato il filtro di trasferimento file per il sito Redmond (vale a dire la configurazione del filtro di trasferimento file con identità site:Redmond). Per eseguire questa operazione, nel comando è incluso il parametro Enabled impostato su $False.

    Set-CsFileTransferFilterConfiguration -Identity site:Redmond -Enabled $False

## ESEMPIO 2

I comandi riportati nell'esempio 2 aggiungono una nuova estensione di file (ps1, ovvero l'estensione degli script di Windows PowerShell) all'elenco di estensioni di file vietate nel sito Redmond. Per aggiungere la nuova estensione di file, il cmdlet **Set-CsFileTransferFilterConfiguration** utilizza il parametro Extensions e il modificatore di elenco Add. Il modificatore aggiunge l'estensione di file specificata (ps1) all'elenco di estensioni vietate. Per aggiungere più estensioni con un singolo comando, è sufficiente separare le estensioni di file con le virgole: @{Add=".ps1",".ps2",".ps3"}. È necessario includere il punto quando si specifica un'estensione di file.

    Set-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Add=".ps1"}

## ESEMPIO 3

Nell'esempio 3 l'estensione di file ps1 viene aggiunta all'elenco Extensions per tutte le configurazioni del filtro di trasferimento file attualmente in uso nell'organizzazione. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsFileTransferFilterConfiguration**, senza parametri aggiuntivi, per restituire una raccolta di tutte le configurazioni del filtro di trasferimento file attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsFileTransferFilterConfiguration**, che aggiunge l'estensione di file ps1 a ogni elemento della raccolta.

    Get-CsFileTransferFilterConfiguration | Set-CsFileTransferFilterConfiguration -Extensions @{Add=".ps1"}

## ESEMPIO 4

Nell'esempio 4 l'estensione del file ps1 viene rimossa dall'elenco di estensioni bloccate dalla configurazione del filtro di trasferimento file per il sito Redmond. Questo esempio è identico all'esempio 3, con la differenza che invece di chiamare il modificatore di elenco Add per aggiungere un'estensione all'elenco, viene chiamato il modificatore di elenco Remove per rimuovere un'estensione dall'elenco.

    Set-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Remove=".ps1"}

## ESEMPIO 5

Nell'esempio 5 viene eseguita la stessa operazione dell'esempio 4, vale a dire la rimozione dell'estensione ps1 dall'elenco di estensioni del filtro di trasferimento file per il sito Redmond. In questo caso, viene però recuperata innanzitutto la configurazione del filtro di trasferimento file per site:Redmond e l'output viene assegnato alla variabile $a, che ora contiene la configurazione per il sito Redmond. Viene quindi recuperata la proprietà Extensions di $a, vale a dire la proprietà Extensions di site:Redmond ($a.Extensions). Questa proprietà include l'elenco delle estensioni di file. Dopo la proprietà Extensions viene utilizzata una chiamata al metodo Remove ($a.Extensions.Remove), al quale viene passato il valore .ps1. In questo modo, tale estensione viene rimossa dall'elenco nella proprietà Extensions. Con questa operazione, l'estensione è stata tuttavia rimossa solo dalla configurazione archiviata in memoria nella variabile $a. Per apportare la modifica al database, è necessario chiamare il cmdlet **Set-CsFileTransferFilterConfiguration**, passando $a al parametro Instance.

    $a = Get-CsFileTransferFilterConfiguration -Identity site:Redmond
    $a.Extensions.Remove(".ps1")
    Set-CsFileTransferFilterConfiguration -Instance $a

## Descrizione dettagliata

Quando si inviano messaggi istantanei, gli utenti possono allegare e inviare file agli altri partecipanti alla conversazione. Lync Server può essere configurato in modo da impedire l'invio dai client di file con determinate estensioni, generalmente riferite a tipi di file che possono rivelarsi dannosi.

La capacità degli utenti di trasferire file con i client Lync Server è determinata dalle impostazioni di configurazione del filtro di trasferimento file applicate nell'ambito globale o (facoltativamente) del sito. Il cmdlet **Set-CsFileTransferFilterConfiguration** consente di modificare una configurazione del filtro di trasferimento file esistente. È possibile modificare l'elenco di estensioni che saranno bloccate sia aggiungendo o rimuovendo le estensioni sia creando un elenco del tutto nuovo. È inoltre possibile utilizzare questo cmdlet per stabilire se il filtro di trasferimento file è abilitato e a quale livello (blocco dei soli file con estensioni corrispondenti a quelle nell'elenco Extensions o blocco di tutti i file).

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsFileTransferFilterConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsFileTransferFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileFilterAction</p></td>
<td><p>Consente di stabilire l'azione da intraprendere se la configurazione per il filtro di trasferimento file è abilitata. Se l'impostazione è BlockAll vengono vietati tutti i trasferimenti di file, indipendentemente dall'estensione del file. Se l'impostazione è Block (valore predefinito), i trasferimenti di file sono ammessi, a meno che l'estensione del file non sia presente tra i tipi di file proibiti nella proprietà Extensions.</p>
<p>Per consentire il trasferimento di tutte le tipologie di file, in modo che gli utenti possano scambiare qualsiasi tipo di file, indipendentemente dall'estensione, impostare la proprietà Enabled per questo criterio su False.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di abilitare o disabilitare il filtro di trasferimento file. Se questo parametro è impostato su True, i file con le estensioni specificate (o tutti i file, a seconda del valore della proprietà Action) non potranno essere trasferiti dal client. Se questo parametro è impostato su False, potranno essere trasferiti tutti i file.</p>
<p>Valore predefinito: True.</p></td>
</tr>
<tr class="even">
<td><p><em>Extensions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco delle estensioni di file che verranno bloccate. Se si tenta di utilizzare un client Lync Server per trasferire un file la cui estensione corrisponde a una di quelle presenti nell'elenco, il trasferimento verrà bloccato e il file non verrà trasferito. L'elenco viene ignorato se Action è impostato su BlockAll (sono bloccati tutti i trasferimenti di file) o se Enabled è impostato su False (non è bloccato alcun trasferimento di file).</p>
<p>Per impostazione predefinita, nella proprietà Extensions sono incluse le seguenti estensioni di file: .ade, .adp, .app, .asp, .bas, .bat, .cer, .chm, .cmd, .com, .cpl, .crt, .csh, .exe, .fxp, .grp, .hlp, .hta, .inf, .ins, .isp, .its, .js, .jse, .ksh, .lnk, .mad, .maf, .mag, .mam, .maq, .mar., mas., .mat, .mau, .mav, .maw, .mda, .mdb, .mde, .mdt, .mdw, .mdz, .msc, .msi, .msp, .mst, .ocx, .ops, .pcd, .pif, .pl, .pnp, .prf, .prg, .pst, .reg, .scf, .scr, .sct, .shb, .shs, .tmp, .url, .vb, .vbe, .vbs, .vsd, .vsmacros, .vss, .vst, .vsw, .ws, .wsc, .wsf, .wsh.</p></td>
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
<td><p>Identificatore univoco della configurazione di trasferimento file da modificare. Questo valore può essere global o site:&lt;nome sito&gt;, dove &lt;nome sito&gt; corrisponde al nome del sito a cui applicare le impostazioni, ad esempio site:Redmond.</p>
<p>Se questo parametro non viene specificato, per impostazione predefinita il cmdlet <strong>Set-CsFileTransferFilterConfiguration</strong> aggiornerà le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>FileTransferFilterConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Questo oggetto deve essere di tipo FileTransferFilterConfiguration e può essere recuperato chiamando il cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration. Consente di accettare l'input da pipeline di oggetti configurazione del filtro di trasferimento file.

## Tipi restituiti

Questo cmdlet non restituisce un valore o un oggetto. In realtà, il cmdlet configura istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsFileTransferFilterConfiguration](new-csfiletransferfilterconfiguration.md)  
[Remove-CsFileTransferFilterConfiguration](remove-csfiletransferfilterconfiguration.md)  
[Get-CsFileTransferFilterConfiguration](get-csfiletransferfilterconfiguration.md)

