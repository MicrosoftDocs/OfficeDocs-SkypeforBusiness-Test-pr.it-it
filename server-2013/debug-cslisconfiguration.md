---
title: Debug-CsLisConfiguration
TOCTitle: Debug-CsLisConfiguration
ms:assetid: 8cc718d6-52ec-4ff3-a77e-8d6df1725fb0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398710(v=OCS.15)
ms:contentKeyID: 49301274
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsLisConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Visualizza la configurazione del servizio Informazioni percorso della funzionalità per chiamate di emergenza Enhanced 9-1-1 (E9-1-1) in formato XML. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Debug-CsLisConfiguration [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Eseguendo questo comando verrà visualizzata l'intera configurazione LIS nella finestra di Lync Server Management Shell in formato XML. Per impostazione predefinita, l'output del cmdlet **Debug-CsLisConfiguration** viene visualizzato su una riga, con puntini di sospensione (…) alla fine della riga a indicare che sono presenti più righe di dati. In questo esempio pertanto l'output viene inviato tramite pipe al cmdlet **Format-Table** specificando il parametro Wrap, per visualizzare l'output completo con ritorni a capo per adattarlo alla finestra di visualizzazione.

    Debug-CsLisConfiguration | Format-Table -Wrap

## Descrizione dettagliata

La configurazione LIS di una implementazione di VoIP aziendale con E9-1-1 è memorizzata in formato compresso. Questo cmdlet decomprime la configurazione e la visualizza in formato XML. Questo può rendere più veloce la diagnostica in una configurazione.

Questo cmdlet recupera le informazioni sulla posizione dall'archivio di gestione centrale. Quando vengono create, queste informazioni vengono archiviate nel database delle posizioni e non vengono spostate nell'archivio di gestione centrale fino a quando non vengono pubblicate con il cmdlet **Publish-CsLisConfiguration**. Se le informazioni sulla posizione non sono state pubblicate (o se la pubblicazione è stata annullata con il cmdlet **Unpublish-CsLisConfiguration**), il cmdlet **Debug-CsLisConfiguration** non restituirà alcun risultato.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Debug-CsLisConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsLisConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare un controller di dominio. Se non è specificato alcun controller di dominio, viene utilizzato il primo disponibile.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di recuperare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

