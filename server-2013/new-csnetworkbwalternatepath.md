---
title: New-CsNetworkBWAlternatePath
TOCTitle: New-CsNetworkBWAlternatePath
ms:assetid: 9017378e-4583-42bc-9572-aa8e9571cfe3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398732(v=OCS.15)
ms:contentKeyID: 49301309
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWAlternatePath

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea nuove impostazioni che definiscono se i dati multimediali possono essere instradati a percorsi alternativi tramite Internet per le connessioni con larghezza di banda vincolata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkBWAlternatePath -AlternatePath <$true | $false> -BWPolicyModality <Audio | Video>

## Esempi

## ESEMPIO 1

In questo esempio viene creato un nuovo percorso alternativo per la larghezza di banda della rete e le impostazioni vengono assegnate a un'area appena creata. Nella prima riga dell'esempio viene chiamato il cmdlet **New-CsNetworkBWAlternatePath** per creare un nuovo percorso alternativo. Un percorso alternativo dispone solo di due proprietà: BWPolicyModality che deve essere impostata su audio o video (audio in questo esempio) e AlternatePath che deve essere impostata su True o False (True in questo esempio). L'output del cmdlet, un riferimento all'oggetto percorso alternativo appena creato, viene assegnato alla variabile $a.

Nella riga 2 dell'esempio il percorso alternativo appena creato viene utilizzato per la creazione di una nuova area di rete. A tale scopo, viene chiamato il cmdlet **New-CsNetworkRegion** con identità (Identity) NorthAmerica. Viene assegnato un valore al parametro obbligatorio CentralSite (nell'esempio il nome del sito centrale per quest'area è Redmond-NA-MCS), quindi viene specificato il parametro BWAlternatePaths, a cui viene passata la variabile ($a) contenente l'oggetto percorso alternativo appena creato.

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $true
    New-CsNetworkRegion -Identity NorthAmerica -CentralSite Redmond-NA-MLS -BWAlternatePaths $a

## Descrizione dettagliata

In una configurazione di Controllo di ammissione di chiamata in Lync Server sono disponibili due modalità: audio e video. È possibile impostare limitazioni della larghezza di banda per ognuna di queste modalità. Se le limitazioni relative alla larghezza di banda impediscono il completamento di una chiamata, è possibile instradare tale chiamata a un percorso alternativo tramite Internet, consentendo l'esecuzione della chiamata. Questo cmdlet consente di creare le impostazioni che definiscono se una chiamata può essere instradata a un percorso alternativo tramite Internet in base alla modalità. All'interno della configurazione di Controllo di ammissione di chiamata queste impostazioni sono valide per area.

Questo cmdlet non salva immediatamente le impostazioni appena create. Al contrario, crea le impostazioni in memoria. Affinché tali impostazioni vengano applicate a un'area della rete, è necessario assegnare l'output del cmdlet a una variabile e quindi utilizzare la variabile come valore per il parametro BWAlternatePaths del cmdlet **New-CsNetworkRegion** o **Set-CsNetworkRegion**. Si noti che è possibile applicare queste impostazioni in modo diretto tramite l'utilizzo dei parametri AudioAlternatePath e VideoAlternatePath relativi ai cmdlet **New-CsNetworkRegion** e **Set-CsNetworkRegion**, senza dover prima chiamare il cmdlet **New-CsNetworkBWAlternatePath** per creare un nuovo oggetto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsNetworkBWAlternatePath** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWAlternatePath"}

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
<td><p><em>AlternatePath</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Boolean</p></td>
<td><p>Impostare il parametro su True per consentire alle chiamate effettuate dal supporto multimediale della modalità specificata nel parametro BWPolicyModality (audio o video) di essere instradate a un percorso alternativo se nel percorso principale non è disponibile una larghezza di banda adeguata.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>BWPolicyModality</p></td>
<td><p>La modalità a cui viene applicata l'impostazione del percorso alternativo.</p>
<p>Valori validi: audio, video</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

