---
title: New-CsClsRegion
TOCTitle: New-CsClsRegion
ms:assetid: 09396d6e-e7ec-43b8-9f5b-d9cac30348f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204658(v=OCS.15)
ms:contentKeyID: 49299612
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova area di configurazione della registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la registrazione degli eventi in più computer. Le aree di registrazione centralizzata devono essere utilizzate con Skype for Business online.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsClsRegion -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsClsRegion -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -OtherRegionAccess <String> -SecurityGroupSuffix <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Sites <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato in questo esempio crea una nuova area globale denominata Europe. La nuova area utilizza il suffisso di gruppo di sicurezza EMEA e consente l'accesso anche all'area global/US.

    New-CsClsRegion -Identity "global/Europe" -SecurityGroupSuffix "EMEA" -OtherRegionAccess "global/US"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con la versione Office 365 di Lync Server, le aree vengono utilizzate per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. Le aree vengono create utilizzando il cmdlet [New-CsClsRegion](new-csclsregion.md) e vengono quindi aggiunte a una raccolta di impostazioni di configurazione della registrazione centralizzata.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsRegion"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsClsRegion** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco della nuova area. Le identità di area sono costituite dall'ambito di configurazione della registrazione centralizzata in cui verrà creata l'area e da un nome di area univoco. Per creare ad esempio un'area globale denominata Redmond, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/Redmond&quot;</p>
<p>Se si utilizza il parametro Identity, non sarà possibile utilizzare il parametro Name o il parametro Parent nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco della nuova area, ad esempio:</p>
<p>-Name &quot;Redmond&quot;</p>
<p>Se si utilizza il parametro Name, sarà necessario utilizzare inoltre il parametro Parent. Non utilizzare tuttavia il parametro Identity nello stesso comando in cui sono presenti i parametri Name e Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>OtherRegionAccess</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di un'area aggiuntiva a cui possono accedere utenti autorizzati per l'area.</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito delle impostazioni di configurazione della registrazione centralizzata in cui verrà posizionata la nuova area. Per aggiungere ad esempio la nuova area alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Parent &quot;global&quot;</p>
<p>È possibile restituire le identità di tutti gli elementi &quot;padre&quot; della registrazione centralizzata utilizzando il comando seguente:</p>
<p>Get-CsCentralizedLoggingConfiguration | Select-Object Identity</p>
<p>Se si utilizza il parametro Name, sarà necessario utilizzare inoltre il parametro Parent. Non utilizzare tuttavia il parametro Identity nello stesso comando in cui sono presenti i parametri Name e Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>SecurityGroupSuffix</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Suffisso da aggiungere alla fine del nome di un gruppo di sicurezza autorizzato per l'area.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Sites</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Siti contenuti in questa area. Corrispondono ai valori dell'attributo SideId nel documento della topologia.</p></td>
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

Nessuno. Il cmdlet New-CsClsRegion non accetta input da pipeline.

## Tipi restituiti

Il cmdlet New-CsClsRegion crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsRegion](get-csclsregion.md)  
[Remove-CsClsRegion](remove-csclsregion.md)  
[Set-CsClsRegion](set-csclsregion.md)

