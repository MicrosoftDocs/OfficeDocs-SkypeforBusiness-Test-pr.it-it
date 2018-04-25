---
title: Publish-CsLisConfiguration
TOCTitle: Publish-CsLisConfiguration
ms:assetid: 54f9d653-075d-4533-b508-231f53b54db4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398364(v=OCS.15)
ms:contentKeyID: 49300554
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Publish-CsLisConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Pubblica la configurazione del server Informazioni percorso dall'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Publish-CsLisConfiguration [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando consente di salvare la configurazione LIS in archivio di gestione centrale.

    Publish-CsLisConfiguration

## Descrizione dettagliata

Per implementare la funzionalità Enhanced 9-1-1 (E9-1-1) in Lync Server, è necessario creare una mappa delle posizioni (wiremap). Questa mappa include l'associazione degli indirizzi fisici a porte, subnet, commutatori e punti di accesso wireless, in modo tale che le chiamate effettuate tramite una connessione di VoIP aziendale raggiungano il più vicino operatore del servizio di emergenza fornendogli la corretta posizione del chiamante. Questa configurazione della mappa, creata chiamando cmdlet quali **Set-CsLisPort** e **Set-CsLisSubnet**, viene archiviata in un database centrale delle posizioni. Questo cmdlet salva tutte le eventuali modifiche apportate al database centrale delle posizioni nell'archivio di gestione centrale e consente di replicare le informazioni nei server Informazioni percorso in modo che le posizioni vengano visualizzate nei client. La configurazione può essere rimossa dall'archivio di gestione centrale chiamando il cmdlet **Unpublish-CsLisConfiguration**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Publish-CsLisConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Publish-CsLisConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Nessuno.

## Tipi restituiti

Questo cmdlet non restituisce un valore.

## Vedere anche

#### Ulteriori risorse

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

