---
title: Debug-CsAddressBookReplication
TOCTitle: Debug-CsAddressBookReplication
ms:assetid: c138f274-7a1f-4074-b6a2-548274af5199
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205232(v=OCS.15)
ms:contentKeyID: 49301854
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsAddressBookReplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la replica tra Active Directory e il Servizio Rubrica di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Debug-CsAddressBookReplication [-DomainController <String>] [-User <String>] [-VerifyReplication <SwitchParameter>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PoolFqdn <Fqdn>] [-VerifyNormalization <SwitchParameter>]

## Esempi

## Esempio 1

Con il comando illustrato nell'esempio 1 è possibile verificare la replica del servizio Rubrica per il pool corrente. Per verificare la replica per un pool specificato, includere il parametro PoolFqdn seguito dal nome di dominio completo del pool da verificare.

    Debug-CsAddressBookReplication

## Esempio 2

Nell'esempio 2 il parametro User viene incluso per la verifica della replica del servizio Rubrica per il pool corrente. Quando il parametro User viene incluso, per l'utente specificato vengono restituite informazioni aggiuntive correlate.

    Debug-CsAddressBookReplication -User "sip:kenmyer@litwareinc.com"

## Esempio 3

Nell'esempio 3 viene utilizzato il parametro VerifyReplication per apportare una modifica all'account utente specificato e quindi verificare che la modifica venga replicata correttamente nella Rubrica.

    Debug-CsAddressBookReplication -User "sip:kenmyer@litwareinc.com" -VerifyReplication 

## Esempio 4

Il comando riportato nell'esempio 4 utilizza il parametro VerifyNormalization per restituire informazioni sugli account utente in cui non è stato possibile applicare le regole di normalizzazione della Rubrica.

    Debug-CsAddressBookReplication -VerifyNormalization

## Descrizione dettagliata

I server della Rubrica sono intermediari tra Servizi di dominio Active Directory e Microsoft Lync Server. Il server della Rubrica garantisce che le informazioni utente archiviate in Lync Server siano sincronizzate con le informazioni utente archiviate in Servizi di dominio Active Directory. A tale scopo, i file della Rubrica vengono sincronizzati periodicamente con le informazioni archiviate nel database utenti.

Il cmdlet **Debug-CsAddressBookReplication** consente agli amministratori di verificare che venga eseguita la replica dei dati tra Active Directory e Lync Server. La verifica completa della replica tra Active Directory e il server della Rubrica può essere un'attività a elevato utilizzo di risorse che richiede tempo. Per questo motivo, è consigliabile utilizzare **Debug-CsAddressBookReplication** solo in scenari di risoluzione dei problemi. Se si desidera eseguire periodicamente un "controllo a campione" del funzionamento del server della Rubrica, utilizzare piuttosto il cmdlet **Test-CsAddressBookService** e/o **Test-CsAddressBookWebQuery**.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsAddressBookReplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet D**ebug-CsAddressBookReplication** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un controller di dominio a cui connettersi per la verifica della replica del servizio Rubrica. Se questo parametro non viene incluso, verrà utilizzato il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre un carattere $ quando si specifica il nome della variabile.</p>
<p>Per salvare le informazioni archiviate nella variabile del logger su un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando analogo al seguente:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato risultante derivante dall'esecuzione del cmdlet verrà archiviato nella variabile specificata. Ad esempio, per archiviare l'output in una variabile denominata $TestOutput utilizzare la sintassi seguente</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool da verificare. Se questo parametro non viene incluso, il pool corrente verrà verificato tramite il cmdlet <strong>Debug-CsAddressBookReplication</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>User</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se incluso, restituisce informazioni dettagliate sulla replica per gli account utente specificati. L'account utente da verificare può essere specificato utilizzando l'indirizzo SIP, l'indirizzo di posta elettronica o SamAccountName dell'utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>VerifyNormalization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, verranno restituite informazioni dettagliate per gli account utente per cui la normalizzazione della Rubrica non è riuscita. Le regole di normalizzazione vengono utilizzate per convertire i numeri di telefono nel formato E.164 utilizzato da Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyReplication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, il cmdlet <strong>Debug-CsAddressBookReplication</strong> modificherà l'account utente specificato in Active Directory e verificherà che le modifiche vengano replicate nella Rubrica. Si noti che la modifica dell'account utente è solo per scopi di test e non interesserà i valori delle proprietà di quell'account.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Debug-CsAddressBookReplication** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Debug-CsAddressBookReplication** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.Activities.Database.AddressBookReplicationTaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

