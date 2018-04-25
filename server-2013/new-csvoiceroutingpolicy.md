---
title: New-CsVoiceRoutingPolicy
TOCTitle: New-CsVoiceRoutingPolicy
ms:assetid: 9e5bd6f6-902f-4911-ab88-9abb581df7fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205135(v=OCS.15)
ms:contentKeyID: 49301500
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRoutingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio di routing vocale. I criteri di routing vocale gestiscono gli utilizzi PSTN per gli utenti della funzionalità vocale ibrida. Questa funzionalità consente agli utenti presenti in Skype for Business online di usufruire delle funzionalità di VoIP aziendale disponibili in un'installazione locale di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsVoiceRoutingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PstnUsages <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo criterio di routing vocale per utente con l'identità RedmondVoiceRoutingPolicy. A tale criterio viene assegnato un solo utilizzo PSTN, ovvero Long Distance.

    New-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -Name "RedmondVoiceRoutingPolicy" -PstnUsages "Long Distance"

## Esempio 2

L'esempio 2 è una variante del comando riportato nell'esempio 1. In questo caso, al nuovo criterio vengono invece assegnati tre utilizzi PSTN, ovvero Long Distance, Local e Internal. È possibile assegnare più utilizzi semplicemente separandoli con una virgola.

    New-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -Name "RedmondVoiceRoutingPolicy" -PstnUsages "Long Distance", "Local", "Internal"

## Descrizione dettagliata

I criteri di routing vocale vengono utilizzati in scenari "ibridi", ovvero scenari in cui alcuni utenti sono situati nella versione locale di Lync Server e altri nella versione Skype for Business online. L'assegnazione di un criterio di routing vocale agli utenti di Skype for Business online consente loro di ricevere ed effettuare chiamate sulla rete PSTN (Public Switched Telephone Network) utilizzando i trunk SIP locali.

Si noti che la sola assegnazione di un criterio di routing vocale agli utenti non comporta l'abilitazione per le chiamate PSTN tramite Skype for Business online. Tali utenti dovranno essere abilitati anche per VoIP aziendale e dovranno disporre di un criterio vocale e di un dial plan appropriati.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRoutingPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet New-CsVoiceRoutingPolicy non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco da assegnare al nuovo criterio di routing vocale. Poiché è possibile creare nuovi criteri solo nell'ambito del singolo utente, l'identità corrisponderà sempre al &quot;nome&quot; (Name) assegnato al criterio. Ad esempio:</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo esplicativo associato a un criterio di routing vocale. Ad esempio, il parametro Description potrebbe includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo per questo criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco degli utilizzi PSTN, ad esempio Local o Long Distance, che possono essere applicati al criterio di routing vocale. L'utilizzo PSTN deve essere già esistente. Gli utilizzi PSTN possono essere recuperati chiamando il cmdlet <strong>Get-CsPstnUsage</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsVoiceRoutingPolicy** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsVoiceRoutingPolicy** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

