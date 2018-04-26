---
title: Test-CsInterTrunkRouting
TOCTitle: Test-CsInterTrunkRouting
ms:assetid: 2248d29a-8a2a-42b1-ab6b-a6c1d74b0455
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204741(v=OCS.15)
ms:contentKeyID: 49299921
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsInterTrunkRouting

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la route e l'utilizzo PSTN utilizzati per il routing di una telefonata da un trunk SIP specificato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsInterTrunkRouting -TargetNumber <PhoneNumber> -TrunkConfiguration <TrunkConfiguration> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 restituiscono le route e gli utilizzi telefono corrispondenti che consentono agli utenti di chiamare il numero di telefono 1-206-555-1219 utilizzando le impostazioni di configurazione trunk del sito Redmond.

    $trunk = Get-CsTrunkConfiguration -Identity "site:Redmond"
    
    Test-CsInterTrunkRouting -TargetNumber "tel:+12065551219" -TrunkConfiguration $trunk

## Descrizione dettagliata

Il cmdlet Test-CsInterTrunkRouting verifica che sia possibile instradare le chiamate da un trunk SIP a un altro. A tale scopo, vengono forniti al cmdlet un numero di telefono e una configurazione trunk. Test-CsInterTrunkRouting segnalerà quindi le route e gli utilizzi PSTN corrispondenti per il numero specificato. Si noti che il routing delle chiamate tra trunk è possibile solo se i trunk dispongono di un formato numero corrispondente al numero di telefono specificato e condividono almeno un utilizzo PSTN.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsInterTrunkRouting"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Test-CsInterTrunkRouting non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>TargetNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>Numero di telefono PSTN da chiamare nel corso del test. Il numero di telefono di destinazione deve essere specificato utilizzando il formato E.164. In questo modo il numero sarà simile al seguente:</p>
<p>-TargetNumber &quot;tel:+12065551219&quot;</p>
<p>Il numero di telefono deve includere il prefisso &quot;tel:&quot; seguito da un segno più (+), dal codice paese/area geografica (1), dall'indicativo di località (206) e dal numero di telefono vero e proprio (5551219). Non utilizzare trattini, parentesi o altri caratteri quando si specifica il numero di telefono.</p></td>
</tr>
<tr class="even">
<td><p><em>TrunkConfiguration</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration</p></td>
<td><p>Riferimento oggetto alla configurazione trunk da testare. Per creare questo riferimento oggetto, utilizzare un comando simile al seguente:</p>
<p>$trunk = Get-CsTrunkConfiguration –Identity &quot;site:Redmond&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings</p></td>
<td><p>Riferimento oggetto che consente di specificare una raccolta di impostazioni di configurazione del routing vocale quando si chiama Test-CsInterTrunkRouting. Per creare questo riferimento oggetto, utilizzare un comando simile al seguente:</p>
<p>$route = Get-CsRoutingConfiguration –Identity &quot;global&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Test-CsInterTrunkRouting non accetta input da pipeline.

## Tipi restituiti

Test-CsInterTrunkRouting restituisce istanze dell'oggetto Microsoft.Rtc.Management.Voice.InterTrunkRoutingTestResult.

## Vedere anche

#### Ulteriori risorse

[Get-CsTrunk](get-cstrunk.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)

