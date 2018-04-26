---
title: New-CsClsSecurityGroup
TOCTitle: New-CsClsSecurityGroup
ms:assetid: e42f2d5f-7720-4b69-8563-48172120d8d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205359(v=OCS.15)
ms:contentKeyID: 49302285
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsSecurityGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo gruppo di sicurezza di configurazione della registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la registrazione degli eventi in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsClsSecurityGroup -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsClsSecurityGroup -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -AccessLevel <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo gruppo di sicurezza di registrazione centralizzata con l'identità global/HelpDesk. In questo esempio, la proprietà AccessLevel è impostata su Tier3.

    New-CsClsSecurityGroup -Identity "global/HelpDesk" -AccessLevel "Tier3"

## Descrizione dettagliata

Il servizio di registrazione centralizzata (che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010) consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. Grazie alla registrazione centralizzata, gli amministratori possono arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un singolo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica su tutti i server Rubrica. Ciò rappresenta una differenza rispetto agli strumenti OCSLogger e OCSTracer che devono essere gestiti, e persino arrestati e avviati, singolarmente in ogni server. Il servizio di registrazione centralizzata consente inoltre agli amministratori di effettuare ricerche nei log di traccia tramite il comando, utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con Skype for Business online, i gruppi di sicurezza vengono utilizzati per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. I gruppi di sicurezza vengono creati utilizzando il cmdlet New-CsClsSecurityGroup e vengono quindi aggiunti a una raccolta di impostazioni di configurazione della registrazione centralizzata.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsSecurityGroup"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsClsSecurityGroup** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>AccessLevel</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Valore di stringa che specifica il livello di accesso assegnato al gruppo. I livelli di accesso sono valori di stringa arbitrari assegnati dagli amministratori e utilizzati per suddividere in categorie i gruppi di sicurezza. Ad esempio:</p>
<p>-AccessLevel &quot;Tier3&quot;</p>
<p>Più gruppi possono condividere lo stesso livello di accesso. Attualmente i soli valori ad avere un significato sono &quot;Tier3&quot;, &quot;Tier2&quot;, &quot;Product&quot;, &quot;Ops&quot; e &quot;Pii&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il nuovo gruppo di sicurezza. Le identità del gruppo di sicurezza sono costituite dall'ambito di configurazione della registrazione centralizzata in cui il gruppo verrà creato più un nome univoco del gruppo di sicurezza. Ad esempio, per creare un gruppo di sicurezza globale denominato HelpDesk, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/HelpDesk&quot;</p>
<p>Se si utilizza il parametro Identity, non è possibile utilizzare il parametro Name o il parametro Parent nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco per il nuovo gruppo di sicurezza. Ad esempio:</p>
<p>-Name &quot;HelpDesk&quot;</p>
<p>Se si utilizza il parametro Name, è necessario utilizzare anche il parametro Parent. Tuttavia, non si deve utilizzare il parametro Identity nello stesso comando dei parametri Name e Parent.</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito delle impostazioni di configurazione della registrazione centralizzata in cui verrà posto il nuovo gruppo di sicurezza. Ad esempio, per aggiungere il nuovo gruppo di sicurezza alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Parent &quot;global&quot;</p>
<p>È possibile restituire identità per tutti gli elementi padre utilizzando il comando seguente:</p>
<p>Get-CsCentralizedLoggingConfiguration | Select-Object Identity</p>
<p>Se si utilizza il parametro Name, è necessario utilizzare anche il parametro Parent. Tuttavia, non si deve utilizzare il parametro Identity nello stesso comando dei parametri Name e Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Nessuno. Il cmdlet **New-CsClsSecurityGroup** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsClsSecurityGroup** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsSecurityGroup](get-csclssecuritygroup.md)  
[Remove-CsClsSecurityGroup](remove-csclssecuritygroup.md)  
[Set-CsClsSecurityGroup](set-csclssecuritygroup.md)

