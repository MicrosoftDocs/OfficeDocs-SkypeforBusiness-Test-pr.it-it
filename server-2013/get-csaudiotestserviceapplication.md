---
title: Get-CsAudioTestServiceApplication
TOCTitle: Get-CsAudioTestServiceApplication
ms:assetid: ef36a059-bf9b-4066-a817-db8d82c41e49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412984(v=OCS.15)
ms:contentKeyID: 49302392
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioTestServiceApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di ottenere informazioni relative all'applicazione di servizio test audio utilizzata nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAudioTestServiceApplication [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Nell'esempio 1, viene utilizzato il cmdlet **Get-CsAudioTestServiceApplication** senza altri parametri per ottenere una raccolta di tutti i contatti del servizio test audio utilizzati al momento nell'organizzazione.

    Get-CsAudioTestServiceApplication

## ESEMPIO 2

Nell'Esempio 2 viene restituito un singolo contatto del servizio test audio: il contatto con Identity sip:RedmondAudioTest@litwareinc.com.

    Get-CsAudioTestServiceApplication -Identity "sip:RedmondAudioTest@litwareinc.com"

## ESEMPIO 3

Nell'Esempio 3 vengono restituiti tutti i contatti del servizio test audio con un nome visualizzato che contiene il valore di stringa "Redmond". Per ottenere questo risultato il comando utilizza il parametro Filter ed il valore di filtro {DisplayName –like "\*Redmond\*"}; questo valore di filtro limita i contatti restituiti a quelli il cui nome visualizzato contiene il valore di stringa "Redmond". Questo comando restituisce i contatti con nome visualizzato "Redmond Audio Test Service Contact", "Redmond Audio Bot" e "Test Contact for Redmond".

    Get-CsAudioTestServiceApplication -Filter {DisplayName -like "*Redmond*"}

## Descrizione dettagliata

Il servizio test audio consente agli utenti di Lync Server di verificare le connessioni vocali prima di effettuare una chiamata. Per ottenere questo risultato, fare clic sul pulsante Controlla qualità chiamata che si trova sulla scheda Dispositivo audio della finestra di dialogo Opzioni di Lync Server. Quando un utente fa clic su questo pulsante, verrà effettuata una chiamata al servizio di test audio automatizzato. Alla chiamata viene risposto e, dopo la riproduzione di una breve introduzione, viene chiesto all'utente di registrare un breve messaggio. La registrazione verrà quindi riprodotta, consentendo al chiamante di ascoltare il proprio messaggio sulla connessione corrente.

Il servizio test audio fa affidamento, in parte, sugli oggetti contatto di Active Directory. Questi oggetti vengono creati automaticamente durante l'installazione di Audio Bot; non esiste la possibilità di creare manualmente questi oggetti. Tuttavia gli amministratori possono utilizzare il cmdlet **Get-CsAudioTestServiceApplication** per recuperare le informazioni sui diversi contatti del servizio di test utilizzati al momento nell'organizzazione. Gli amministratori possono utilizzare **Set-CsAudioTestServiceApplication** anche per modificare le proprietà di questi contatti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsAudioTestServiceApplication** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAudioTestServiceApplication"}

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
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti contatto.</p>
<p>Per utilizzare il parametro Credential è necessario creare per prima cosa un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sul contatto. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-cs-001) o dal nome di dominio completo (FQDN) (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici per Lync Server. Ad esempio, è possibile limitare i dati restituiti agli oggetti contatto del test audio con un nome visualizzato specifico o a quelli che fanno uso di una particolare lingua.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisca solo i contatti con nome visualizzato Audio Test Service Contacts assomiglierà al seguente, con DisplayName che rappresenta l'attributo di Active Directory, -eq che rappresenta l'operatore di comparazione (uguale a); &quot;Audio Test Service Contact&quot; che rappresenta il valore del filtro:</p>
<p>-Filter {DisplayName -eq &quot;Audio Test Service Contact&quot;}</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indirizzo SIP del contatto del servizio test audio.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di limitare i contatti recuperati da una specifica unità organizzativa di Active Directory (OU). Il parametro OU restituisce i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, saranno restituiti gli utenti di tutte e tre le unità organizzative.</p>
<p>Per specificare una OU occorre utilizzare il nome distinto (DN) del contenitore, ad esempio: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti da un comando. Ad esempio, per ottenere sette utenti (indipendentemente dal numero di utenti nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Si noti che non c'è modo di stabilire quali saranno i sette utenti restituiti. Se si imposta ResultSize su 7, ma la foresta contiene solo tre utenti, il comando restituirà i tre utenti e verrà completato senza errori.</p>
<p>ResultSize può essere impostato su qualsiasi numero intero compreso tra 0 e 2147483647. Se impostato su 0, il comando verrà eseguito ma i dati non verranno restituiti.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsAudioTestServiceApplication** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[Set-CsAudioTestServiceApplication](set-csaudiotestserviceapplication.md)

