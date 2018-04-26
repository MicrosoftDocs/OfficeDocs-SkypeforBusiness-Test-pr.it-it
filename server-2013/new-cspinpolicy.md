---
title: New-CsPinPolicy
TOCTitle: New-CsPinPolicy
ms:assetid: d64fb0f9-1cdc-4497-992a-d002abafe92e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398935(v=OCS.15)
ms:contentKeyID: 49302122
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPinPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio PIN client. L'autenticazione tramite PIN consente agli utenti di accedere a Lync Server immettendo il proprio PIN anziché il nome utente e la password. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsPinPolicy -Identity <XdsIdentity> [-AllowCommonPatterns <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaximumLogonAttempts <UInt32>] [-MinPasswordLength <UInt32>] [-PINHistoryCount <UInt64>] [-PINLifetime <UInt64>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **New-CsPinPolicy** per creare nuovi criteri PIN con valore Identity site:Redmond. In questo comando è incluso solo un parametro facoltativo, MinPasswordLength, che viene utilizzato per impostare la proprietà MinPasswordLength su 10. Tutte le altre proprietà dei criteri verranno configurate con i valori predefiniti.

    New-CsPinPolicy -Identity "site:Redmond" -MinPasswordLength 10

## ESEMPIO 2

Il comando mostrato nell'esempio 2 crea un nuovo criterio con il parametro Identity site:Redmond. In questo comando vengono utilizzati i parametri MinPasswordLength, PINHistory e PINLifetime per configurare esplicitamente tre valori di proprietà diversi per il nuovo criterio.

    New-CsPinPolicy -Identity "site:Redmond" -MinPasswordLength 10 -PINHistoryCount 10 -PINLifetime 30

## ESEMPIO 3

I comandi mostrati nell'esempio 3 illustrano come è possibile creare nuovi criteri PIN solo in memoria, modificare i valori delle proprietà per i criteri e quindi utilizzare il cmdlet **Set-CsPinPolicy** per trasformare i criteri presenti solo in memoria in criteri PIN effettivi. Nella prima riga dell'esempio vengono utilizzati il cmdlet **New-CsPinPolicy** e il parametro InMemory per creare criteri in memoria con valore Identity site:Redmond. Questi criteri vengono archiviati nella variabile $x. Se i criteri non fossero assegnati a una variabile, verrebbero creati solo in memoria e scomparirebbero subito dopo il completamento dell'esecuzione del comando.

Dopo aver assegnato i criteri virtuali alla variabile $x, i tre comandi successivi vengono utilizzati per modificare i valori delle proprietà per i criteri. Ad esempio, nella seconda riga il valore della proprietà MinPasswordLength viene impostato su 10. Dopo la configurazione di tutte le proprietà, viene utilizzato il cmdlet **Set-CsPinPolicy** per creare criteri effettivi con il valore Identity site:Redmond. A tale scopo, viene utilizzato il parametro Instance e fornita la variabile $x come valore del parametro. Dopo avere chiamato il cmdlet **Set-CsPinPolicy**, sarà possibile visualizzare i criteri e i valori delle relative proprietà utilizzando il cmdlet **Get-CsPinPolicy**.

    $x = New-CsPinPolicy -Identity "site:Redmond" -InMemory
    $x.MinPasswordLength = 10
    $x.PINHistoryCount = 10
    $x.PINLifetime = 30
    Set-CsPinPolicy -Instance $x

## ESEMPIO 4

I comandi dell'esempio 4 creano nuovi criteri PIN (site:Paris) che utilizzano uno dei valori delle proprietà presenti nei criteri esistenti site:Redmond. A tale scopo, nel primo comando viene utilizzato il cmdlet **Get-CsPinPolicy** per recuperare i criteri PIN site:Redmond. Le informazioni recuperate per tali criteri vengono quindi archiviate nella variabile $x.

Nel secondo comando viene utilizzato il cmdlet **New-CsPinPolicy** per creare i criteri site:Paris. Viene inoltre utilizzato il parametro MinPasswordLength per specificare il valore della proprietà MinPasswordLength. Anziché utilizzare un valore numerico hardcoded, il comando utilizza invece $x.MinPasswordLength come valore del parametro, indicando al cmdlet **New-CsPinPolicy** di impostare la lunghezza minima della password sul valore della proprietà MinPasswordLength presente nei criteri site:Redmond. Il risultato è che il valore della proprietà MinPasswordLength verrà copiato dai criteri esistenti site:Redmond ai nuovi criteri site:Paris.

    $x = Get-CsPinPolicy -Identity "site:Redmond"
    New-CsPinPolicy -Identity "site:Paris" -MinPasswordLength $x.MinPasswordLength 

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. Per accedere al sistema o partecipare a una conferenza, gli utenti in genere devono immettere un nome utente e una password. Tale operazione può tuttavia rappresentare un problema se si utilizza un telefono privo di tastiera alfanumerica. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché il nome utente e la password.

In Lync Server vengono utilizzati criteri per il PIN per gestire le proprietà di autenticazione tramite PIN. È pertanto possibile specificare la lunghezza minima di un codice PIN, nonché stabilire se consentire codici PIN che utilizzano modelli comuni, ad esempio cifre consecutive (come nel caso del codice PIN 123456). È possibile utilizzare il cmdlet **New-CsPinPolicy** per creare nuovi criteri di autenticazione tramite PIN configurabili nell'ambito del sito o nell'ambito per utente. Sebbene sia possibile definire anche un criterio PIN globale, non sarà possibile creare un secondo criterio PIN globale ma solo modificare il criterio globale esistente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsPinPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPinPolicy"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità univoca da assegnare al criterio. I criteri per il PIN possono essere creati in ambito sito o in ambito per utente. Per creare un criterio nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per creare un criterio nell'ambito per utente, utilizzare una sintassi simile alla seguente: -Identity RedmondPinPolicy.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCommonPatterns</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i modelli comuni sono consentiti o meno nei codici PIN. I modelli comuni includono cifre ripetute (222222), quattro o più cifre consecutive (123456) e codici PIN che corrispondono al numero di telefono o al numero di interno di un utente. Se questo parametro è impostato su True, i modelli comuni sono consentiti (ad esempio, il codice PIN 456789 che include cifre consecutive). Se è impostato su False, i modelli comuni non sono consentiti. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo esplicativo associato al criterio PIN. Ad esempio, il parametro Description potrebbe includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaximumLogonAttempts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero di errori di accesso consecutivi consentiti prima che il codice PIN di un utente venga bloccato automaticamente. Gli errori di accesso vengono conteggiati in due modi: come errori di accesso locali e come errori di accesso globali. Quando un utente tenta per la prima volta di eseguire l'accesso, inizia una nuova finestra di osservazione di 30 minuti. Ogni accesso non riuscito nel corso dei 30 minuti viene registrato come errore di accesso locale e come errore di accesso globale. Se durante i 30 minuti della finestra di osservazione l'utente raggiunge il valore impostato per MaximumLogonAttempts, verrà bloccato temporaneamente e non potrà accedere al sistema per un'ora. Durante tale intervallo non sarà autorizzato a eseguire l'accesso con l'autenticazione tramite PIN anche se fornisce il codice PIN corretto.</p>
<p>Allo scadere del periodo di blocco, il valore relativo ai tentativi di accesso locali dell'utente verrà reimpostato su 0, mentre il valore relativo ai tentativi di accesso globali resterà invariato. Se l'utente continua a sbagliare l'accesso, alla fine raggiungerà anche il numero massimo consentito di tentativi di accesso globali. A quel punto, il codice PIN verrà bloccato dal sistema e l'utente non potrà utilizzare l'autenticazione tramite PIN finché un amministratore non sbloccherà il codice.</p>
<p>Il numero massimo di tentativi di accesso consentiti inoltre varia in base alle dimensioni del codice PIN. Non viene pertanto visualizzato un valore predefinito per la proprietà MaximumLogonAttempts quando si esegue Get-CsPinPolicy. Per impostazione predefinita, un codice PIN con lunghezza pari a 4 consente agli utenti 10 tentativi di accesso locali e 100 tentativi di accesso globali. Un codice PIN con lunghezza pari a 5 consente 25 tentativi di accesso locali e 1000 tentativi di accesso globali, mentre i codici PIN con una lunghezza superiore a 6 consentono 25 tentativi locali e 5000 tentativi globali. Se si specifica un valore per la proprietà MaximumLogonAttempts, tale valore verrà utilizzato come numero massimo consentito di tentativi di accesso locali. Il valore relativo al numero di accessi globali invece non cambia, indipendentemente dal valore assegnato a MaximumLogonAttempts.</p>
<p>Ogni volta che un utente riesce ad accedere utilizzando l'autenticazione tramite PIN, il conteggio dei tentativi di accesso locali non riusciti viene reimpostato su 0. Il conteggio dei tentativi di accesso globali invece viene reimpostato solo quando un amministratore sblocca il codice PIN di un utente.</p>
<p>MaximumLogonAttempts può essere impostata su qualsiasi valore intero compreso tra 1 e 999 incluso. Non è tuttavia consigliabile modificare questa proprietà. Quando è impostata su un valore null (valore predefinito) Lync Server 2013 calcola automaticamente i criteri di blocco. In questo modo, in genere, viene offerta la massima sicurezza.</p></td>
</tr>
<tr class="even">
<td><p><em>MinPasswordLength</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La lunghezza minima consentita, ovvero il numero minimo di cifre in un codice PIN. Ad esempio, se MinPasswordLength è impostato su 8, il codice PIN 1259 verrà rifiutato perché contiene solo 4 cifre. I codici PIN devono essere costituiti da almeno 4 cifre e da un numero massimo di 24 cifre. Il valore predefinito è 5.</p></td>
</tr>
<tr class="odd">
<td><p><em>PINHistoryCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica la frequenza con cui gli utenti sono autorizzati a riutilizzare lo stesso codice PIN. Ad esempio, se PINHistoryCount è impostato su 3, le prime tre volte che l'utente reimposta il proprio codice PIN, deve utilizzare un nuovo codice. Alla quarta reimpostazione può riutilizzare il primo codice PIN utilizzato. Alla quinta reimpostazione può riutilizzare il secondo codice PIN e così via. Il conteggio della cronologia PIN può essere rappresentato da un qualsiasi numero intero incluso tra 0 e 20 (compresi); 0 significa che gli utenti possono utilizzare più volte lo stesso numero PIN. Per impostazione predefinita, PINHistoryCount è impostato su 0.</p>
<p>Se PINLifetime è impostato su un valore maggiore di 0, anche PINHistoryCount dovrà essere maggiore di 0. Ad esempio, non è possibile impostare PINLifetime su 30 e lasciare PINHistoryCount impostato su 0.</p></td>
</tr>
<tr class="even">
<td><p><em>PINLifetime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica il periodo di validità (in giorni) del PIN; alla scadenza, gli utenti devono selezionarne uno nuovo prima che venga consentita l'autenticazione del PIN come modalità di accesso al sistema. PINLifetime può essere impostato su un qualsiasi numero intero incluso tra 0 e 999 (compresi); 0 indica che i numeri PIN non hanno alcuna scadenza. Per impostazione predefinita, la durata del PIN è impostata su 0.</p>
<p>Se si imposta PINLifetime su un valore maggiore di 0, sarà necessario impostare anche PINHistoryCount su un valore maggiore di 0.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsPinPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Crea una nuova istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

