---
title: Set-CsTrunkConfiguration
TOCTitle: Set-CsTrunkConfiguration
ms:assetid: 18152388-68de-4a6b-b5a1-248534ecde72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398238(v=OCS.15)
ms:contentKeyID: 49299814
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrunkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-02-27_

Modifica una configurazione trunk esistente che descrive le impostazioni di un'entità peer di trunking, ad esempio un gateway PSTN (Public Switched Telephone Network), un sistema IP-PBX (Public Branch Exchange) o un servizio SBC (Session Border Controller) nel provider di servizi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTrunkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene modificata una configurazione trunk con identità site:Redmond e viene abilitato il bypass degli elementi multimediali. Il bypass degli elementi multimediali viene abilitato assegnando il valore $True al parametro EnableBypass. Le proprietà rimanenti per questa configurazione manterranno i valori esistenti.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## ESEMPIO 2

In questo esempio viene modificata una regola di conversione in uscita definita per la configurazione trunk con identità site:Redmond. Si noti che, per apportare la modifica, non viene effettivamente chiamato il cmdlet **Set-CsTrunkConfiguration**. Le modifiche apportate tramite il cmdlet **Set-CsOutboundTranslationRule** verranno estese automaticamente alla configurazione trunk con identità corrispondente alla parte di ambito dell'identità della regola di conversione in uscita.

    Set-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Translation '$1'

## ESEMPIO 3

Nell'esempio 3 viene impostato SRTPMode per tutte le configurazioni trunk definite su Facoltativo nell'ambito del sito. Nella prima parte del comando viene chiamato il cmdlet **Get-CsTrunkConfiguration**, che utilizza il parametro Filter per recuperare tutte le configurazioni trunk con valore Identity che inizia con site:, ovvero tutte le configurazioni trunk definite a livello di sito. La raccolta di configurazioni viene quindi inviata tramite pipe al cmdlet **Set-CsTrunkConfiguration**, che imposta la proprietà SRTPMode di ciascuna configurazione su Optional.

    Get-CsTrunkConfiguration -Filter site:* | Set-CsTrunkConfiguration -SRTPMode "Optional"

## ESEMPIO 4

In questo esempio viene modificata una configurazione trunk con identità site:Redmond per abilitare il supporto PIDF-LO. Per impostazione predefinita, il valore del parametro EnablePIDFLOSupport è False. In questo esempio, il valore viene impostato su True per consentire il supporto della posizione per le chiamate di emergenza. Per consentire l'invio delle informazioni sulla posizione al trunk da parte dell'applicazione di routing in uscita, è necessario impostare EnablePIDFLOSupport su True.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnablePIDFLOSupport $True

## Descrizione dettagliata

Utilizzare questo cmdlet per modificare una configurazione di trunking applicabile a entità gateway PSTN. Ogni configurazione contiene impostazioni specifiche di un'entità trunking peer, ad esempio un gateway PSTN, un sistema IP-PBX o un servizio SBC nel provider di servizi. Tali impostazioni consentono di configurare diversi aspetti, ad esempio se abilitare o meno il bypass degli elementi multimediali in questo trunk, se inviare o meno i pacchetti RTCP (Real-Time Control Protocol) in determinate condizioni e se richiedere o meno la crittografia SRTP (Secure Real-Time Protocol).

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsTrunkConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrunkConfiguration"}

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
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Il valore di questo parametro determina se esiste un punto di terminazione multimediale noto. Un esempio di punto di terminazione multimediale noto può essere costituito da un gateway PSTN in cui la terminazione degli elementi multimediali ha lo stesso IP della terminazione dei segnali. Impostare questo valore su False se il trunk non dispone di un punto di terminazione multimediale noto.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Stringa che descrive lo scopo della configurazione trunk.</p></td>
</tr>
<tr class="even">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se è possibile utilizzare il protocollo 3pcc per consentire alle chiamate trasferite di ignorare il sito ospitato. 3pcc è noto anche come &quot;controllo di terze parti&quot; e viene applicato quando viene utilizzata una terza parte per connettere due chiamanti, ad esempio un operatore che effettua una chiamata tra la persona A e la persona B. Il metodo REFER è un metodo SIP standard che indica che il destinatario deve contattare una terza parte utilizzando le informazioni fornite dal mittente. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBypass</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Il valore di questo parametro determina se il bypass multimediale è abilitato per questo trunk. Impostare questo valore su True per abilitare il bypass. Per il corretto funzionamento del bypass multimediale, devono essere supportate alcune funzionalità da parte dei gateway PSTN, dei servizi SBC e dei sistemi PBX, tra cui:</p>
<p>- La possibilità di ricevere risposte instradate a un invito.</p>
<p>- I client Lync Server e il punto di terminazione multimediale devono essere in grado di comunicare direttamente senza l'intermediazione di un Mediation Server.</p>
<p>- La subnet del gateway deve essere definita nello stesso luogo della subnet del client oppure, se in luoghi diversi, è necessario che i siti non siano separati da collegamenti WAN con larghezza di banda limitata.</p>
<p>Il bypass degli elementi multimediali può essere abilitato solo se vengono soddisfatte le seguenti condizioni:</p>
<p>- Il parametro ConcentratedTopology è impostato su True</p>
<p>- Il parametro EnableReferSupport è impostato su False e RTCPActiveCalls e RTCPCallsOnHold sono impostati su False oppure EnableReferSupport è impostato su True</p>
<p>Se EnableBypass è impostato su True ed EnableReferSupport è impostato su False, le chiamate di bypass che verranno trasferite successivamente diventeranno di non bypass.</p>
<p>Affinché il bypass multimediale funzioni per un determinato trunk, è necessario che venga abilitato sia globalmente che per il trunk in questione. Per abilitare il bypass multimediale globalmente, utilizzare il cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro viene impostato su True, le chiamate in uscita che non ricevono risposta dal gateway entro 10 secondi verranno instradate al trunk successivo disponibile. Se non sono presenti trunk aggiuntivi, la chiamata verrà automaticamente eliminata. In un'organizzazione con reti e risposte dei gateway lente, esiste il rischio che le chiamate vengano eliminate inutilmente.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro viene impostato su True, il routing vocale in base al luogo sarà abilitato per le chiamate che passano attraverso trunk SIP gestiti dalla raccolta specificata di impostazioni di configurazione di tali trunk. Con questo tipo di routing, durante l'instradamento delle chiamate, vengono prese in considerazione sia la posizione dell'utente che effettua la chiamata sia la posizione dell'utente che riceve la chiamata. Quando questa proprietà è impostata su True (il valore predefinito è False), è necessario impostare anche la proprietà NetworkSiteId.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se il provider di servizi è un operatore di telefonia mobile.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se i trunk SIP supportano il servizio vocale online. Con tale servizio, gli utenti dispongono di un account di Lync Server locale, ma con segreteria telefonica ospitata da Skype for Business online. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se instradare le chiamate di emergenza con PIDF-LO (Presence Information Data Format Location Object) attraverso il gateway definito. Impostare il parametro su True se le chiamate di emergenza devono essere instradate a un provider di servizi di emergenza certificato. La posizione verrà trasmessa con la chiamata.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se questo trunk supporta la ricezione di richieste Refer da Mediation Server.</p>
<p>Il bypass degli elementi multimediali può essere abilitato solo se vengono soddisfatte le seguenti condizioni:</p>
<p>- Il parametro ConcentratedTopology è impostato su True</p>
<p>- Il parametro EnableReferSupport è impostato su False e RTCPActiveCalls e RTCPCallsOnHold sono impostati su False oppure EnableReferSupport è impostato su True</p>
<p>Se EnableBypass è impostato su True ed EnableReferSupport è impostato su False, le chiamate di bypass che verranno trasferite successivamente diventeranno di non bypass.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se i trunk SIP supportano il latch RTP, una tecnologia che consente la connettività RTP/RTCP tramite un firewall o un dispositivo NAT (Network Address Translator). Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se il timer sessione è abilitato. I timer sessione consentono di determinare se una determinata sessione è ancora attiva.</p>
<p>Anche se questo parametro è impostato su False, è possibile che i timer di sessione siano applicabili se sono abilitati nella connessione remota. In questo caso, il Mediation Server risponderà alle indagini dei timer di sessione dall'entità remota.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, il gateway PSTN, il sistema IP-PBX o il servizio SBC nel provider di servizi incrementa il volume audio in flussi vocali che vengono inviati al Mediation Server o ai client Lync Server. Se il valore è impostato su False, il volume audio verrà aumentato nel Mediation Server (per chiamate non di bypass) o nei client Lync Server (per chiamate di bypass).</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se le informazioni del registro chiamate verranno inoltrate tramite il trunk. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'intestazione PAI (P-Asserted-Identity) verrà inoltrata insieme alla chiamata. L'intestazione PAI consente di verificare l'identità del chiamante. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificatore univoco che include l'ambito della configurazione trunk. Le configurazioni trunk possono esistere nell'ambito globale o del sito oppure nell'ambito del servizio nel caso di un servizio gateway PSTN, ad esempio site:Redmond per il sito o PstnGateway:Redmond.litwareinc.com per il servizio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>TrunkConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p>
<p>Questo parametro richiede un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration, che può essere recuperato chiamando il cmdlet <strong>Get-CsTrunkConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>UInt32</p></td>
<td><p>Numero massimo di risposte instradate che possono essere ricevute da un gateway PSTN, un sistema IP-PBX o un servizio SBC nel provider di servizi per un invito inviato a Mediation Server.</p>
<p>Valore predefinito: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>ID del sito di rete associato alla raccolta di impostazioni di configurazione dei trunk. Se la proprietà EnableLocationRestriction è impostata su True, il routing in base al luogo attraverso tale trunk verrà gestito utilizzando le impostazioni configurate per il sito specificato. Gli ID dei siti di rete possono essere recuperati mediante il seguente comando:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di regole di conversione dei numeri in uscita assegnate al trunk. È possibile recuperare informazioni sulle regole disponibili utilizzando il comando seguente:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di regole di conversione dei numeri di telefono che si applicano alle chiamate gestite mediante il routing in uscita (chiamate instradate a destinazioni PBX o PSTN).</p>
<p>Sebbene l'elenco e le regole possano essere modificati direttamente tramite questo cmdlet, è consigliabile modificare le regole di conversione in uscita mediante il cmdlet <strong>Set-CsOutboundTranslationRule</strong>. Tramite il cmdlet <strong>Set-CsOutboundTranslationRule</strong> viene modificata la regola e le modifiche vengono estese automaticamente alla configurazione trunk. Per modificare la configurazione trunk tramite l'aggiunta di una nuova regola di conversione in uscita, chiamare il cmdlet <strong>New-CsOutboundTranslationRule</strong>. La nuova regola verrà aggiunta alla configurazione trunk con l'ambito corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di utilizzi PSTN assegnati al trunk. È possibile recuperare informazioni sugli utilizzi disponibili utilizzando il comando seguente:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se il parametro viene impostato su True, Mediation Server rimuoverà i segni più (+) iniziali dagli URI (Uniform Resource Identifier) prima di inviarli al provider di servizi.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo parametro specifica se i pacchetti RTCP devono continuare a essere inviati dal gateway PSTN, dal sistema IP-PBX o dal servizio SBC nel provider di servizi per le chiamate attive. Una chiamata attiva in questo contesto indica una chiamata in cui è consentito il flusso degli elementi multimediali almeno in una direzione. Se il valore di RTCPActiveCalls è impostato su True, il client Mediation Server o Lync Server può terminare una chiamata qualora non riceva pacchetti RTCP per oltre 30 secondi.</p>
<p>Con la disabilitazione dei controlli degli elementi multimediali RTCP ricevuti per le chiamate attive in elementi Lync Server viene rimossa un'importante protezione per l'individuazione di un peer rimosso. Questa operazione deve essere effettuata solo se necessario.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo parametro specifica se i pacchetti RTCP devono continuare a essere inviati attraverso il trunk per le chiamate in attesa e se non deve essere previsto il flusso di pacchetti di elementi multimediali in alcuna direzione. Se è abilitato il comando di musica di attesa nel client Lync Server o nel trunk, la chiamata verrà considerata attiva e questa proprietà verrà ignorata. In questo caso utilizzare il parametro RTCPActiveCalls.</p>
<p>Con la disabilitazione dei controlli degli elementi multimediali RTCP ricevuti per le chiamate attive in elementi Lync Server viene rimossa un'importante protezione per l'individuazione di un peer rimosso. Questa operazione deve essere effettuata solo se necessario.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Elenco di regole di conversione del codice di riposta SIP che si applicano ai codici di risposta ricevuti da un gateway PSTN, un sistema IP-PBX o un servizio SBC nel provider di servizi. Queste regole consentono all'amministratore di eseguire il mapping tra i codici di risposta SIP con valori compresi tra 400 e 699 ricevuti su un trunk e nuovi valori più coerenti con Lync Server.</p>
<p>È possibile creare questo elenco e le regole corrispondenti direttamente tramite questo cmdlet. È tuttavia consigliabile creare le regole di conversione del codice di risposta SIP mediante la chiamata del cmdlet <strong>New-CsSipResponseCodeTranslationRule</strong>. Tale cmdlet consente di creare la regola e assegnarla alla configurazione trunk con l'ambito corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SRTPMode</p></td>
<td><p>Il valore di questo parametro determina il livello di supporto del protocollo SRTP per la protezione del traffico multimediale tra il Mediation Server e il gateway PSTN, il sistema IP-PBX o il servizio SBC presso il provider dei servizi. Nel caso del bypass multimediale, questo valore deve essere compatibile con l'impostazione di EncryptionLevel nella configurazione degli elementi multimediali. Tale configurazione viene definita utilizzando i cmdlet <strong>New-CsMediaConfiguration</strong> e <strong>Set-CsMediaConfiguration</strong>.</p>
<p>Valori validi:</p>
<p>- Obbligatorio: è necessario utilizzare la crittografia SRTP.</p>
<p>- Facoltativo: SRTP verrà utilizzato se supportato dal provider di servizi.</p>
<p>- Non supportato: la crittografia SRTP non è supportata, pertanto non verrà utilizzata.</p>
<p>Si noti che il parametro SRTPMode viene utilizzato esclusivamente se il gateway è configurato per l'utilizzo del protocollo TLS (Transport Layer Security). Se invece il gateway è configurato con il protocollo TCP (Transmission Control Protocol) per il trasporto, il parametro SRTPMode verrà impostato internamente su NotSupported.</p>
<p>Valore predefinito: Obbligatorio</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration. Accetta l'input da pipeline di oggetti configurazione trunk.

## Tipi restituiti

Questo cmdlet non restituisce un valore, bensì modifica un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

