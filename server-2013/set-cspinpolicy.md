---
title: Set-CsPinPolicy
TOCTitle: Set-CsPinPolicy
ms:assetid: f0e1afb9-4c71-45c5-8093-6cd12db3d697
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412997(v=OCS.15)
ms:contentKeyID: 49302415
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPinPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica uno o più criteri PIN client esistenti. L'autenticazione tramite PIN consente agli utenti di accedere a Lync Server immettendo il proprio PIN anziché il nome utente e la password. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsPinPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPinPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCommonPatterns <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaximumLogonAttempts <UInt32>] [-MinPasswordLength <UInt32>] [-PINHistoryCount <UInt64>] [-PINLifetime <UInt64>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene modificato il criterio PIN assegnato al sito Redmond. In questo caso, il comando imposta su 10 il valore della proprietà MinPasswordLength. I nuovi codici PIN dovranno pertanto contenere almeno 10 cifre.

    Set-CsPinPolicy -Identity site:Redmond -MinPasswordLength 10

## ESEMPIO 2

Nell'esempio 2 vengono modificate due proprietà del criterio PIN per utente con valore Identity RedmondUsersPinPolicy, ovvero viene modificato il valore delle proprietà MinPasswordLength e AllowCommonPatterns.

    Set-CsPinPolicy -Identity RedmondUsersPinPolicy -MinPasswordLength 10 -AllowCommonPatterns $True

## ESEMPIO 3

Il comando mostrato nell'esempio 3 consente di modificare il valore di MinPasswordLength per tutti i criteri per il PIN configurati per l'utilizzo nell'organizzazione. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPinPolicy** senza alcun parametro per recuperare una raccolta di tutti i criteri per il PIN esistenti. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPinPolicy**, che modifica il valore della proprietà MinPasswordLength per ogni criterio della raccolta.

    Get-CsPinPolicy | Set-CsPinPolicy -MinPasswordLength 10

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. In genere, l'accesso al sistema o la partecipazione a una conferenza richiedono l'immissione del nome utente e della password. Tale operazione può rappresentare un problema se si utilizza un telefono privo di tastierino alfanumerico. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché il nome utente e la password.

In Lync Server vengono utilizzati criteri per il PIN per gestire le proprietà di autenticazione tramite PIN. È pertanto possibile specificare la lunghezza minima di un codice PIN, nonché stabilire se consentire codici PIN che utilizzano modelli comuni, ad esempio cifre consecutive (come nel caso del codice PIN 123456). I criteri per il PIN possono essere configurati nell'ambito globale, nell'ambito del sito e nell'ambito per utente. Per modificare i valori delle proprietà di uno qualsiasi di questi criteri, è possibile utilizzare il cmdlet **Set-CsPinPolicy**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsPinPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPinPolicy"}

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
<td><p><em>AllowCommonPatterns</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i modelli comuni sono consentiti o meno nei codici PIN. I formati comuni includono la ripetizione delle cifre (225577), 4 o più cifre consecutive (991234) e i PIN che corrispondono al numero di telefono o al numero di interno di un utente. Se questo parametro è impostato su True, i modelli comuni sono consentiti (ad esempio, il codice PIN 123456 che include cifre consecutive). Se è impostato su False, i modelli comuni non sono consentiti. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo aggiuntivo associato al criterio PIN. Ad esempio, il parametro Description potrebbe includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco assegnato al criterio al momento della relativa creazione. È possibile assegnare i criteri per il PIN con ambito globale, nell'ambito del sito o nell'ambito per utente. Per fare riferimento all'istanza globale, utilizzare la seguente sintassi: -Identity global. Per fare riferimento a un criterio nell'ambito del sito, utilizzare una sintassi analoga alla seguente: -Identity site:Redmond. Per fare riferimento a un criterio per utente, utilizzare una sintassi analoga alla seguente: -Identity RedmondPinPolicy.</p>
<p>Se il parametro Identity non viene specificato, il cmdlet <strong>Set-CsPinPolicy</strong> modificherà il criterio globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto UserPinPolicy</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaximumLogonAttempts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero di errori di accesso consecutivi consentiti prima che il codice PIN di un utente venga bloccato automaticamente. Gli errori di accesso vengono conteggiati in due modi: come errori di accesso locali e come errori di accesso globali. Quando un utente tenta per la prima volta di eseguire l'accesso, inizia una nuova finestra di osservazione di 30 minuti. Ogni accesso non riuscito nel corso dei 30 minuti viene registrato come errore di accesso locale e come errore di accesso globale. Se durante i 30 minuti della finestra di osservazione l'utente raggiunge il valore impostato per MaximumLogonAttempts, verrà bloccato temporaneamente e non potrà accedere al sistema per un'ora. Durante tale intervallo non sarà autorizzato a eseguire l'accesso con l'autenticazione tramite PIN anche se fornisce il codice PIN corretto.</p>
<p>Allo scadere del periodo di blocco, il valore relativo ai tentativi di accesso locali dell'utente verrà reimpostato su 0, mentre il valore relativo ai tentativi di accesso globali resterà invariato. Se l'utente continua a sbagliare l'accesso, alla fine raggiungerà anche il numero massimo consentito di tentativi di accesso globali. A quel punto, il codice PIN verrà bloccato dal sistema e l'utente non potrà utilizzare l'autenticazione tramite PIN finché un amministratore non sbloccherà il codice.</p>
<p>Il numero massimo di tentativi di accesso consentiti inoltre varia in base alle dimensioni del codice PIN. Non viene pertanto visualizzato un valore predefinito per la proprietà MaximumLogonAttempts quando si esegue il cmdlet <strong>Get-CsPinPolicy</strong>. Per impostazione predefinita, un codice PIN con lunghezza pari a 4 consente agli utenti 10 tentativi di accesso locali e 100 tentativi di accesso globali. Un codice PIN con lunghezza pari a 5 consente 25 tentativi di accesso locali e 1000 tentativi di accesso globali, mentre i codici PIN con una lunghezza superiore a 6 consentono 25 tentativi locali e 5000 tentativi globali. Se si specifica un valore per la proprietà MaximumLogonAttempts, tale valore verrà utilizzato come numero massimo consentito di tentativi di accesso locali. Il valore relativo al numero di accessi globali invece non cambia, indipendentemente dal valore assegnato a MaximumLogonAttempts.</p>
<p>Ogni volta che un utente riesce ad accedere utilizzando l'autenticazione tramite PIN, il conteggio dei tentativi di accesso locali non riusciti viene reimpostato su 0. Il conteggio dei tentativi di accesso globali invece viene reimpostato solo quando un amministratore sblocca il codice PIN di un utente.</p>
<p>MaximumLogonAttempts può essere impostata su qualsiasi valore intero compreso tra 1 e 999 incluso. Non è tuttavia consigliabile modificare questa proprietà. Quando è impostata su un valore null (valore predefinito) Lync Server 2013 calcola automaticamente i criteri di blocco. In questo modo, in genere, viene offerto il massimo livello di sicurezza.</p></td>
</tr>
<tr class="even">
<td><p><em>MinPasswordLength</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La lunghezza minima consentita (ovvero il numero minimo di cifre) in un numero PIN. Ad esempio, se MinPasswordLength è impostato su 8, il codice PIN 1259 verrà rifiutato perché contiene solo 4 cifre. I codici PIN devono essere costituiti da almeno 4 cifre e da un numero massimo di 24 cifre. Il valore predefinito è 5.</p></td>
</tr>
<tr class="odd">
<td><p><em>PINHistoryCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica la frequenza con cui gli utenti sono autorizzati a riutilizzare lo stesso codice PIN. Ad esempio, se PINHistoryCount è impostato su 3, le prime tre volte in cui reimpostano i propri codici PIN, gli utenti dovranno utilizzare un nuovo codice. Alla quarta reimpostazione, potranno riutilizzare il primo codice PIN utilizzato. Alla quinta reimpostazione, potranno riutilizzare il secondo codice PIN e così via. Il conteggio della cronologia PIN può essere rappresentato da un qualsiasi numero intero compreso tra 0 e 20 inclusi. 0 significa che gli utenti possono utilizzare più volte lo stesso codice PIN. Per impostazione predefinita, PINHistoryCount è configurato su 0.</p>
<p>Se PINLifetime è impostato su un valore maggiore di 0, anche PINHistoryCount dovrà essere maggiore di 0. Ad esempio, non è possibile impostare PINLifetime su 30 e lasciare PINHistoryCount impostato su 0.</p></td>
</tr>
<tr class="even">
<td><p><em>PINLifetime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica il periodo di validità (in giorni) del codice PIN. Alla scadenza, gli utenti devono selezionarne uno nuovo prima che possano eseguire l'autenticazione tramite PIN per accedere al sistema. PINLifetime può essere impostato su qualsiasi numero intero compreso tra 0 e 999 inclusi. 0 indica che i codici PIN non hanno alcuna scadenza. Per impostazione predefinita, la durata del PIN è impostata su 0.</p>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy. Il cmdlet **Set-CsPinPolicy** accetta l'input da pipeline dell'oggetto criterio PIN.

## Tipi restituiti

Il cmdlet **Set-CsPinPolicy** non restituisce un valore o un oggetto. Il cmdlet piuttosto configura una o più istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)

