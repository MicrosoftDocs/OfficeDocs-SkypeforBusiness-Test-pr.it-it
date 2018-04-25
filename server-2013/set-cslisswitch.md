---
title: Set-CsLisSwitch
TOCTitle: Set-CsLisSwitch
ms:assetid: ad2a1890-724a-4f9f-bd50-de0c9de86f8e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412823(v=OCS.15)
ms:contentKeyID: 49301643
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisSwitch

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un commutatore del server Informazioni percorso, crea un'associazione tra un commutatore e una posizione (creando una nuova posizione se questa non esiste) o modifica un commutatore esistente e la relativa posizione associata. L'associazione tra commutatore e posizione viene utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la posizione del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLisSwitch -ChassisID <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisSwitch -ChassisID <String> [-Description <String>] <COMMON PARAMETERS>

    Set-CsLisSwitch -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata o aggiornata una voce posizione commutatore LIS. Il comando nell'esempio include solo un parametro (obbligatorio): ChassisID. Il valore di ChassisID è l'indirizzo MAC del commutatore, in questo caso 99-99-99-99-99-99.

Si noti che in questo esempio non vengono incluse informazioni sull'indirizzo. È possibile creare una voce commutatore sul Location Information Server senza associarla a un indirizzo. Tuttavia, le chiamate di emergenza instradate tramite questo commutatore potrebbero (a seconda della subnet o delle posizioni di porta definite) non contenere informazioni sufficiente perché l'operatore di emergenza identifichi una posizione.

IMPORTANTE: Se una posizione di un commutatore LIS con questo parametro ChassisID esiste già, verrà sostituito dai valori in questo comando. Questo significa che se questo commutatore fosse associato a un indirizzo (una posizione fisica), tale associazione non esisterebbe più perché non è stata inclusa nel comando alcuna informazioni sulla posizione. La posizione continuerà a esistere nel database delle posizioni ma non verrà associato a questo commutatore.

    Set-CsLisSwitch -ChassisID 99-99-99-99-99-99

## ESEMPIO 2

Nell'esempio 2 viene aggiornato il commutatore creato nell'esempio 1 aggiungendo informazioni sull'indirizzo (in realtà verrà eliminata la voce esistente e sostituita con questa nuova voce). Se l'indirizzo non esiste nel database delle posizioni, questo cmdlet creerà tale posizione.

    Set-CsLisSwitch -ChassisID 99-99-99-99-99-99 -Location "30/1000" -HouseNumber 1234 -PreDirectional NE -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente all'operatore di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata sia effettuata da una connessione VoIP (Voice over Internet Protocol), queste informazioni devono essere estrapolate in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet consente all'amministratore di mappare le posizioni fisiche al connettore di rete tramite cui il client viene connesso.

Il parametro ChassisID è l'unico parametro richiesto per questo cmdlet. Se si immette un valore ChassisID già esistente, questo cmdlet aggiorna la posizione di tale connettore in base ai parametri di posizione forniti. Se ChassisID non esiste, verrà creata una nuova posizione commutatore.

Se nel database delle posizioni non esiste una posizione con un indirizzo che corrisponde esattamente ai parametri immessi qui (inclusi i valori NULL), verrà creato un nuovo indirizzo in base ai parametri immessi con questo cmdlet. Per recuperare un elenco di posizioni, è possibile chiamare il cmdlet **Get-CsLisLocation**. Il cmdlet **Set-CsLisSwitch** non richiede parametri di posizione. È possibile creare una voce commutatore senza associarla a una posizione. È inoltre possibile creare una posizione non valida con questo cmdlet. Una posizione valida è costituita, come minimo, dai parametri Location, HouseNumber, StreetName, City, State e Country. Se non si forniscono tutti questi parametri, è possibile che le chiamate ricevute dal commutatore a cui si fa riferimento non contengano le informazioni richieste dall'operatore di emergenza (a seconda del fatto che siano disponibili o meno impostazioni valide per una subnet o un punto di accesso wireless utilizzabili in sostituzione delle impostazioni del commutatore). È consigliabile essere più specifici possibile con i parametri della posizione e completarne il maggior numero possibile.

È anche possibile creare le voci commutatore chiamando il cmdlet **Set-CsLisPort**. Se si chiama il cmdlet **Set-CsLisPort** con un valore ChassisID che non presenta una voce commutatore esistente, tale commutatore verrà creato.

È importante notare che queste modifiche diventano effettive solo se è stata configurata la proprietà MACResolverUrl tramite il cmdlet [New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md) o [Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md). La proprietà MACResolverUrl specifica l'URL di un servizio Web in grado di determinare da un indirizzo IP l'indirizzo MAC (Media Access Control) della scheda di rete associata all'indirizzo IP.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsLisSwitch** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisSwitch"}

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
<td><p><em>ChassisID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo MAC (Media Access Control) del commutatore di rete. Questo valore deve essere in formato nn-nn-nn-nn-nn-nn, ad esempio 12-34-56-78-90-ab, o nel formato di un indirizzo IP. Se non esiste una voce con il valore ChassisID specificato, verrà creata una nuova posizione commutatore. Se non esiste una voce con il parametro ChassisID specificato, tale voce verrà sostituita.</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La città della posizione.</p>
<p>Lunghezza massima: 64 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>CompanyName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della società in questa posizione.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il paese/area geografica in cui si trova la posizione.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione dettagliata di questa posizione commutatore di rete.</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della posizione. Nel caso di una società indica il numero della strada in cui ha sede la società.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, come 1/2 o A. Ad esempio: 1234 1/2 Oak Street o 1234 A Elm Street.</p>
<p>Nota: per indicare un numero di appartamento o di un ufficio, è necessario utilizzare il parametro Location. Ad esempio: -Location &quot;Suite 100/Office 150&quot;.</p>
<p>Lunghezza massima: 5 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della posizione. Generalmente questo valore è il nome di una posizione più specifica rispetto all'indirizzo civico, quale un numero di ufficio, ma può essere qualsiasi valore stringa.</p>
<p>Lunghezza massima: 20 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il codice postale associato a questa posizione.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La designazione direzionale di una via. Esempio: NE o NW per Main Street NE o 7th Avenue NW.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La designazione direzionale per un nome di una via che precede il nome della via. Esempio: NE o NW per NE Main Street o NW 7th Avenue.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Lo stato o la provincia associato a questa posizione.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della via per questa posizione.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il tipo di via indicato nel nome, ad esempio Street, Avenue o Court.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
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

Accetta l'input da pipeline di oggetti commutatore LIS.

## Tipi restituiti

Questo cmdlet consente di creare o modificare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisSwitch](remove-cslisswitch.md)  
[Get-CsLisSwitch](get-cslisswitch.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Set-CsLisPort](set-cslisport.md)  
[Get-CsLisPort](get-cslisport.md)

