---
title: 'Lync Server 2013: Requisiti di resilienza dei siti di succursale'
TOCTitle: Requisiti di resilienza dei siti di succursale
ms:assetid: a570922c-52bd-42d7-bd64-226578b3d110
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412772(v=OCS.15)
ms:contentKeyID: 49301549
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di resilienza dei siti di succursale per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento vengono fornite informazioni utili per preparare gli utenti per la resilienza dei siti di succursale e per il funzionamento continuato (survivability) della segreteria telefonica e vengono specificati i requisiti hardware e software pertinenti.

## Preparazione degli utenti di succursale per la resilienza del sito di succursale

Per preparare gli utenti per la resilienza del sito di succursale, impostare il pool di registrazione corrispondente come Survivable Branch Appliance (SBA) o Survivable Branch Server.

## Assegnazioni di registrazione per utenti di succursale

Indipendentemente dalla soluzione di resilienza del sito di succursale scelta, è necessario assegnare una funzione di registrazione principale a ogni utente. Gli utenti del sito di succursale devono sempre registrarsi nella funzione di registrazione presso il sito di succursale, indipendentemente dal fatto che tale funzione si trovi nel Survivable Branch Appliance, nel Survivable Branch Server o in un server Lync Server 2013 Standard o Server Enterprise Edition autonomo. Per consentire ai client del sito di succursale di individuare il pool di registrazione di backup corrispondente quando il Survivable Branch Appliance non è disponibile, è necessario un record di risorse servizi (SRV) DNS (Domain Name System).

Se un sito di succursale non dispone di un server DNS, per l'individuazione del Survivable Branch Appliance o del Survivable Branch Server esistono due modalità di configurazione alternative:

  - Configurazione dell'opzione DHCP 120 nel server DHCP (Dynamic Host Configuration Protocol) del sito di succursale in modo che faccia riferimento al nome di dominio completo (FQDN) del Survivable Branch Appliance o del Survivable Branch Server.

  - Configurazione del Survivable Branch Appliance o del Survivable Branch Server in modo che risponda alle query DHCP 120.

## Routing vocale per gli utenti di succursale

Per gli utenti di un sito di succursale è consigliabile creare criteri VoIP (Voice over Internet Protocol) a livello di utente separati. Tali criteri dovrebbero includere una route principale che utilizzi il gateway del server di succursale o del Survivable Branch Appliance e una o più route di backup che utilizzino un trunk con un gateway PSTN (Public Switched Telephone Network) presso il sito centrale. Se la route principale non è disponibile, viene sostituita dalla route di backup, che può utilizzare uno o più gateway del sito centrale. In questo modo, non è rilevante se l'utente è registrato presso la funzione di registrazione del sito di succursale o presso il pool di registrazione di backup nel sito centrale: i criteri VoIP dell'utente saranno sempre attivi. Questa considerazione è particolarmente importante per gli scenari di failover. Se ad esempio per connettersi a un pool di registrazione di backup presso il sito centrale è necessario rinominare il Survivable Branch Appliance o riconfigurare il Survivable Branch Appliance, è necessario spostare gli utenti del sito di succursale nel sito centrale per tutta la durata del periodo di utilizzo del backup. Per i dettagli sulla ridenominazione o la riconfigurazione di un Survivable Branch Appliance, vedere l'[Appendice B: gestione di un Survivable Branch Appliance in Lync Server 2013](lync-server-2013-appendix-b-managing-a-survivable-branch-appliance.md) nella documentazione relativa alla distribuzione. Se tali utenti non dispongono di criteri VoIP o di dial plan a livello di utente, per impostazione predefinita al momento dello spostamento in un altro sito vengono applicati i criteri VoIP e i dial plan a livello di sito del sito centrale, anziché quelli del sito di succursale. In questo scenario le chiamate degli utenti del sito di succursale avranno esito positivo se a tali utenti non è possibile applicare i criteri VoIP e i dial plan a livello di sito utilizzati dal pool di registrazione di backup. Se ad esempio gli utenti di un sito di succursale situato in Giappone vengono spostati in un sito centrale situato a Redmond, è improbabile che un dial plan con regole di normalizzazione che antepongono il prefisso +1425 a tutte le chiamate a numeri di sette cifre sia in grado di convertire correttamente le chiamate di tali utenti.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Quando si crea una route di backup per una succursale, è consigliabile aggiungere ai criteri utente della succursale due record di utilizzo telefono PSTN e assegnare route distinte a ognuno. La prima route, principale, dovrà instradare le chiamate al gateway associato all'SBA ( Survivable Branch Appliance) o al server di succursale, mentre la seconda route, di backup, dovrà instradare le chiamate al gateway presso il sito centrale. Per l'indirizzamento delle chiamate, l'SBA o il server di succursale dovrà tentare tutte le route assegnate al primo record di utilizzo PSTN prima di tentare quelle del secondo record di utilizzo.</td>
</tr>
</tbody>
</table>


Per garantire che le chiamate in arrivo per gli utenti del sito di succursale raggiungano gli utenti a cui sono destinate in caso di indisponibilità del gateway di succursale o del componente Windows del sito del Survivable Branch Appliance (come avviene ad esempio quando il gateway di succursale o del Survivable Branch Appliance viene disattivato per manutenzione), reindirizzare le chiamate in arrivo al pool di registrazione di backup presso il sito centrale creando una route di failover sul gateway o utilizzando il provider DID (Direct Inward Dialing). Dal pool di registrazione di backup del sito centrale le chiamate verranno instradate agli utenti di succursale attraverso il collegamento WAN. Verificare che la route sia in grado di convertire i numeri nei formati di numero di telefono consentiti per il gateway PSTN o un altro trunk peer. Per informazioni dettagliate sulla creazione di una route di failover, vedere [Configurazione di una route di failover in Lync Server 2013](lync-server-2013-configuring-a-failover-route.md). Per consentire la normalizzazione delle chiamate in arrivo da parte del trunk associato al gateway del sito di succursale, è inoltre necessario creare dial plan a livello di servizio. Se presso un sito di succursale sono presenti due Survivable Branch Appliance, è possibile creare un dial plan a livello di sito per entrambi, a meno che non sia necessario utilizzare un dial plan a livello di servizio distinto per ognuno.


> [!NOTE]
> Per tenere conto del consumo delle risorse del sito centrale da parte degli utenti dei siti di succursale che si appoggiano al sito centrale per le funzionalità di presenza, conferenza o failover, è consigliabile considerare ogni utente del sito di succursale come se fosse registrato presso il sito centrale. Attualmente il numero di utenti del sito di succursale, inclusi gli utenti registrati in un Survivable Branch Appliance, è illimitato.



È inoltre consigliabile creare criteri vocali e di dial plan a livello di utente e quindi assegnarli agli utenti del sito di succursale. Per informazioni dettagliate, vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md) e [Creare i criteri di routing VoIP per gli utenti di succursali in Lync Server 2013](lync-server-2013-create-the-voip-routing-policy-for-branch-users.md) nella documentazione relativa alla distribuzione.

## Routing di numeri di interno

Durante la preparazione di dial plan e criteri vocali per gli utenti di siti di succursale, verificare di aver incluso regole di normalizzazione e di conversione conformi alle stringhe e al formato dei numeri utilizzati nell'attributo msRTCSIP-line (o URI di linea) per consentire l'instradamento corretto delle chiamate di Lync 2013 tra gli utenti del sito di succursale e gli utenti del sito centrale, soprattutto quando le chiamate devono essere reinstradate tramite PSTN in caso di indisponibilità del collegamento WAN. Per i numeri composti contenenti numeri di interno, sono inoltre necessarie considerazioni specifiche rispetto ai numeri di telefono semplici.

Per le regole di normalizzazione e le regole di conversione corrispondenti a URI di linea contenenti un numero di interno, da solo o insieme a un numero di telefono E. 164 completo, esistono requisiti aggiuntivi. In questa sezione sono descritti alcuni scenari di esempio con l'indirizzamento di chiamate per URI di linea contenenti un numero di interno.

Se nell'organizzazione non sono configurati numeri di telefono DID (Direct Inward Dial) per utenti singoli e l'URI di linea di ogni utente è configurato con un *solo* numero di interno, gli utenti interni possono chiamarsi componendo solo il numero di interno desiderato. È tuttavia necessario configurare regole di normalizzazione applicabili alle chiamate da un utente di un sito di succursale a un utente del sito centrale corrispondenti ai numeri di interno.

In uno scenario in cui sia disponibile un collegamento WAN tra il sito di succursale e il sito centrale, per le chiamate tra utenti del sito di succursale e utenti del sito centrale non è necessaria la regola di normalizzazione per la conversione del numero, poiché la chiamata non viene indirizzata attraverso PSTN. Ad esempio:


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome regola</th>
<th>Descrizione</th>
<th>Formato numero</th>
<th>Conversione</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5digitExtensions</p></td>
<td><p>Non converte i numeri a cinque cifre</p></td>
<td><p>^(\d{5})$</p></td>
<td><p>$1</p></td>
<td><p>10001 non viene convertito</p></td>
</tr>
</tbody>
</table>


È inoltre necessario prevedere numeri di interno per scenari specifici in cui, ad esempio, il collegamento WAN tra un sito di succursale e il sito centrale non sia disponibile e sia necessario instradare tramite PSTN le chiamate provenienti dal sito di succursale. Se durante un'interruzione del funzionamento del collegamento WAN un utente di un sito di succursale chiama un utente del sito centrale componendo solo l'interno di quest'ultimo, è necessaria una regola di conversione in uscita che aggiunga il numero di telefono completo dell'utente del sito centrale. Se l'URI di linea di un utente contiene il numero di telefono completo dell'organizzazione e il numero di interno univoco dell'utente anziché il numero di telefono completo univoco dell'utente, è necessaria un regola di conversione in uscita che aggiunga il numero di telefono completo dell'organizzazione. Ad esempio:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Formato corrispondente</th>
<th>Conversione</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Converte i numeri a cinque cifre in numero di telefono e interno dell'utente corrispondente</p></td>
<td><p>^(\d{5})$</p></td>
<td><p>+14255550123;ext=$1</p></td>
<td><p>10001 viene convertito in +14255550123;ext=10001</p></td>
</tr>
<tr class="even">
<td><p>Converte i numeri a cinque cifre in numero di telefono dell'organizzazione e interno dell'utente corrispondente</p></td>
<td><p>^(\d{5})$</p></td>
<td><p>+14255550100;ext=$1</p></td>
<td><p>10001 viene convertito in +14255550100;ext=10001</p></td>
</tr>
</tbody>
</table>


In questo scenario, se i numeri di interno non sono supportati dal trunk peer che gestisce il reindirizzamento a PSTN, la regola di conversione in uscita deve inoltre prevedere la rimozione del numero di interno. Ad esempio:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Formato corrispondente</th>
<th>Conversione</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rimuove l'interno dai numeri di telefono con interno</p></td>
<td><p>^\+(\d*);ext=(\d*)$</p></td>
<td><p>+$1</p></td>
<td><p>+14255550123;ext=10001 viene convertito in +14255550123</p></td>
</tr>
</tbody>
</table>


Indipendentemente dalla disponibilità di un collegamento WAN, se per l'organizzazione non sono configurati numeri DID per i singoli utenti e l'URI di linea di ogni utente contiene il numero di telefono dell'organizzazione e il numero di interno univoco dell'utente, è necessario configurare l'URI di linea del numero di telefono dell'organizzazione con un numero raggiungibile da parte del trunk peer o del gateway PSTN presso il sito di succursale. È inoltre necessario configurare l'URI di linea del numero di telefono dell'organizzazione in modo che includa l'interno univoco per le chiamate da indirizzare a tale numero.

Per informazioni dettagliate sulle chiamate da un utente del sito centrale a un utente di un sito di succursale in caso di indisponibilità del collegamento WAN tra i siti, vedere "Preparazione per il funzionamento continuato (survivability) della segreteria telefonica" più avanti in questo argomento. Per informazioni dettagliate sui dial plan e le regole di normalizzazione, con altre regole di esempio, vedere [Dial plan e regole di normalizzazione in Lync Server 2013](lync-server-2013-dial-plans-and-normalization-rules.md) nella documentazione relativa alla pianificazione e [Configurazione dei dial plan in Lync Server 2013](lync-server-2013-configuring-dial-plans.md) nella documentazione relativa alla distribuzione. Per informazioni dettagliate sulle regole di conversione in uscita, vedere [Regole di conversione in Lync Server 2013](lync-server-2013-translation-rules.md) nella documentazione relativa alla pianificazione e [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.

## Preparazione per il funzionamento continuato (survivability) della segreteria telefonica

La Messaggistica unificata di Exchange di solito viene installata solo presso il sito centrale e non presso i siti di succursale. Il chiamante deve poter lasciare un messaggio nella segreteria telefonica anche quando il collegamento WAN tra il sito di succursale e il sito centrale non è disponibile. La configurazione dell'URI di linea per il numero di telefono dell'Operatore automatico Messaggistica unificata di Exchange che fornisce il servizio di segreteria telefonica agli utenti dei siti di succursale richiede pertanto un'attenzione particolare, così come i criteri vocali, il dial plan e le regole di normalizzazione applicabili per tale numero di telefono della segreteria telefonica.

Survivable Branch Appliance (SBA) e Survivable Branch Server consentono il funzionamento continuato (survivability) della segreteria telefonica per gli utenti di succursale durante un'interruzione del collegamento WAN. In particolare, se si utilizza un Survivable Branch Appliance o un Survivable Branch Server e il collegamento WAN diventa non disponibile, l'SBA o il Survivable Branch Server reinstrada tramite PSTN le chiamate senza risposta alla Messaggistica unificata di Exchange presso il sito centrale. Con un SBA o un Survivable Branch Server, durante un'interruzione del funzionamento del collegamento WAN gli utenti possono inoltre recuperare i messaggi nella segreteria telefonica tramite PSTN. In caso di indisponibilità del collegamento WAN, il Survivable Branch Appliance o il Survivable Branch Server infine accoda le notifiche delle chiamate senza risposta e quindi, quando il collegamento WAN viene ripristinato, le carica nel server di Messaggistica unificata di Exchange. Per garantire la resilienza del reinstradamento della segreteria telefonica, aggiungere una voce per l'FQDN del pool del sito centrale e una voce per l'FQDN del server perimetrale nel Survivable Branch Server. In caso contrario, se il sito di succursale non dispone di un server DNS, può verificarsi il timeout della risoluzione DNS.

Per configurare il funzionamento continuato (survivability) della segreteria telefonica per gli utenti dei siti di succursale, sono consigliate le configurazioni seguenti:

  - Un amministratore Microsoft Exchange deve configurare Messaggistica unificata di Exchange Operatore automatico in modo che accetti solo messaggi. Con questa configurazione viene disabilitata ogni altra funzionalità generica, ad esempio il trasferimento a un utente o al centralino. In alternativa, l'amministratore di Exchange può indirizzare le chiamate al centralino utilizzando Operatore automatico, generico o personalizzato.

  - L'amministratore Lync Server deve utilizzare il numero di telefono assegnato a Operatore automatico come numero **Operatore automatico messaggistica unificata di Exchange** nelle impostazioni di reindirizzamento della segreteria telefonica per Survivable Branch Appliance o il server di succursale.

  - L'amministratore di Lync Server deve ottenere e utilizzare il numero di telefono per l'accesso del sottoscrittore della Messaggistica unificata di Exchange come numero di **accesso del sottoscrittore** nelle impostazioni di reinstradamento della segreteria telefonica per il Survivable Branch Appliance o il Survivable Branch Server.

  - L'amministratore di Lync Server deve configurare la Messaggistica unificata di Exchange in modo che a tutti gli utenti di succursale a cui è necessario l'accesso alla segreteria telefonica durante un problema del collegamento WAN sia associato un unico dial plan.

  - In caso di indisponibilità del collegamento WAN, le chiamate agli utenti dei siti di succursale possono essere instradate alla casella vocale di messaggistica unificata di Exchange degli utenti, ma solo se i criteri vocali applicati alle chiamate specificano un numero di telefono della segreteria telefonica univoco e senza numero di interno.

## Requisiti hardware e software per la resilienza dei siti di succursale

I requisiti hardware e software variano a seconda della soluzione di resilienza in uso.

## Requisiti per Survivable Branch Appliance

L'hardware e il software necessari sono incorporati nel Survivable Branch Appliance. È inoltre consigliabile, tuttavia, che in ogni sito di succursale sia distribuito un server DHCP per ottenere indirizzi IP per i client. In caso contrario, quando il lease DHCP scade, i client perdono la connettività IP.

Se i server DNS aziendali si trovano solo presso i siti centrali, in caso di interruzione del funzionamento del collegamento WAN gli utenti dei siti di succursale non saranno in grado di connettersi a tali server. L'individuazione di Lync Server, che utilizza un record di risorse di servizio (SRV) DNS, quindi non funzionerà. Per garantire il reinstradamento rapido durante un problema del collegamento WAN, i record DNS devono essere memorizzati nella cache presso il sito di succursale. Se il router di succursale supporta la memorizzazione dei record DNS nella cache, attivarla. In alternativa, è possibile distribuire un server DNS presso la succursale. Può trattarsi di un server autonomo o di una versione del Survivable Branch Appliance in grado di supportare le funzionalità DNS. Per informazioni dettagliate, rivolgersi al provider del Survivable Branch Appliance.


> [!NOTE]
> Presso un sito di succursale non è necessario un controller di dominio. Il Survivable Branch Appliance effettua l'autenticazione dei client mediante un certificato speciale che invia ai client in risposta alla richiesta di certificato proveniente dai client al momento dell'accesso.



I client Lync possono individuare Lync Server mediante l'utilizzo dell'opzione DHCP 120 (opzione registrazione SIP). È possibile configurare tale opzione in uno dei due modi seguenti:

  - Configurando il server DHCP presso il sito di succursale in modo che risponda alle query DHCP 120, che restituiscono l'FQDN della funzione di registrazione del Survivable Branch Appliance o del Survivable Branch Server.

  - Attivando DHCP in Lync Server. In questo modo la funzione di registrazione di Lync Server risponde alle query DHCP 120. Si noti che la funzione di registrazione risponde solo alle query DHCP con l'opzione 120.

Nei siti di succursale di grandi dimensioni dotati di più subnet, per inoltrare query DHCP 120 al server DHCP (configurazione 1) o alla funzione di registrazione (configurazione 2), è inoltre necessario abilitare gli agenti di inoltro DHCP.

È infine necessario configurare gli utenti dei siti di succursale per VoIP aziendale ed eseguirne il provisioning con un endpoint di comunicazione unificata appropriato.

## Requisiti per Survivable Branch Server

I requisiti per Survivable Branch Server sono analoghi a quelli di un Front End Server. Per informazioni dettagliate, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa alla pianificazione.

## Requisiti per distribuzioni di siti di succursale Lync Server in scala intera

Per informazioni dettagliate, vedere [Determinazione dei requisiti dell'infrastruttura per Lync Server 2013](lync-server-2013-determining-your-infrastructure-requirements.md) nella documentazione relativa alla pianificazione.

