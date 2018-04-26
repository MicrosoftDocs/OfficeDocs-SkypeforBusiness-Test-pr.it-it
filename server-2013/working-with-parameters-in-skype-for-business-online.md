---
title: Uso di parametri
TOCTitle: Uso di parametri
ms:assetid: 29ebda0f-ae5f-4512-ad59-240c3605b240
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362778(v=OCS.15)
ms:contentKeyID: 56269894
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso di parametri

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Quando si usa il parametro Identity, si noterà probabilmente che il valore del parametro kenmyer@litwareinc.com è racchiuso tra virgolette doppie:

    -Identity "kenmyer@litwareinc.com"

Una delle domande che le persone che non hanno familiarità con Windows PowerShell pongono invariabilmente è: perché usare le virgolette doppie e quando vanno usate. Non esiste una risposta semplice a questa domanda, ma ci sono alcune regole generali da seguire:

  - Le virgolette doppie non sono di solito necessarie quando il valore del parametro è un numero. Ad esempio, per limitare il numero di utenti restituito dal cmdlet [Get-CsOnlineUser](get-csonlineuser.md), usare questa sintassi:
    
        -ResultSize 100
    
    In effetti, non bisogna mai racchiudere un numero tra virgolette doppi, perché in tal caso Windows PowerShell potrebbe non riuscire a interpretare correttamente il valore come numero.
    
    In modo analogo, non includere mai virgole in un numero. Per impostare ad esempio la dimensione del risultato su 10000,00, questa sintassi non sarebbe corretta:
    
        -ResultSize 10000,00
    
    Verrà infatti generato un errore perché Windows PowerShell usa la virgola per separare i valori degli argomenti. In questo caso, Windows PowerShell interpreterà la sintassi come se venissero passati due valori del parametro distinti: 10000 e 00. Non essendo possibile impostare la dimensione di un risultato contemporaneamente su 10000 e su 0, verrà generato un errore. Usare invece questa sintassi senza virgole:
    
        -ResultSize 10000

  - Le virgolette doppie non sono di solito necessarie anche quando il valore del parametro è una data.
    
        -StartDate 6/1/2013
    
    Questa sintassi è tuttavia valida solo quando non è inclusa l'ora. Se si include l'ora, essendo necessario inserire uno spazio vuoto tra la data e l'ora, il valore del parametro deve essere racchiuso tra virgolette doppie:
    
        -StartDate "6/1/2013 10:00AM"
    
    Si tenga presente che il comando precedente è formattato per i computer che usano la lingua inglese (Stati Uniti) nelle opzioni internazionali. Se non si usa l'inglese (Stati Uniti), formattare date e ore in base alle impostazioni del computer. Per verificare le opzioni internazionali usate da Windows PowerShell, eseguire questo comando al prompt dei comandi di Windows PowerShell:
    
        Get-Host | Select-Object CurrentUICulture

  - I valori stringa, ad esempio il nome di una persona, non richiedono in genere le virgolette doppie. Le principali eccezioni riguardano i casi in cui il valore stringa include caratteri con restrizioni, come uno spazio vuoto, una virgola o altri segni di punteggiatura. Questa sintassi funziona ad esempio perché l'identità dell'utente non include alcun carattere con restrizioni:
    
        -Identity "kenmyer@litwareinc.com"
    
    Questo comando invece avrà esito negativo perché Identity include uno spazio vuoto:
    
        -Identity Ken Myer
    
    Il comando precedente non riesce perché Windows PowerShell usa gli spazi vuoti per separare singoli parametri. Pertanto Windows PowerShell interpreta Ken come parametro di Identity e Myer come un nuovo parametro, restituendo pertanto il messaggio di errore seguente:
    
        Get-CsOnlineUser : Impossibile trovare un parametro posizionale che accetta l'argomento 'Myer'.
    
    Per usare un valore del parametro che include uno spazio vuoto, oppure una virgola o qualsiasi altro carattere con restrizioni, racchiudere il valore tra virgolette doppie:
    
        -Identity "Ken Myer"
    
    Nella maggior parte dei casi Windows PowerShell consente di usare virgolette singole anziché quelle doppie. Ad esempio, questa è una sintassi di Windows PowerShell valida:
    
        -Identity 'Ken Myer'
    
    Si noti tuttavia che è necessario usare lo stesso tipo di virgolette all'inizio e alla fine della stringa. Questa sintassi di Windows PowerShell non è valida:
    
        -Identity "Ken Myer'
    
    Se si tenta di eseguire questo comando, nella console di Windows PowerShell verrà visualizzato quanto segue:
    
    ``` 
    >>
    ```
    
    La freccia doppia è un modo per richiedere di completare il comando: avendo iniziato con le virgolette doppie, Windows PowerShell prevede l'uso di virgolette doppie di chiusura. Se viene visualizzato \>\>, premere CTRL+C per annullare il comando e quindi riprovare.

  - Le virgolette doppie non devono essere usate con i valori booleani (True/False). Si noti inoltre che per specificare i valori True/False, è necessario usare le variabili di Windows PowerShell $True e $False. Ad esempio:
    
        -EnterpriseVoiceEnabled $True

Ci sono inoltre parametri di Windows PowerShell noti come *parametri opzionali* che non accettano valori di parametro:

    -WhatIf

Non solo i valori di parametro non sono richiesti quando si usa un parametro opzionale, ma se ne viene incluso, viene generato un errore. Se si tenta ad esempio di eseguire questo comando:

    -WhatIf $True

avrà esito negativo e verrà visualizzato un messaggio di errore simile al seguente:

    Set-CsUserAcp: Impossibile trovare un parametro posizionale che accetta l'argomento 'True'.

Per gestire Skype for Business online tramite Windows PowerShell è necessario conoscere quali cmdlet si possono usare. È inoltre necessario sapere quali parametri sono disponibili per ogni cmdlet e il *tipo di dati* di ogni parametro, ovvero se il parametro accetta un valore data, un valore stringa, un numero e così via. Queste informazioni, unitamente a numerosi esempi sull'uso dei cmdlet, sono disponibili negli argomenti della Guida dei cmdlet di Skype for Business online. Ad esempio, questi sono i parametri che è possibile usare con il cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md):

![Parametri per un cmdlet specifico di PowerShell](images/Dn362778.ead7add1-eec3-4fa4-8bbe-9aa72bb7a1ae(OCS.15).png "Parametri per un cmdlet specifico di PowerShell")

Come si può vedere, la tabella dei parametri include una descrizione del cmdlet, indica se il parametro è richiesto (obbligatorio) o facoltativo e il tipo di dati per ogni parametro. Si noti che il tipo di dati descritto nella tabella è quello ufficiale usato da .NET Framework. Il tipo di dati è pertanto indicato come System.Management.Automation.SwitchParameter anziché solo come Parametro opzionale. Ecco una guida rapida dei tipi di dati più comunemente usati dai cmdlet di Skype for Business online:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Valore stringa che rappresenta l'identità di un utente. Corrisponde di solito all'indirizzo UPN o SIP dell'utente:</p>
<pre><code>-Identity &quot;kenmyer@litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN è un nome di dominio completo, ad esempio:</p>
<pre><code>-Fqdn &quot;atl-lync-001.litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Boolean</p></td>
<td><p>Un valore booleano è un valore True/False. È necessario usare le variabili di Windows PowerShell $True e $False quando si specificano valori booleani:</p>
<pre><code>-Enabled $True -EnterpriseVoiceEnabled $False</code></pre></td>
</tr>
<tr class="even">
<td><p>System.Guid</p></td>
<td><p>GUID è l'acronimo di <em>Globally Unique Identifier</em>, ovvero un identificatore univoco globale che in Skype for Business online viene assegnato a ogni tenant di Skype for Business online. Ad esempio:</p>
<pre><code>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</code></pre>
<p>È possibile recuperare il GUID assegnato ai tenant di Skype for Business online tramite il comando:</p>
<pre><code>Get-CsTenant | Select-Object TenantId</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>I parametri opzionali sono così definiti perché vengono attivati, diversamente sono disattivati. Se il parametro è presente, è per così dire attivato, se non è presente è disattivato. Per usare ad esempio il parametro Confirm per richiedere la conferma prima di eseguire un comando, includerlo senza valori di parametro come parte del comando. Ad esempio:</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot; -Confirm</code></pre>
<p>Se non si vuole richiedere conferma, non includere il parametro Confirm:</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>System.String</p></td>
<td><p>Un valore stringa è un valore alfanumerico che, in generale, può contenere qualsiasi carattere digitabile sulla tastiera, ad esempio:</p>
<pre><code>-Password &quot;abc123%&amp;*&quot;</code></pre>
<p>È consigliabile racchiudere i valori stringa tra virgolette doppie. Non è sempre obbligatorio, ma lo è se il valore stringa contiene uno spazio vuoto o una virgola oppure se è una parola chiave riservata di Windows PowerShell. Una parola chiave è un comando o un altro elemento che fa parte dello stesso linguaggio di Windows PowerShell. Ad esempio, “If” e “End” sono entrambe parole chiave di Windows PowerShell. Per altre informazioni, digitare il comando seguente al prompt dei comandi di Windows PowerShell:</p>
<p>Get-Help about_Reserved_Words</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Introduzione a Windows PowerShell e Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

