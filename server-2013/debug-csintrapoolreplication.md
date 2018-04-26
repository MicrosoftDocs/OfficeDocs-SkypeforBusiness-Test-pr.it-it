---
title: Debug-CsIntraPoolReplication
TOCTitle: Debug-CsIntraPoolReplication
ms:assetid: 9882f703-07c7-46fe-b525-7efd1326503c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205103(v=OCS.15)
ms:contentKeyID: 49301406
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsIntraPoolReplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la replica sincrona di un pool confrontando i dati archiviati per un determinato utente in un Front End Server primario con i dati relativi a quello stesso utente archiviati nei Front End Server di replica. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Debug-CsIntraPoolReplication -UserUri <UserIdParameter> <COMMON PARAMETERS>

    Debug-CsIntraPoolReplication -ConferenceDirectory <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica la replica in un Front End Server utilizzando l'utente con l'indirizzo SIP "sip:kenmyer@litwareinc.com".

    Debug-CsIntraPoolReplication -UserUri "sip:kenmyer@litwareinc.com"

## Esempio 2

Nell'esempio 2 la replica viene verificata utilizzando tutti gli utenti che dispongono di account utente nell'unità organizzativa Redmond. A tale scopo, nel comando viene innanzitutto chiamato Get-CsUser insieme al parametro OU. Il valore di parametro "OU=Redmond,dc=litwareinc,dc=com" limita i dati restituiti agli account utente trovati nell'unità organizzativa Redmond. Tali account vengono quindi inviati tramite pipe al cmdlet ForEach-Object, che a sua volta utilizza il cmdlet Debug-CsIntraPoolReplication per verificare lo stato di replica di ogni account incluso nell'unità organizzativa.

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | ForEach-Object {Debug-CsIntraPoolReplication $_.Identity}

## Esempio 3

Il comando riportato nell'esempio 3 verifica lo stato di replica utilizzando una coppia di indirizzi SIP di utenti. A tale scopo, i due indirizzi SIP (racchiusi tra virgolette e separati da una virgola) vengono inviati tramite pipe al cmdlet ForEach-Object, che quindi esegue il cmdlet Debug-CsIntraPoolReplication su ogni indirizzo SIP.

    "sip:kenmyer@litwareinc.com","sip:pilar@litwareinc.com" | ForEach-Object {Debug-CsIntraPoolReplication -UserUri $_}

## Esempio 4

Nell'esempio 4 la replica viene verificata per la directory conferenze con l'ID 13.

    Debug-CsIntraPoolReplication -ConferenceDirectory 13

## Esempio 5

Nell'esempio 5 viene illustrato come verificare la replica per tutti gli utenti che si trovano in un determinato pool di registrazione. A tale scopo, nel comando viene innanzitutto chiamato Get-CsUser insieme al parametro Filter. Il valore di filtro {RegistrarPool –eq "atl-cs-001.litwareinc.com"} limita i dati restituiti agli account utente che si trovano nel pool di registrazione atl-cs-001.litwareinc.com. Tali account vengono quindi inviati tramite pipe al cmdlet Debug-CsIntraPoolReplication, che verifica la replica per ogni utente incluso nel pool.

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Debug-CsIntraPoolReplication UserUri {$_.Identity}

## Descrizione dettagliata

Il cmdlet Debug-CsIntraPoolReplication consente agli amministratori di verificare che sia attiva la replica tra un Front End Server primario e i relativi Front End Server di replica. Per ottenere questo risultato, è possibile procedere in due modi: 1) verificare che i dati di un utente specificato siano identici nel Front End Server e nei relativi server di replica oppure 2) verificare che i dati di una directory conferenze siano identici nel Front End Server e in tutti i relativi server di replica. Per eseguire queste due operazioni, Debug-CsIntraPoolReplication si connette innanzitutto al Front End Server primario e crea un file XML contenente dati di utenti o di directory conferenze. Il cmdlet quindi si connette ai server di replica, crea file XML simili e infine verifica che il contenuto selezionato nei file XML sia identico.

Il cmdlet Debug-CsIntraPoolReplication verifica la replica per un pool selezionando uno o più account utente (o una directory conferenze) e richiedendo tramite query a un Front End Server primario e a tutti i relativi Front End Server di replica i dati su tali account o directory conferenze. Le informazioni recuperate dal Front End Server primario e dai server di replica vengono quindi messe a confronto. Se i dati corrispondono, la replica all'interno del pool sta funzionando come previsto.

Questo cmdlet può essere chiamato solo utilizzando utenti o directory conferenze che si trovano in Lync Server 2013.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsIntraPoolReplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Debug-CsIntraPoolReplication non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>ConferenceDirectory</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Consente di verificare la replica di una directory conferenze. Le directory conferenze devono essere specificate mediante la relativa identità. Le identità delle directory conferenze possono essere recuperate eseguendo questo comando:</p>
<p>Get-CsConferenceDirectory | Select-Object Identity, ServiceId</p>
<p>Non è possibile utilizzare il parametro ConferenceDirectory e il parametro UserUri nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>UserUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indirizzo SIP dell'account utente utilizzato nella verifica della replica all'interno del pool. Ad esempio:</p>
<p>-UserUri &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Non è possibile utilizzare il parametro ConferenceDirectory e il parametro UserUri nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa o oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Debug-CsIntraPoolReplication accetta un valore stringa inviato tramite pipeline che rappresenta l'indirizzo SIP o il nome visualizzato di Active Directory di un account utente abilitato per Lync Server. Il cmdlet accetta inoltre le istanze inviate tramite pipeline dell'oggetto utente di Active Directory per un utente abilitato per Lync Server.

## Tipi restituiti

Debug-CsIntraPoolReplication restituisce istanze dell'oggetto Microsoft.Rtc.Management.UserPinservice.Data.syncReplicationDetails.

## Vedere anche

#### Ulteriori risorse

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)  
[Test-CsReplica](test-csreplica.md)

