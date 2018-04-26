---
title: New-CsVoicePolicy
TOCTitle: New-CsVoicePolicy
ms:assetid: 3852de89-a604-437a-9fdf-3597b88ce13d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425856(v=OCS.15)
ms:contentKeyID: 49300203
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio vocale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsVoicePolicy -Identity <XdsIdentity> [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creato un nuovo criterio vocale per utente con le impostazioni predefinite e con identità (Identity) UserVoicePolicy1.

    New-CsVoicePolicy -Identity UserVoicePolicy1

## ESEMPIO 2

Con questo esempio viene creato un nuovo criterio vocale per utente con identità UserVoicePolicy2; la proprietà AllowSimulRing viene impostata su False, in modo che qualsiasi utente a cui è assegnato questo criterio non sia abilitato per lo squillo simultaneo, una funzionalità che determina se è possibile impostare un secondo telefono (ad esempio un cellulare) affinché squilli ogni volta che squilla il telefono dell'ufficio dell'utente. Questo comando, inoltre, consente di aggiungere "Local" all'elenco degli utilizzi PSTN per associare questo criterio vocale a una route vocale che impiega l'utilizzo PSTN Local. Il parametro Identity non è specificato in modo esplicito. Il parametro Identity è un parametro posizionale, pertanto se si inserisce il valore dell'identità al primo posto nell'elenco dei parametri non è necessario dichiarare esplicitamente che si tratta di Identity.

    New-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{add = "Local"}

## ESEMPIO 3

In questo esempio viene creato un nuovo criterio vocale per il sito Redmond e al criterio vengono applicati tutti gli utilizzi PSTN definiti per l'organizzazione. Nella prima riga dell'esempio viene chiamato il cmdlet **Get-CsPstnUsage** per recuperare il set globale di utilizzi PSTN per l'organizzazione e salvarlo nella variabile $a. Nella seconda riga viene chiamato il cmdlet **New-CsVoicePolicy** per creare il nuovo criterio vocale per il sito Redmond. Al parametro PstnUsages viene passato un valore per aggiungere al criterio l'elenco contenuto nel set globale di utilizzi PSTN. Si noti la sintassi del valore di aggiunta, $a.Usage. Fa riferimento alla proprietà Usage delle impostazioni di utilizzo PSTN, che contiene l'elenco di utilizzi PSTN.

    $a = Get-CsPstnUsage
    New-CsVoicePolicy site:Redmond -PstnUsages @{add = $a.Usage}

## Descrizione dettagliata

Questo cmdlet consente di creare un nuovo criterio vocale. I criteri vocali sono utilizzati per gestire funzionalità di VoIP aziendale quali, ad esempio, lo squillo simultaneo (vale a dire la capacità di far squillare un secondo telefono ogni volta che si riceve una chiamata sul telefono dell'ufficio) e l'inoltro di chiamata. Il criterio creato da questo cmdlet determina se molte di queste funzionalità sono abilitate o disabilitate.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsVoicePolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicePolicy"}

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
<td><p>XdsIdentity</p></td>
<td><p>Identificatore univoco che specifica l'ambito o il nome del criterio. I valori validi per questo cmdlet sono site:&lt;nome sito&gt;, dove &lt;nome sito&gt; corrisponde al nome del sito di Lync Server a cui si applica il criterio, ad esempio site:Redmond, e una stringa che designa un criterio per utente, ad esempio RedmondVoicePolicy. Per impostazione predefinita, è presente un criterio globale.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True, le chiamate possono essere inoltrate. Se questo parametro è impostato su False, le chiamate non possono essere inoltrate.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True, le chiamate effettuate ai numeri interni residenti su un altro pool saranno instradate attraverso la rete PSTN (Public Switched Telephone Network) nel caso in cui il pool o la WAN non sia disponibile.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Lo squillo simultaneo è una funzionalità che consente di far squillare più telefoni quando viene composto un singolo numero. Con l'impostazione del parametro su True viene abilitata questa funzionalità. Se questo parametro è impostato su False, lo squillo simultaneo non può essere configurato per alcun utente a cui è assegnato questo criterio.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Consente agli amministratori di gestire l'inoltro di chiamata e lo squillo simultaneo. I valori consentiti sono:</p>
<p>* VoicePolicyUsage: per tutte le chiamate viene utilizzato il criterio vocale predefinito per gestire l'inoltro di chiamate lo squillo simultaneo. Questo è il valore predefinito.</p>
<p>* InternalOnly: l'inoltro di chiamata e lo squillo simultaneo vengono applicati solo alle chiamate tra utenti di Lync.</p>
<p>* CustomUsage: per la gestione dell'inoltro di chiamata e dello squillo simultaneo verrà applicato un utilizzo PSTN personalizzato. Questo utilizzo deve essere specificato tramite il parametro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Utilizzo PSTN personalizzato applicato per la gestione dell'inoltro di chiamata e lo squillo simultaneo. Per aggiungere un utilizzo personalizzato al criterio vocale, utilizzare una sintassi simile alla seguente:</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Per rimuovere un utilizzo personalizzato, utilizzare la sintassi seguente:</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Si noti che è possibile specificare per il parametro CustomCallForwardingSimulRingUsages solo un utilizzo già esistente.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Una descrizione del criterio vocale.</p>
<p>Lunghezza massima: 1040 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>I criteri possono essere impostati per gestire la configurazione della rete, compresa la limitazione della larghezza di banda. Se il parametro viene impostato su True è possibile sostituire questi criteri. In altri termini, se il parametro è impostato su True, non verranno eseguite verifiche sulla larghezza di banda e le chiamate verranno passate indipendentemente dalle impostazioni del servizio Controllo di ammissione di chiamata.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>applicazione Parcheggio di chiamata consente di mettere in attesa, o parcheggiare, una chiamata effettuata a un determinato numero all'interno di un gruppi di numeri, in modo da riprenderla successivamente. Con l'impostazione del parametro su True viene abilitata l'applicazione. Se il parametro è impostato su False, gli utenti a cui è assegnato questo criterio non possono parcheggiare le chiamate effettuate verso il loro numero telefonico.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Determina se è possibile trasferire le chiamate a un altro numero. Se questo parametro è impostato su True, le chiamate possono essere trasferite; se il parametro è impostato su False, le chiamate non possono essere trasferite.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>La delega delle chiamate consente a un utente di rispondere alle chiamate di un altro utente oppure di effettuare chiamate per conto dell'altro utente. Ad esempio, un manager può impostare la delega delle chiamate in modo che tutte le chiamate in arrivo squillino sia sul suo telefono sia su quello di un amministratore. Se il parametro viene impostato su True, gli utenti con questo criterio possono configurare la delega delle chiamate. Con l'impostazione del parametro su False viene disabilitata la delega delle chiamate.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>La registrazione delle chiamate dannose è uno standard che consente di registrare le chiamate che un utente ha designato come dannose. Queste chiamate possono essere registrate anche se l'ID del chiamante è bloccato. La registrazione è disponibile solo per le autorità preposte, non per l'utente. Se questa proprietà è impostata su True, sarà possibile registrare le chiamate dannose.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Intercettazione team consente a un utente di designare un gruppo di altri utenti i cui telefoni squilleranno quando viene chiamato il numero di tale utente. Questa funzionalità è utile nei gruppi in cui, ad esempio, qualunque membro può rispondere alle chiamate in entrata provenienti dai clienti. Con l'impostazione del parametro su True viene abilitata questa funzionalità.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se si imposta questo parametro su True, le chiamate a un dispositivo mobile senza risposta verranno instradate alla segreteria telefonica dell'organizzazione anziché alla segreteria telefonica del provider del dispositivo mobile. Se una chiamata riceve una risposta &quot;troppo presto&quot; (ovvero prima che sia trascorso l'intervallo di tempo specificato con la proprietà PSTNVoicemailEscapeTimer), si presupporrà che il dispositivo mobile non sia disponibile e la chiamata verrà instradata alla segreteria telefonica dell'organizzazione.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Nome visualizzabile per questo criterio.</p>
<p>Valore predefinito: DefaultPolicy</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>I numeri a tariffa PSTN sono più comunemente noti come numeri a tariffa interurbana. Le organizzazioni possono talvolta aggirare l'utilizzo di questi numeri a tariffa implementando una soluzione VoIP (Voice over Internet Protocol) che permetta di connettere le succursali attraverso chiamate di rete. Se il parametro è impostato su True, le chiamate saranno inviate tramite PSTN e sarà necessario sostenere i costi relativi, che potrebbero essere eliminati utilizzando la rete per evitare i numeri a tariffa.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un elenco di utilizzi PSTN disponibili per questo criterio. L'utilizzo PSTN collega un criterio vocale a una route telefonica.</p>
<p>Qualsiasi valore stringa può essere collocato nell'elenco purché esistente nell'elenco globale corrente di utilizzi PSTN. Le stringhe duplicate non sono ammesse; tutte le stringhe devono essere univoche. Per recuperare gli utilizzi PSTN, è possibile richiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Per impostazione predefinita, questo elenco è vuoto. Se non viene fornito un valore per questo parametro, viene visualizzato un messaggio di avviso che indica che gli utenti a cui viene assegnato questo criterio non potranno effettuare chiamate PSTN esterne.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int64</p></td>
<td><p>Tempo (in millisecondi) utilizzato per determinare se una chiamata ha ricevuto una risposta &quot;troppo presto&quot;. Se si riceve una risposta entro l'intervallo di tempo specificato, in Lync Server si presupporrà che il dispositivo mobile non sia disponibile e la chiamata verrà trasferita automaticamente alla segreteria telefonica dell'organizzazione. Se non si riceve alcuna risposta prima della scadenza dell'intervallo di tempo, la chiamata potrà procedere. Il valore predefinito è 1500 millisecondi.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per cui viene creato il nuovo criterio vocale. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceDeploymentMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>VoiceDeploymentMode</p></td>
<td><p>I valori consentiti sono:</p>
<p>* OnPrem</p>
<p>* Online</p>
<p>* OnlineBasic</p>
<p>* OnPremOnlineHybrid</p>
<p>Il valore predefinito è OnPrem.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet consente di creare un'istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy.

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

