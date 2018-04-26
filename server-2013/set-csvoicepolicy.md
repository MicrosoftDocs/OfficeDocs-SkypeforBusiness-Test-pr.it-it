---
title: Set-CsVoicePolicy
TOCTitle: Set-CsVoicePolicy
ms:assetid: e6035b74-d760-4c48-aa0b-d09d129e0830
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399021(v=OCS.15)
ms:contentKeyID: 49302284
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio vocale esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene impostata la proprietà AllowSimulRing su False per il criterio per utente UserVoicePolicy2 in modo che qualsiasi utente a cui è assegnato questo criterio non sia abilitato per lo squillo simultaneo, una funzionalità che determina se è possibile impostare un secondo telefono (ad esempio un cellulare) affinché squilli ogni volta che squilla il telefono dell'ufficio dell'utente. Questo comando rimuove anche "Local" dall'elenco degli utilizzi PSTN per questo criterio. Il parametro Identity non è specificato in modo esplicito. Il parametro Identity è un parametro posizionale, pertanto se si inserisce il valore dell'identità al primo posto nell'elenco dei parametri non è necessario dichiarare esplicitamente che si tratta di Identity.

    Set-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{remove="Local"}

## ESEMPIO 2

Con questo esempio vengono modificati i criteri vocali per il sito Redmond in modo che tutti gli utilizzi PSTN definiti per l'organizzazione siano applicati a questi criteri. La prima riga dell'esempio chiama il cmdlet **Get-CsPstnUsage** per recuperare il set globale degli utilizzi PSTN per l'organizzazione e salvato questo set nella variabile $a. Con la seconda riga viene chiamato il cmdlet **Set-CsVoicePolicy** per modificare i criteri vocali per il sito Redmond. Al parametro PstnUsages viene passato un valore per sostituire l'elenco corrente di utilizzi per i criteri con l'elenco contenuto nel set globale di utilizzi PSTN. Si noti la sintassi del valore replace, $a.Usage, che fa riferimento alla proprietà Usage delle impostazioni di utilizzo PSTN, che contiene l'elenco di utilizzi PSTN.

    $a = Get-CsPstnUsage
    Set-CsVoicePolicy -Identity site:Redmond -PstnUsages @{replace=$a.Usage}

## Descrizione dettagliata

Questo cmdlet consente di modificare un criterio vocale esistente. I criteri vocali sono utilizzati per gestire funzionalità di VoIP aziendale quali, ad esempio, lo squillo simultaneo (vale a dire la capacità di far squillare un secondo telefono ogni volta che si riceve una chiamata sul telefono dell'ufficio) e l'inoltro di chiamata. Utilizzare questo cmdlet per modificare le impostazioni che abilitano o disabilitano molte di queste funzionalità.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsVoicePolicy** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicePolicy"}

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
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True, gli utenti a cui è assegnato il criterio potranno inoltrare le chiamate. Se questo parametro è impostato su False, le chiamate non possono essere inoltrate.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro è impostato su True, le chiamate effettuate ai numeri interni residenti in un altro pool verranno instradate attraverso la rete PSTN (Public Switched Telephone Network) nel caso in cui il pool o la rete WAN non sia disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Lo squillo simultaneo è una funzionalità che consente di far squillare più telefoni quando viene composto un singolo numero. Con l'impostazione del parametro su True viene abilitato lo squillo simultaneo. Se questo parametro è impostato su False, lo squillo simultaneo non può essere configurato per alcun utente assegnato a questo criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Consente agli amministratori di gestire l'inoltro di chiamata e lo squillo simultaneo. I valori consentiti sono:</p>
<p>* VoicePolicyUsage: inoltro di chiamata e squillo simultaneo su tutte le chiamate vengono gestiti mediante l'utilizzo dei criteri vocali predefiniti. Questo è il valore predefinito.</p>
<p>* InternalOnly: inoltro di chiamata e squillo simultaneo sono limitati alle chiamate effettuate da un utente Lync a un altro.</p>
<p>* CustomUsage: inoltro di chiamata e squillo simultaneo vengono gestiti mediante un utilizzo PSTN personalizzato. Questo utilizzo deve essere specificato mediante il parametro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Utilizzo PSTN personalizzato mediante cui si gestiscono inoltro di chiamata e squillo simultaneo. Per aggiungere un utilizzo personalizzato ai criteri vocali, utilizzare una sintassi analoga alla seguente:</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Per rimuovere un utilizzo personalizzato, utilizzare la sintassi seguente:</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Notare che l'utilizzo deve esistere prima di poter essere utilizzato con il parametro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Una descrizione del criterio vocale.</p>
<p>Lunghezza massima: 1040 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>È possibile impostare i criteri in modo che limitino la larghezza di banda e definiscano altre proprietà relative alla configurazione di rete. Se il parametro viene impostato su True è possibile sostituire questi criteri. In altri termini, se il parametro è impostato su True, non verranno eseguite verifiche sulla larghezza di banda e le chiamate verranno passate indipendentemente dalle impostazioni del servizio Controllo di ammissione di chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>applicazione Parcheggio di chiamata consente di mettere in attesa, o parcheggiare, una chiamata effettuata a un determinato numero all'interno di un gruppi di numeri, in modo da riprenderla successivamente. Con l'impostazione di questo parametro su True l'applicazione viene abilitata per gli utenti a cui è assegnato questo criterio. Se il parametro è impostato su False, gli utenti a cui è assegnato questo criterio non possono parcheggiare le chiamate effettuate verso il loro numero telefonico.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Determina se è possibile trasferire le chiamate a un altro numero. Se questo parametro è impostato su True, le chiamate possono essere trasferite; se il parametro è impostato su False, le chiamate non possono essere trasferite.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>La delega delle chiamate consente a un utente di rispondere alle chiamate di un altro utente oppure di effettuare chiamate per conto dell'altro utente. Ad esempio, un manager può impostare la delega delle chiamate in modo che tutte le chiamate in arrivo squillino sia sul suo telefono sia su quello di un amministratore. Se il parametro viene impostato su True, gli utenti con questo criterio possono configurare la delega delle chiamate. Con l'impostazione del parametro su False viene disabilitata la delega delle chiamate.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>La registrazione delle chiamate dannose è uno standard che consente di registrare le chiamate che un utente ha designato come dannose. Queste chiamate possono essere registrate anche se l'ID del chiamante è bloccato. La registrazione è disponibile solamente per le autorità, non per l'utente. Se questa proprietà è impostata su True, sarà possibile registrare le chiamate dannose.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Intercettazione team consente a un utente di designare un gruppo di altri utenti i cui telefoni squilleranno quando viene chiamato il numero di tale utente. Questa funzionalità è utile nei gruppi in cui, ad esempio, qualunque membro può rispondere alle chiamate in entrata provenienti dai clienti. Con l'impostazione del parametro su True viene abilitata questa funzionalità.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Quando è impostato su True, le chiamate senza risposta a un dispositivo mobile vengono instradate alla segreteria telefonica dell'organizzazione anziché alla segreteria telefonica del provider del dispositivo mobile. Se una chiamata ottiene una risposta &quot;troppo presto&quot;, ossia prima che che sia trascorso il valore configurato per la proprietà PSTNVoicemailEscapeTimer, si presuppone che il dispositivo mobile non sia disponibile e la chiamata viene instradata alla segreteria telefonica dell'organizzazione.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificatore univoco che specifica l'ambito, e in alcuni casi il nome, del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Questo oggetto deve essere di tipo VoicePolicy e può essere recuperato chiamando il cmdlet <strong>Get-CsVoicePolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Un nome descrittivo per questo criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>I numeri a tariffa PSTN sono più comunemente noti come numeri a tariffa interurbana. Le organizzazioni possono a volte bypassare questi numeri a tariffa implementando una soluzione VoIP (Voice over Internet Protocol) che permetta di connettere le succursali attraverso chiamate di rete. Se il parametro è impostato su True, le chiamate verranno inviate attraverso la rete PSTN e sarà necessario sostenere costi che potrebbero essere eliminati sfruttando la rete ed evitando i numeri a tariffa.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un elenco di utilizzi PSTN disponibili per questo criterio. L'utilizzo PSTN collega un criterio vocale a una route telefonica.</p>
<p>Qualsiasi valore stringa può essere collocato nell'elenco purché esistente nell'elenco globale corrente di utilizzi PSTN. Le stringhe duplicate non sono ammesse; tutte le stringhe devono essere univoche. Per recuperare gli utilizzi PSTN, è possibile richiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Ricordare che se si utilizza questo parametro per rimuovere tutti gli utilizzi PSTN dal criterio, gli utenti assegnati al criterio non saranno in grado di effettuare chiamate PSTN in uscita.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int64</p></td>
<td><p>Periodo di tempo (in millisecondi) utilizzato per determinare se una chiamata ha ottenuto una risposta &quot;troppo presto&quot;. Se una risposta viene ricevuta entro questo intervallo di tempo Lync Server presuppone che il dispositivo mobile non sia disponibile e passa automaticamente la chiamata alla segreteria telefonica dell'organizzazione. Se non viene ricevuta una risposta prima che sia trascorso l'intervallo di tempo, viene consentito alla chiamata di procedere.</p>
<p>Il valore predefinito è 1500.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui è necessario modificare i criteri vocali, ad esempio:</p>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Accetta l'input da pipeline di oggetti criterio vocale.

## Tipi restituiti

Questo cmdlet non restituisce un valore o un oggetto. Configura piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

