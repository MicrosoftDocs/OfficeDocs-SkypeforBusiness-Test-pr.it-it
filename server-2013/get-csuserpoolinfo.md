---
title: Get-CsUserPoolInfo
TOCTitle: Get-CsUserPoolInfo
ms:assetid: 7be81a85-c536-4d5c-b866-af7380e45c0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398615(v=OCS.15)
ms:contentKeyID: 49301093
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserPoolInfo

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni relative al pool di registrazione, al pool di registrazione di backup e al pool di servizi utente cui è stato assegnato un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUserPoolInfo -Identity <UserIdParameter> [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Questo comando restituisce le informazioni sui pool per un singolo utente, ovvero l'utente con l'indirizzo SIP sip:kenmyer@litwareinc.com.

    Get-CsUserPoolInfo "sip:kenmyer@litwareinc.com"

## ESEMPIO 2

Nell'esempio 2 vengono restituite le informazioni sui pool per tutti gli utenti abilitati per Lync Server. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** senza alcun parametro per restituire una raccolta di tutti gli utenti abilitati per Lync Server. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsUserPoolInfo**, che visualizza le informazioni sui pool per ogni utente della raccolta.

    Get-CsUser | Get-CsUserPoolInfo

## ESEMPIO 3

Il comando riportato nell'Esempio 3 è una variazione del comando utilizzato nell'Esempio 2 nel quale venivano restituite informazioni relative a tutti gli utenti abilitati per Lync Server. Tuttavia, è possibile che utenti siano stati abilitati per Lync Server ma non siano stati assegnati ad un pool di registrazione. Il comando riportato nell'Esempio 2 visualizza un messaggio di errore per ciascun utente che risponde a quei criteri, quei messaggi di errore vengono soppressi nell'Esempio 3.

Per eliminare i messaggi di errore, nell'esempio 3 viene utilizzato ancora il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti abilitati per Lync Server. Questa volta però la raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli utenti in cui la proprietà RegistrarPool non è uguale a un valore Null, ovvero gli utenti a cui è stato assegnato un pool di registrazione. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Get-CsUserPoolInfo**, che visualizza le informazioni sui pool per ogni utente della raccolta.

    Get-CsUser | Where-Object {$_.RegistrarPool -ne $Null} | Get-CsUserPoolInfo

## ESEMPIO 4

Nell'esempio 4 vengono visualizzate le informazioni sul pool per tutti gli utenti a cui è stato assegnato il pool primario redmond-cs-001.litwareinc.com. A tale scopo, viene chiamato il cmdlet **Get-CsUser** insieme al parametro Filter. Il valore di filtro {$\_.PrimaryPoolFqdn -eq "redmond-cs-001.litwareinc.com"} restituisce solo gli utenti la cui proprietà PrimaryPoolFqdn è uguale a redmond-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsUserPoolInfo**, che recupera le informazioni sul pool per ogni utente della raccolta.

    Get-CsUser -Filter {$_.PrimaryPoolFqdn -eq "redmond-cs-001.litwareinc.com"} | Get-CsUserPoolInfo

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce le informazioni sui pool per tutti gli utenti ai quali non è stato assegnato un pool di registrazione di backup. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** per restituire un raccolta di tutti gli utenti che sono stati abilitati per Lync Server. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Get-CsUserPoolInfo**, che recupera le informazioni sui pool per ogni utente della raccolta. Le informazioni sui pool infine vengono inviate tramite pipe al cmdlet **Where-Object**, che visualizza i dati solo per gli utenti in cui la proprietà BackupPoolFqdn è uguale a un valore Null.

    Get-CsUser | Get-CsUserPoolInfo | Where-Object {$_.BackupPoolFqdn -eq $Null}

## Descrizione dettagliata

Quando un utente viene abilitato per Lync Server, deve trovarsi in un pool di registrazione. Questo pool è responsabile dell'autenticazione dell'utente e deve tenere traccia del relativo stato e della relativa posizione. Se è necessario conoscere il pool di registrazione al quale è stato assegnato un utente, è possibile recuperare queste informazioni utilizzando un comando simile al seguente:

    Get-CsUser "Ken Myer" | Select-Object RegistrarPool

In molti casi, sapere il pool di registrazione di un utente è tutto quel che serve sapere. In altri casi, potrebbe essere necessario conoscere a quale pool di registrazione di riserva è stato assegnato l'utente (il pool da utilizzare se il pool di registrazione primario non è disponibile), i nomi dei computer che compongono questo pool ed il pool servizi utente al quale è stato assegnato l'utente. Queste informazioni dettagliate possono essere recuperate eseguendo il cmdlet **Get-CsUserPoolInfo**.

Per Lync Server 2013, il cmdlet Get-CsUserPoolInfo è stato modificato in modo da restituire informazioni sui Front End Server primari di un utente nel relativo pool primario e nel relativo pool di replica. Quando in un pool sono inclusi diversi Front End Server, ogni utente viene assegnato a un gruppo di routing che, a sua volta, viene assegnato a un Front End Server primario e a un Front End Server di replica. Quando un utente esegue l'accesso, per impostazione predefinita viene registrato nel Front End Server primario. Nell'output di Get-CsUserPoolInfo tale server viene elencato come PrimaryPoolPrimaryRegistrar. Se per il pool primario dell'utente è stato eseguito il failover, tale utente verrà registrato nel Front End Server primario nel pool di backup (di replica). Tale server verrà elencato nell'output come BackupPoolPrimaryRegistrar.

Si noti che le informazioni di replica verranno visualizzate solo se al pool primario dell'utente è stato assegnato un pool di riserva.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsUserPoolInfo** i membri dei gruppi seguenti: RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserPoolInfo"}

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
<td><p>Indica l'identità dell'utente di cui si stanno recuperando le informazioni relative al pool utente. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Servizi di dominio Active Directory dell'utente (ad esempio, Davide Garghentini). È anche possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con cognome che termina con un valore di stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare le informazioni sul pool di utenti dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Get-CsUserPoolInfo** accetta gli input tramite pipeline dei valori stringa che rappresentano il nome di account SAM (SamAccountName) di un account utente abilitato per Lync Server. Il cmdlet accetta anche istanze di oggetti utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUserPoolInfo** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Xds.GetOCsUserPoolInfoCmdlet+UserInformation.

