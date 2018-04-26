---
title: Set-CsUICulture
TOCTitle: Set-CsUICulture
ms:assetid: 53fbc126-1df9-4ea0-8055-4e9530ab89d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398354(v=OCS.15)
ms:contentKeyID: 49300593
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUICulture

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare le impostazioni cultura (ovvero le impostazioni internazionali e della lingua) utilizzate da Lync Server Management Shell. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUICulture -Culture <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di impostare le impostazioni cultura per Lync Server Management Shell su Inglese USA. Per ottenere questo risultato, impostare il codice della lingua en-US.

    Set-CsUICulture -Culture "en-US"

## ESEMPIO 2

Nell'esempio 2 vengono impostate le impostazioni cultura di Lync Server Management Shell sulle impostazioni cultura predefinite. Le impostazioni cultura predefinite sono quelle selezionate per l'installazione iniziale di Lync Server.

    Set-CsUICulture -Culture "default"

## Descrizione dettagliata

Sebbene Lync Server sia disponibile in diverse lingue, questo software non può essere definito un'applicazione MUI (Multilingual User Interface, interfaccia utente multilingue) vera e propria. Tra l'altro, questo significa che l'interfaccia utente di Lync Server Management Shell non cambia la lingua ogni volta che si cambia la lingua del sistema operativo. Si supponga ad esempio di aver installato la versione in inglese americano di Lync Server e che anche il sistema operativo Windows sia nella stessa lingua. Se nel sistema operativo si modificano le impostazioni cultura, ovvero le impostazioni internazionali e della lingua, applicando il danese, la modifica non verrà estesa automaticamente a Lync Server Management Shell. L'interfaccia utente di Lync Server Management Shell, inclusi i messaggi di errore e il testo della Guida, continuerà a essere visualizzata in inglese americano. Per modificare le impostazioni cultura di Lync Server Management Shell, è necessario eseguire il cmdlet **Set-CsUICulture**.

Quando si utilizza il cmdlet **Set-CsUICulture**, è necessario tenere presente due aspetti. Il cmdlet **Set-CsUICulture** innanzitutto può essere utilizzato esclusivamente per modificare le impostazioni di Lync Server Management Shell nel computer locale, in quanto non è in grado di modificare un'istanza remota di Lync Server Management Shell. Ciò è dovuto al fatto che tutti gli utenti di un computer condividono la stessa istanza di Lync Server Management Shell: se si consentisse a un utente remoto di modificare le impostazioni cultura, questa modifica avrebbe immediatamente effetto anche su tutti gli altri utenti di Lync Server Management Shell, incluso l'utente locale.

In secondo luogo, è possibile impostare solo l'inglese USA ("en-US") oppure la lingua utilizzata per l'installazione iniziale di Lync Server ("default"). Ad esempio, se in origine è stata installata la versione italiana di Lync Server, le impostazioni cultura dell'interfaccia utente potranno essere solo in inglese o italiano.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsUICulture** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p><em>Culture</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare le impostazioni cultura per Lync Server Management Shell. Impostare le impostazioni cultura su &quot;en-US&quot; per l'inglese (Stati Uniti) oppure su &quot;default&quot; per utilizzare la lingua scelta al momento dell'installazione iniziale di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Nessuno. Il cmdlet **Set-CsUICulture** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsUICulture** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze esistenti della classe System.Globalization.CultureInfo.

## Vedere anche

#### Ulteriori risorse

[Get-CsUICulture](get-csuiculture.md)

