---
title: Get-CsCallParkOrbit
TOCTitle: Get-CsCallParkOrbit
ms:assetid: 73bbb09a-7966-4af1-aff3-001f5cc56df1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398554(v=OCS.15)
ms:contentKeyID: 49300978
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCallParkOrbit

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ottiene le impostazioni di intervallo di codici orbit del parcheggio di chiamata per l'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsCallParkOrbit [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsCallParkOrbit [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Type <CallPark | GroupPickup>]

## Esempi

## ESEMPIO 1

In questo esempio viene utilizzato il cmdlet **Get-CsCallParkOrbit** senza specificare parametri aggiuntivi. Se utilizzato in questo modo, il cmdlet **Get-CsCallParkOrbit** restituisce una raccolta di tutti gli intervalli di codici orbit del parcheggio di chiamata configurati per l'utilizzo nella propria organizzazione.

    Get-CsCallParkOrbit

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il cmdlet **Get-CsCallParkOrbit** per restituire informazioni sull'intervallo di codici orbit del parcheggio di chiamata denominato "Redmond CPO 1".

    Get-CsCallParkOrbit -Identity "Redmond CPO 1"

## ESEMPIO 3

Con il comando riportato in questo esempio vengono restituiti tutti gli intervalli di orbit del parcheggio di chiamata che contengono la stringa "Redmond" nel relativo parametro Identity. Ad esempio, questo comando consente di ottenere gli orbit del parcheggio di chiamata con identità come "Redmond 501", "CP Redmond 1" e "ARedmond". Il comando utilizza il parametro Filter con il carattere jolly (\*) per definire l'oggetto della ricerca. Per la ricerca non viene applicata la distinzione tra maiuscole e minuscole.

    Get-CsCallParkOrbit -Filter *Redmond*

## ESEMPIO 4

Questo comando restituisce tutti gli intervalli di codici orbit del parcheggio di chiamata assegnati al servizio di parcheggio di chiamata con ID ApplicationServer:pool0.litwareinc.com. Il cmdlet **Get-CsCallParkOrbit** recupera una raccolta di tutti gli intervalli di codici orbit del parcheggio di chiamata e quindi la invia tramite pipe al cmdlet **Where-Object**. La chiamata al cmdlet **Where-Object** consente di trovare tutti i codici orbit del parcheggio di chiamata inclusi nella raccolta le cui rispettive proprietà CallParkServiceId includono il valore ApplicationServer:pool0.litwareinc.com. Si noti che è stato aggiunto il metodo toString alla fine del nome del parametro CallParkServiceId. CallParkServiceId è di tipo WritableServiceId. Per poter confrontare questo valore con la stringa fornita è necessario convertirlo in una stringa chiamando il metodo toString.

    Get-CsCallParkOrbit | Where-Object {$_.CallParkServiceId.toString() -eq "ApplicationServer:pool0.litwareinc.com"}

## ESEMPIO 5

Il comando riportato in questo esempio restituisce tutti gli intervalli di codici orbit del parcheggio di chiamata in cui l'intervallo di numeri inizia con il prefisso \*. Dopo che il cmdlet **Get-CsCallParkOrbit** ha recuperato una raccolta di tutti gli intervalli di codici orbit del parcheggio di chiamata, la raccolta viene inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** circoscrive la raccolta agli intervalli di codici orbit del parcheggio di chiamata la cui località inizia con \*. A tale scopo, viene ricercata nella proprietà StartsWith dell'oggetto NumberRangeStart la stringa "\*".

    Get-CsCallParkOrbit | Where-Object {$_.NumberRangeStart.StartsWith("*")}

## ESEMPIO 6

Il comando riportato in questo esempio restituisce tutti gli intervalli di codici orbit del parcheggio di chiamata in cui ai numeri dell'intervallo non è stato assegnato alcun prefisso. Per prefisso si intende il valore \* o \# anteposto al numero. Tutti i codici orbit del parcheggio di chiamata restituiti da questo comando avranno intervalli costituiti esclusivamente da numeri, senza caratteri. Il cmdlet **Get-CsCallParkOrbit** recupera una raccolta di tutti gli intervalli di codici orbit del parcheggio di chiamata, che viene poi inviata tramite pipe al cmdlet **Where-Object**. I criteri della chiamata al cmdlet **Where-Object** sono i seguenti: $\_.NumberRangeStart\[0\]). Questo criterio restituisce il primo carattere del numero iniziale dell'intervallo. Si noti che deve essere controllato solo l'inizio dell'intervallo: se il prefisso non è contenuto all'inizio, è chiaramente assente. Questo carattere viene passato alla funzione IsDigit per stabilire se si tratta di un carattere numerico. In questo caso, verranno restituite le informazioni sul codice orbit del parcheggio di chiamata per il corrispondente elemento della raccolta.

    Get-CsCallParkOrbit | Where-Object {[Char]::IsDigit($_.NumberRangeStart[0])}

## Descrizione dettagliata

Questo cmdlet recupera le impostazioni per i codici orbit del parcheggio di chiamata definiti per un'organizzazione. È possibile recuperare un singolo intervallo di codici orbit del parcheggio di chiamata (specificato dal parametro Identity) oppure utilizzare il cmdlet **Get-CsCallParkOrbit** senza parametri per recuperare tutti gli intervalli di codici orbit del parcheggio di chiamata definiti per un'organizzazione. I codici orbit del parcheggio di chiamata sono costituiti da impostazioni che specificano un intervallo di numeri presso cui un utente può parcheggiare una chiamata e i server associati a tali intervalli di numeri.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsCallParkOrbit** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmin. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCallParkOrbit"}

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
<td><p>Questo parametro accetta una stringa di caratteri jolly e restituisce tutti gli intervalli orbit del parcheggio di chiamata con identità corrispondenti a tale stringa. Ad esempio, il valore Redmond* specificato per il filtro consente di ottenere tutti gli orbit del parcheggio di chiamata i cui nomi iniziano con la stringa Redmond, ad esempio Redmond 1, Redmond 2 e RedmondCPO.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome univoco dell'intervallo orbit del parcheggio di chiamata. Questo nome viene assegnato dall'amministratore durante la definizione dell'intervallo orbit del parcheggio di chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di orbit del parcheggio di chiamata dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Core.OrbitType</p></td>
<td><p>Specifica il tipo di codice orbit del parcheggio di chiamata da recuperare. Lync Server 2013 supporta due tipi diversi di codici orbit del parcheggio di chiamata:</p>
<p>CallPark. Questo è il codice orbit standard del parcheggio di chiamata, in base al quale un utente mette una chiamata in attesa e quindi può recuperarla da un altro telefono componendo il numero del parcheggio di chiamata specificato.</p>
<p>GroupPickup. Con la risposta alle chiamate di gruppo, gli utenti possono rispondere a una chiamata in arrivo effettuata a qualsiasi membro del gruppo di risposta alle chiamate di gruppo. I gruppi di risposta alle chiamate di gruppo vengono configurati dagli amministratori.</p>
<p>Per restituire un tipo specifico di codice orbit del parcheggio di chiamata, utilizzare una sintassi simile alla seguente:</p>
<p>-Type GroupPickup</p>
<p>Per restituire tutti i codici orbit del parcheggio di chiamata, indipendentemente dal tipo, omettere il parametro Type.</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbits.

## Vedere anche

#### Ulteriori risorse

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Remove-CsCallParkOrbit](remove-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)

