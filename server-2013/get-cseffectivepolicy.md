---
title: Get-CsEffectivePolicy
TOCTitle: Get-CsEffectivePolicy
ms:assetid: 03b2984f-3a24-4b8d-bcaf-5049de9e2556
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204636(v=OCS.15)
ms:contentKeyID: 49299522
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsEffectivePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce i "criteri validi" per l'utente o gli utenti specificati. Se pertanto a un utente è stato assegnato un criterio per utente, verrà visualizzata l'identità di tale criterio. Se a un utente non è stato assegnato un criterio per utente, il cmdlet **Get-CsEffectivePolicy** indicherà se l'utente è gestito in base a un criterio del servizio, del sito o globale. In questo modo è possibile determinare esattamente quale criterio viene utilizzato per gestire un determinato utente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsEffectivePolicy -Identity <UserIdParameter> [-Credential <PSCredential>] [-DomainController <Fqdn>] [-ResultSize <Unlimited>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce i criteri validi per l'utente con nome visualizzato di Active Directory Ken Myer.

    Get-CsEffectivePolicy - Identity "Ken Myer"

## Esempio 2

Nel comando precedente vengono restituite informazioni sui criteri validi per gli utenti con nomi visualizzati Ken Myer e Pilar Ackerman. È possibile restituire informazioni sui criteri per più utenti inviando più identità utente tramite pipe al cmdlet **Get-CsEffectivePolicy**.

    "Ken Myer","Pilar Ackerman" | Get-CsEffectivePolicy

## Esempio 3

Nell'esempio 3 vengono restituite informazioni sui criteri validi per tutti gli utenti a cui è stato assegnato il criterio di conferenza RedmondConferencingPolicy. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** per restituire una raccolta di utenti a cui è stato assegnato il criterio RedmondConferencingPolicy. Utilizzando il parametro Filter con valore {ConferencingPolicy –eq "RedmondConferencingPolicy"} vengono restituiti solo i dati relativi agli utenti a cui è stato assegnato il criterio di conferenza per utente RedmondConferencingPolicy. Questa raccolta di account utente viene quindi inviata tramite pipe al cmdlet **Get-CsEffectivePolicy**, che visualizza informazioni sui criteri validi per ogni utente della raccolta.

    Get-CsUser -Filter {ConferencingPolicy -eq "RedmondConferencingPolicy"} | Get-CsEffectivePolicy

## Esempio 4

L'esempio 4 è una variante del comando riportato nell'esempio 3. Anche in questo esempio vengono restituite informazioni sui criteri validi per tutti gli utenti a cui è stato assegnato il criterio di conferenza RedmondConferencingPolicy. In questo caso però le informazioni restituite si limitano all'identità utente e al criterio per dispositivi mobili. Questo risultato viene ottenuto restituendo le informazioni su tutti i criteri validi e quindi inviandole tramite pipe al cmdlet **Select-Object**, che viene utilizzato a sua volta per limitare i dati visualizzati alle proprietà Identity e MobilityPolicy.

    Get-CsUser -Filter {ConferencingPolicy -eq "RedmondConferencingPolicy"} | Get-CsEffectivePolicy | Select-Object Identity, MobilityPolicy

## Esempio 5

Nell'esempio 5 vengono visualizzate informazioni sui criteri validi per tutti gli utenti del reparto Finance. A tale scopo, vengono utilizzati innanzitutto il cmdlet **Get-CsUser** e la proprietà LdapFilter per restituire una raccolta di account utente. Il valore di filtro "Department=Finance" limita gli account a quelli degli utenti che lavorano nel reparto Finance. La raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsEffectivePolicy**, che visualizza informazioni sui criteri validi per ogni utente della raccolta.

    Get-CsUser -LdapFilter "Department=Finance" | Get-CsEffectivePolicy

## Descrizione dettagliata

Il cmdlet **Get-CsUser** restituisce inoltre informazioni sui criteri di Microsoft Lync Server utilizzati per controllare il comportamento di un utente. Ad esempio:

DialPlan : RedmondDialPlan

LocationPolicy : RedmondLocationPolicy

ClientPolicy :

Dall'output precedente risulta che l'utente è gestito da un dial plan e da un criterio di percorso specifici, ma non da un client. In realtà l'utente è gestito da un criterio client, ovvero il criterio globale o un criterio del sito. Il cmdlet **Get-CsUser** tuttavia restituisce informazioni solo sui criteri per utente assegnati all'utente. Se l'utente è gestito da un criterio globale, del sito o del servizio, il cmdlet **Get-CsUser** non restituisce alcuna informazione.

In scenari di risoluzione dei problemi può essere molto utile sapere se un utente è gestito da un criterio globale, da un criterio del sito o da un criterio del servizio. In questi casi è possibile utilizzare il cmdlet **Get-CsEffectivePolicy** per restituire informazioni esatte sui criteri utilizzati per controllare il comportamento di un utente. Per l'utente precedente, il cmdlet **Get-CsEffectivePolicy** può restituire informazioni simili alle seguenti:

LocationProfile : RedmondDialPlan

LocationPolicy : RedmondLocationPolicy

ClientPolicy : Global

Questo output indica che l'utente è gestito dal criterio client globale.

Diversamente dal cmdlet **Get-CsUser**, il cmdlet **Get-CsEffectivePolicy** restituisce informazioni solo sui criteri. Non restituisce informazioni aggiuntive come il pool di registrazione o il numero di telefono dell'utente. Esistono inoltre alcune differenze nella terminologia utilizzata nel cmdlet **Get-CsUser** per etichettare i nomi dei criteri rispetto alla terminologia utilizzata dal cmdlet **Get-CsEffectivePolicy**. Per il cmdlet **Get-CsUser** ad esempio viene utilizzato il nome DialPlan, mentre per il cmdlet **Get-CsEffectivePolicy** viene utilizzato il nome LocationProfile.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsEffectivePolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsEffectivePolicy** non sono direttamente disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indica l'identità dell'account utente di cui vengono calcolate le impostazioni dei criteri effettivi. Le identità utente vengono specificate in genere con uno dei formati seguenti: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN), 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio litwareinc\kenmyer) e 4) il nome visualizzato di Active Directory dell'utente (ad esempio Ken Myer). È inoltre possibile fare riferimento all'account utente utilizzando il nome distinto dell'utente in Active Directory.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet Get-CsEffectivePolicy utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari per utilizzare gli oggetti utente.</p>
<p>Per utilizzare il parametro Credential, è necessario innanzitutto creare un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere nella Guida l'argomento relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sull'utente. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome di dominio completo (FQDN), ad esempio:</p>
<p>-DomainController &quot;atl-dc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette utenti (indipendentemente dal numero di utenti nella foresta), includere il parametro -ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette utenti saranno restituiti.</p>
<p>La dimensione del risultato può essere impostata su un numero intero compreso tra 0 e 2147483647, estremi inclusi. Se si imposta il parametro su 0, il comando verrà eseguito ma non restituirà dati. Se si imposta ResultSize su 7 ma la foresta include solo tre utenti, il comando restituirà i tre utenti e verrà completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Get-CsEffectivePolicy** accetta un valore stringa inviato tramite pipeline che rappresenta il nome visualizzato di un account utente abilitato per Lync Server. Il cmdlet accetta inoltre istanze dell'oggetto utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsEffectivePolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.AD.Cmdlets.EffectivePolicies.

## Vedere anche

#### Ulteriori risorse

[Get-CsUser](get-csuser.md)

