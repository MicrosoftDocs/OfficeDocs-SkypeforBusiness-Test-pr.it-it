---
title: Grant-CsConferencingPolicy
TOCTitle: Grant-CsConferencingPolicy
ms:assetid: 43c63a01-5072-45f0-89ee-8c3ae0cd9035
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425937(v=OCS.15)
ms:contentKeyID: 49300356
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsConferencingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio conferenza nell'ambito per utente. I criteri conferenza determinano le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella conferenza le funzionalità audio e video IP e il numero massimo di persone che possono partecipare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsConferencingPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Grant-CsConferencingPolicy** viene utilizzato per assegnare il criterio SalesConferencingPolicy all'utente con identità "Ken Myer".

    Grant-CsConferencingPolicy -identity "Ken Myer" -PolicyName SalesConferencingPolicy

## ESEMPIO 2

Nell'esempio 2 il criterio conferenza FinanceConferencingPolicy viene assegnato a tutti gli utenti che hanno un account nell'unità organizzativa Finance. Per assegnare lo stesso criterio a tutti gli utenti di una determinata unità organizzativa (OU), viene utilizzato il cmdlet **Get-CsUser** per recuperare tutti gli account di tale unità. Dopo il recupero degli account utente, queste informazioni vengono inviate tramite pipe al cmdlet **Grant-CsConferencingPolicy**, che assegna il criterio FinanceConferencingPolicy a ogni utente incluso nella raccolta.

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Grant-CsConferencingPolicy -PolicyName FinanceConferencingPolicy

## ESEMPIO 3

L'esempio 3 rappresenta una variante dell'esempio 2. In questo caso, però, per gli utenti nell'unità organizzativa Finance viene annullata l'assegnazione dei criteri di conferenza per utente. A tale scopo, il comando chiama il cmdlet **Grant-CsConferencingPolicy** e specifica un valore Null ($Null) per il parametro PolicyName.

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Grant-CsConferencingPolicy -PolicyName $Null

## ESEMPIO 4

Nell'esempio 4 viene assegnato il criterio HRConferencingPolicy a tutti gli utenti che lavorano nel reparto Human Resources. A tale scopo, vengono chiamati il cmdlet **Get-CsUser** e il parametro LdapFilter per recuperare l'insieme di utenti appropriato. Il valore di parametro "Department=Human Resources" garantisce che vengano restituiti solo gli account utente in cui l'attributo Department è stato impostato su "Human Resources". Dopo il recupero degli account utente, la raccolta viene inviata tramite pipe al cmdlet **Grant-CsConferencingPolicy**, che assegna il criterio HRConferencingPolicy a ogni utente incluso nella raccolta.

    Get-CsUser -LdapFilter "Department=Human Resources" | Grant-CsConferencingPolicy -PolicyName HRConferencingPolicy

## Descrizione dettagliata

Le conferenze rappresentano un aspetto importante di Lync Server: consentono a gruppi di utenti di incontrarsi online per visualizzare diapositive e video, condividere applicazioni, scambiare file e comunicare e collaborare in altro modo.

Per gli amministratori è importante mantenere il controllo sulle conferenze e sulle impostazioni della conferenza. In alcuni casi potrebbero esserci problemi di sicurezza: per impostazione predefinita, chiunque, inclusi gli utenti non autenticati, può partecipare alle riunioni e salvare le presentazioni o gli stampati distribuiti durante queste riunioni. In altri casi potrebbero esserci problemi di larghezza di banda: molte riunioni contemporaneamente, ciascuna con centinaia di partecipanti e con feed video e scambio di file, possono causare dei problemi sulla rete. In aggiunta, possono esserci occasionali problemi legali. Ad esempio, per impostazione predefinita i partecipanti alla riunione possono effettuare annotazioni sui contenuti condivisi, tuttavia queste annotazioni non vengono salvate quando la riunione viene archiviata. Se l'organizzazione è tenuta a conservare tutte le comunicazioni elettroniche, potrebbe essere opportuno disabilitare le annotazioni.

Esiste naturalmente una differenza tra la teoria della gestione delle impostazioni delle conferenze e l'effettiva gestione di queste impostazioni. In Lync Server le conferenze vengono gestite con specifici criteri. Nelle precedenti versioni del software questi criteri sono conosciuti come criteri riunione. Come già detto, i criteri conferenza consentono di stabilire le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella riunione audio e video IP o il numero massimo di persone che possono partecipare. I criteri conferenza possono essere configurati nell'ambito globale, del sito o di un singolo utente. In questo modo gli amministratori possono stabilire quali funzionalità rendere disponibili per ogni utente.

Quando si crea un criterio a livello di sito, il criterio viene assegnato automaticamente al sito appropriato al momento della creazione. Questo non è applicabile per i criteri per utente, i quali non vengono assegnati ad alcun utente mentre vengono creati. È invece necessario utilizzare il cmdlet **Grant-CsConferencingPolicy** per assegnare esplicitamente criteri di conferenza per utente a un utente o a un gruppo di utenti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Grant-CsConferencingPolicy** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsConferencingPolicy"}

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
<td><p>Indica l'identità dell'account utente al quale devono essere assegnati i criteri. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). Alle identità utente è anche possibile fare riferimento utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si specifica l'identità utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti con un nome visualizzato che termina con la stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>&quot;Nome&quot; del criterio da assegnare. Il PolicyName è semplicemente l'Identity del criterio meno l'ambito (il prefisso &quot;tag:&quot;). Ad esempio, un criterio con Identity tag:Redmont ha un PolicyName uguale a Redmond; un criterio con Identity tag:RedmondConferencingPolicy ha un PolicyName uguale a RedmondConferencingPolicy.</p>
<p>Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare il parametro PolicyName su $Null.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare il nome di dominio completo (FQDN) di un controller di dominio da contattare durante l'assegnazione del nuovo criterio. Se questo parametro non viene specificato, il cmdlet <strong>Grant-CsConferencingPolicy</strong> contatterà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare attraverso la pipeline un oggetto utente che rappresenta l'utente al quale si sta assegnando il criterio. Per impostazione predefinita, il cmdlet <strong>Grant-CsConferencingPolicy</strong> non fornisce alcun oggetto attraverso la pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsConferencingPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsConferencingPolicy** non restituisce oggetti o valori. Se però si include il parametro PassThru, il cmdlet restituirà istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)

