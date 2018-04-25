---
title: Get-CsRoutingConfiguration
TOCTitle: Get-CsRoutingConfiguration
ms:assetid: 37a1cbc9-b8b2-423c-8ebb-7947fdcad24e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425851(v=OCS.15)
ms:contentKeyID: 49300181
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera l'oggetto configurazione di routing, che include un elenco di tutte le route vocali definite in una distribuzione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsRoutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con questo esempio viene recuperata la configurazione di routing. Per recuperare le singole route vocali, utilizzare il cmdlet **Get-CsVoiceRoute**.

    Get-CsRoutingConfiguration

## Descrizione dettagliata

Le route vocali includono istruzioni che indicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale a numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Questo cmdlet viene utilizzato per recuperare l'istanza globale in cui è contenuto un elenco di tutte le route vocali definite nella distribuzione di Lync Server. Per recuperare le singole route vocali o per recuperarle come oggetti singoli anziché come elenco, utilizzare il cmdlet **Get-CsVoiceRoute**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsRoutingConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRoutingConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Può esistere una sola istanza di questo oggetto, quindi questo parametro non ha alcuno scopo.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'ambito della configurazione di routing da recuperare. L'unico valore possibile è Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la configurazione di routing dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsRoutingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Writable.Policy.Voice.PSTNRoutingSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

