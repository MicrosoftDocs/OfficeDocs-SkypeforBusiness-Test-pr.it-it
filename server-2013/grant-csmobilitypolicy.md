---
title: Grant-CsMobilityPolicy
TOCTitle: Grant-CsMobilityPolicy
ms:assetid: c5ca6d6c-e442-4375-b8fd-1016a0aef33b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690038(v=OCS.15)
ms:contentKeyID: 49301934
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsMobilityPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna a un utente o a un gruppo di utenti i criteri per dispositivi mobili per utente. I criteri per dispositivi mobili determinano se un utente può o meno utilizzare Lync Mobile. Questi criteri gestiscono inoltre la capacità di un utente di utilizzare la funzionalità Chiamata tramite ufficio, che consente agli utenti di effettuare e ricevere chiamate telefoniche sul cellulare utilizzando il numero dell'ufficio anziché quello del cellulare. I criteri per dispositivi mobili possono essere utilizzati anche per richiedere connessioni Wi-Fi quando si effettuano o ricevono chiamate. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Grant-CsMobilityPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di assegnare il criterio per dispositivi mobili per utente RedmondMobilityPolicy a un singolo utente: Davide Garghentini.

    Grant-CsMobilityPolicy -Identity "Ken Myer" -PolicyName "RedmondMobilityPolicy"

## ESEMPIO 2

Nell'esempio 2 il criterio per dispositivi mobili RedmondMobilityPolicy viene assegnato agli utenti attualmente gestiti dal criterio NorthAmericaMobilityPolicy. A tale scopo, nel comando vengono utilizzati innanzitutto il cmdlet **Get-CsUser** e il parametro Filter per recuperare tutti gli utenti a cui è assegnato il criterio NorthAmericaMobilityPolicy. Questo risultato viene ottenuto utilizzando il valore di filtro {MobilityPolicy –eq "NorthAmericaMobilityPolicy"}. Dopo aver recuperato la raccolta di account utente, gli account vengono quindi inviati tramite pipe al cmdlet **Grant-CsMobilityPolicy**, che assegna a ogni utente il criterio RedmondMobilityPolicy.

    Get-CsUser -Filter {MobilityPolicy -eq "NorthAmericaMobilityPolicy"} | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## ESEMPIO 3

Nell'esempio 3 vengono assegnati i criteri per dispositivi mobili RedmondMobilityPolicy a tutti gli utenti che si trovano a Redmond. A tale scopo, il comando chiama prima di tutto il cmdlet **Get-CsUser** insieme al parametro LdapFilter. Il valore di filtro "l=Redmond" restituisce tutti gli utenti che si trovano a Redmond. "l" rappresenta l'attributo "locality" di Active Directory. Dopo essere stati recuperati, gli account utente vengono inviati tramite pipe al cmdlet **Grant-CsMobilityPolicy**. A sua volta, il cmdlet **Grant-CsMobilityPolicy** assegna a ogni utente i criteri RedmondMobilityPolicy.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## ESEMPIO 4

Nell'esempio 4 il criterio RedmondMobilityPolicy viene assegnato agli utenti che dispongono di account Lync Server in atl-cs-001.litwareinc.com. A tale scopo, nel comando vengono utilizzati innanzitutto il cmdlet **Get-CsUser** e il parametro Filter per recuperare tutti gli account utente che si trovano nel pool di registrazione specificato. Questo risultato viene ottenuto utilizzando il valore di filtro {RegistrarPool –eq "atl-cs-001.litwareinc.com"}. Dopo aver recuperato la raccolta di account utente, gli account vengono quindi inviati tramite pipe al cmdlet **Grant-CsMobilityPolicy**, che assegna a ogni utente il criterio RedmondMobilityPolicy.

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## Descrizione dettagliata

Lync Mobile è un'applicazione client che consente agli utenti di eseguire Lync nei cellulari. La caratteristica Chiamata tramite ufficio consente agli utenti di effettuare chiamate con il cellulare che risultano provenire dal numero dell'ufficio anziché da quello del cellulare. Gli utenti abilitati per la caratteristica Chiamata tramite ufficio possono ottenere questo risultato componendo il numero direttamente dal cellulare oppure utilizzando l'opzione di conferenza telefonica con chiamata in uscita. Con questa opzione, un utente richiede in effetti al server dei servizi per dispositivi mobili di effettuare una chiamata al suo posto. La chiamata viene configurata dal server e quindi l'utente viene richiamato sul cellulare. Dopo che l'utente ha risposto, il server compone il numero della parte chiamata. Entrambe queste funzionalità possono essere gestite tramite i criteri per dispositivi mobili.

Con Lync Server 2013, i dispositivi mobili possono effettuare o ricevere chiamate tramite la rete cellulare standard oppure tramite connessioni Wi-Fi. I criteri per dispositivi mobili possono essere utilizzati per richiedere connessioni Wi-Fi e impedire le chiamate tramite la rete cellulare.

Quando si installa Lync Server, è presente un singolo criterio per dispositivi mobili globale che si applica a tutti gli utenti. Gli amministratori possono tuttavia utilizzare il cmdlet **New-CsMobilityPolicy** per creare criteri personalizzati nell'ambito del sito o per utente.

Se si crea un nuovo criterio nell'ambito del sito, il criterio viene automaticamente assegnato al sito appropriato. Se tuttavia si crea un criterio per dispositivi mobili nell'ambito per utente, il criterio viene creato ma non viene assegnato automaticamente ad alcun utente. È necessario utilizzare il cmdlet **Grant-CsMobilityPolicy** per assegnare in modo specifico un criterio per dispositivi mobili a uno o più utenti.

Si noti che i criteri per dispositivi mobili non vengono visualizzati per impostazione predefinita quando si esegue il cmdlet **Get-CsUser**. Per questo motivo, non è possibile visualizzare i criteri per dispositivi mobili per utente assegnati a un utente eseguendo un comando analogo al seguente:

Get-CsUser "Davide Garghentini"

È invece necessario utilizzare un comando analogo al seguente per visualizzare tutti i valori delle proprietà, inclusi i criteri per dispositivi mobili, per un utente:

Get-CsUser "Davide Garghentini" | Select-Object \*

In alternativa, è possibile utilizzare un comando analogo al seguente per visualizzare solo il nome visualizzato e i criteri per dispositivi mobili per l'utente:

Get-CsUser "Davide Garghentini" | Select-Object DisplayName, MobilityPolicy

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Grant-CsMobilityPolicy** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Indica il valore Identity dell'account utente a cui assegnare il criterio per dispositivi mobili per utente. Le identità utente vengono in genere specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio litwareinc\davidegarghentini), 4) il nome visualizzato Active Directory dell'utente (ad esempio Davide Garghentini). È possibile specificare le identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come valore Identity dell'utente. L'identità &quot;* Smith&quot; consente, ad esempio, di assegnare il criterio a tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>&quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno l'ambito del criterio (prefisso &quot;tag:&quot;). Un criterio con valore Identity tag:Redmond ha ad esempio un parametro PolicyName uguale a Redmond, mentre un criterio con valore Identity tag:RedmondUsersMobilityPolicy ha un parametro PolicyName uguale a RedmondUsersMobilityPolicy. Per assegnare un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-PolicyName RedmondUsersMobilityPolicy</p>
<p>Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare PolicyName su un valore Null ($Null).</p>
<p>-PolicyName $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare il nome di dominio completo di un controller di dominio da contattare durante l'assegnazione del nuovo criterio. Se questo parametro non viene specificato, il cmdlet <strong>Grant-CsMobilityPolicy</strong> si metterà in contatto con il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare attraverso la pipeline un oggetto utente che rappresenta l'utente a cui viene assegnato il criterio. Per impostazione predefinita, il cmdlet <strong>Grant-CsMobilityPolicy</strong> non passa oggetti attraverso la pipeline.</p></td>
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

Il cmdlet **Grant-CsMobilityPolicy** accetta input tramite pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta anche input tramite pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsMobilityPolicy** non restituisce alcun oggetto o valore. Se tuttavia si include il parametro PassThru, il cmdlet sarà in grado di inviare tramite pipeline istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

