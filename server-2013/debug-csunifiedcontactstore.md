---
title: Debug-CsUnifiedContactStore
TOCTitle: Debug-CsUnifiedContactStore
ms:assetid: 8e92d262-604d-41b1-9530-947765025a79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994054(v=OCS.15)
ms:contentKeyID: 52062197
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsUnifiedContactStore

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che i contatti di un utente o di un gruppo di utenti siano memorizzati nell'archivio contatti unificato.

Questo cmdlet è stato introdotto negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.

## Sintassi

    Debug-CsUnifiedContactStore -Identity <UserIdParameter> [-ContactDataExportFileName <String>] <COMMON PARAMETERS>

    Debug-CsUnifiedContactStore -PoolFqdn <Fqdn> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 verifica lo stato dell'archivio contatti unificato per tutti gli utenti i cui account sono contenuti nel pool atl-cs-001.litwareinc.com.

    Debug-CsUnifiedContactStore -PoolFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'esempio 2 lo stato dell'archivio contatti unificato viene verificato per un singolo utente, ovvero l'utente con indirizzo SIP "kenmyer@litwareinc.com".

    Debug-CsUnifiedContactStore -Identity "kenmyer@litwareinc.com"

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli utenti di accedere al proprio elenco contatti da diverse applicazioni, tra cui Microsoft Lync 2013, Outlook 2013 e Outlook Web App. Questo accesso è possibile perché le informazioni dei contatti vengono archiviate in un'unica posizione, ovvero Microsoft Exchange Server 2013.

Il cmdlet **Debug-CsUnifiedContactStore** consente agli amministratori di verificare se un utente o un insieme di utenti specifico (ovvero tutti gli utenti i cui account sono contenuti in un pool specifico) dispongono dei propri elenchi contatti archiviati nell'archivio contatti unificato. Se si esegue il cmdlet **Debug-CsUnifiedContactStore** per un account utente specifico, verrà indicato se i contatti dell'utente sono stati spostati nell'archivio contatti unificato, il numero di tentativi di spostamento dei contatti e l'ultimo tentativo di migrazione dell'elenco contatti da parte di Lync Server. Se viene chiamato per un pool, il cmdlet **Debug-CsUnifiedContactStore** restituisce dati simili ai seguenti:

FrontEnd: atl-cs-001.litwareinc.com  
UcsDisabledCount: 44  
UcsAllowedCount: 129  
UcsMigratingCount: 11  
UcsMigratedCount:  
FailedUserData:

Il cmdlet **Debug-CsUnifiedContactStore** e il parametro ContactDataExportFileName possono essere utilizzati inoltre per esportare le informazioni sui contatti di un utente in un file XML.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsUnifiedContactStore"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Debug-CsUnifiedContactStore** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indirizzo SIP di un singolo utente di cui viene verificato lo stato dell'archivio contatti unificato (è possibile specificare un solo utente per comando), ad esempio:</p>
<p>-Identity &quot;kenmyer@litwareinc.com&quot;</p>
<p>Quando si specifica l'indirizzo SIP, il prefisso sip: è facoltativo. Funzionerà anche la sintassi seguente:</p>
<p>-Identity &quot;sip:kenmyer@litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di registrazione di cui viene verificato lo stato dell'archivio contatti unificato. Verranno controllati tutti gli account utente contenuti nel pool specificato, ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ContactDataExportFileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file XML in cui vengono inclusi i contatti dell'utente specifico quando vengono esportati dall'archivio contatti unificato, ad esempio:</p>
<p>-ContactDataExportFileName &quot;C:\Exports\KenMyer.xml&quot;</p>
<p>Si noti che è necessario includere il parametro Identity e l'indirizzo SIP dell'utente di cui si desidera esportare i contatti. Se l'utente non è stato abilitato per l'archivio contatti unificato, il comando verrà terminato e non verrà esportato alcun contatto.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Debug-CsUnifiedContactStore** non accetta dati inviati tramite pipeline.

## Tipi restituiti

Il cmdlet **Debug-CsUnifiedContactStore** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Presence.Cmdlets.GetUcsFrontEndData.

## Vedere anche

#### Ulteriori risorse

[Test-CsUnifiedContactStore](test-csunifiedcontactstore.md)

