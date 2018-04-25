---
title: Get-CsTrunkConfiguration
TOCTitle: Get-CsTrunkConfiguration
ms:assetid: 15951113-5f96-4f44-8cad-9ff97fb5dfd6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398224(v=OCS.15)
ms:contentKeyID: 49299779
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrunkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più configurazioni trunk, che descrivono le impostazioni di un'entità peer di trunking, ad esempio un gateway PSTN (Public Switched Telephone Network), un sistema IP-PBX (Private Branch Exchange) o un servizio SBC (Session Border Controller) nel provider di servizi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsTrunkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate tutte le configurazioni trunk della distribuzione di Lync Server.

    Get-CsTrunkConfiguration

## ESEMPIO 2

In questo esempio viene recuperata la configurazione trunk con identità site:Redmond. Poiché le identità sono univoche, questo comando restituirà al massimo un oggetto.

    Get-CsTrunkConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono recuperate tutte le configurazioni trunk definite a livello di sito. Il cmdlet **Get-CsTrunkConfiguration** utilizza il parametro Filter per recuperare tutte le configurazioni trunk con valore Identity che inizia con site:, ovvero tutte le configurazioni trunk definite a livello di sito.

    Get-CsTrunkConfiguration -Filter site:*

## Descrizione dettagliata

Utilizzare questo cmdlet per recuperare una o più configurazioni di trunking applicabili a entità gateway PSTN. Ogni configurazione contiene impostazioni specifiche di un'entità trunking peer, ad esempio un gateway PSTN, un sistema IP-PBX o un servizio SBC nel provider di servizi. Tali impostazioni consentono di configurare diversi aspetti, ad esempio se abilitare o meno il bypass degli elementi multimediali in questo trunk, se inviare o meno i pacchetti RTCP (Real-Time Control Protocol) in determinate condizioni e se richiedere o meno la crittografia SRTP (Secure Real-Time Protocol).

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsTrunkConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrunkConfiguration"}

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
<td><p>Questo parametro accetta una stringa di caratteri jolly e restituisce tutti i trunk con identità corrispondenti a tale stringa. Ad esempio, con un valore di filtro site:*, vengono restituiti tutti i trunk definiti a livello di sito.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della configurazione del trunk che si desidera recuperare. Le configurazioni trunk possono essere definite nell'ambito globale, del sito oppure del servizio nel caso di un servizio gateway PSTN, ad esempio site:Redmond per il sito o PstnGateway:Redmond.litwareinc.com per il servizio.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la configurazione trunk dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet restituisce un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)

