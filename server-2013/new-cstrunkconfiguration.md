---
title: New-CsTrunkConfiguration
TOCTitle: New-CsTrunkConfiguration
ms:assetid: f3958f86-3313-4929-9f9d-f796a2669aea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413021(v=OCS.15)
ms:contentKeyID: 49302462
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrunkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova configurazione trunk esistente che descrive le impostazioni di un'entità peer di trunking, ad esempio un gateway PSTN (Public Switched Telephone Network), un sistema IP-PBX (Public Branch Exchange) o un servizio SBC (Session Border Controller) nel provider di servizi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsTrunkConfiguration -Identity <XdsIdentity> [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-InMemory <SwitchParameter>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene creata una nuova configurazione trunk con identità site:Redmond. Le restanti proprietà per questa nuova configurazione verranno popolate con valori predefiniti.

    New-CsTrunkConfiguration -Identity site:Redmond

## ESEMPIO 2

Con questo esempio viene creata una nuova configurazione trunk con identità site:Redmond e viene abilitato il bypass multimediale. Il bypass multimediale viene abilitato assegnando il valore $True al parametro EnableBypass. Le restanti proprietà per questa nuova configurazione verranno popolate con valori predefiniti.

    New-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## ESEMPIO 3

Con questo esempio viene creata una nuova configurazione trunk con identità site:Redmond, quindi viene assegnata una nuova conversione in uscita a tale trunk. Nella prima riga dell'esempio viene chiamato il cmdlet **New-CsTrunkConfiguration** per creare la nuova configurazione trunk con impostazioni predefinite. Nella seconda linea viene chiamato il cmdlet **New-CsOutboundTranslationRule**. Si noti il valore assegnato all'identità: site:Redmond/OTR1. La prima parte dell'identità (site:Redmond) definisce l'ambito a cui viene applicata la regola. Tale ambito corrisponde all'identità della nuova configurazione trunk, pertanto questa regola verrà applicata automaticamente a tale configurazione. L'ambito è seguito da una barra (/) e da una stringa, che corrisponde a un nome univoco per questa regola (possono esistere più regole per ogni ambito). Vengono quindi passati valori ai parametri Pattern e Translation per definire questa regola.

    New-CsTrunkConfiguration -Identity site:Redmond
    New-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Pattern '^\+(\d{8})$' -Translation '9$1'

## Descrizione dettagliata

Utilizzare questo cmdlet per creare una nuova configurazione di trunk applicabile alle entità del gateway PSTN. Ogni configurazione contiene impostazioni specifiche per un'entità peer trunk quale un gateway PSTN, IP-PBX o SBC nel provider di servizi. Tali impostazioni consentono di configurare vari aspetti, ad esempio se abilitare o meno il bypass multimediale in questo trunk, se i pacchetti RTCP devono essere inviati o meno in determinate condizioni e se richiedere o meno la crittografia SRTP (Secure Real-Time Protocol).

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsTrunkConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrunkConfiguration"}

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
<td><p>Identificatore univoco che include l'ambito della configurazione trunk. Le configurazioni trunk possono essere create per l'ambito del sito, oppure per l'ambito del servizio nel caso di un gateway PSTN. (Una configurazione globale esiste per impostazione predefinita e non è possibile rimuoverla o ricrearla). Ad esempio, site:Redmond (per il sito) o PstnGateway:Redmond.litwareinc.com (per il servizio).</p></td>
</tr>
<tr class="even">
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Il valore di questo parametro determina se esiste un punto di terminazione multimediale noto. Un esempio di punto di terminazione multimediale noto può essere costituito da un gateway PSTN in cui la terminazione dei supporti ha lo stesso IP della terminazione dei segnali. Impostare questo valore su False se il trunk non dispone di un punto di terminazione multimediale noto.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Stringa che descrive lo scopo della configurazione trunk.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se è possibile utilizzare il protocollo 3pcc per consentire alle chiamate trasferite di eseguire il bypass del sito ospitato. 3pcc è anche definito &quot;controllo di terza parte&quot; e viene eseguito quando viene utilizzata una terza parte per connettere una coppia di chiamanti (ad esempio, un operatore che esegue una chiamata dalla persona A alla persona B). Il metodo REFER è un metodo SIP standard che indica che il destinatario deve contattare una terza parte utilizzando le informazioni fornite dal mittente. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBypass</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Il valore di questo parametro determina se il bypass multimediale è abilitato per questo trunk. L'impostazione di questo valore su True consente di abilitare il bypass. Affinché il bypass multimediale funzioni correttamente, è necessario che i gateway PSTN, i controller SBC e i sistemi PBX supportino determinate funzionalità, tra cui:</p>
<p>- La possibilità di ricevere risposte instradate a un invito.</p>
<p>- I client Lync Server e i punti di terminazione multimediale devono essere in grado di comunicare direttamente senza l'intermediazione di Mediation Server.</p>
<p>- La subnet del gateway deve essere definita nello stesso luogo della subnet del client oppure, se in luoghi diversi, è necessario che i siti non siano separati da collegamenti WAN con larghezza di banda limitata.</p>
<p>Il bypass multimediale può essere abilitato solo nei seguenti casi:</p>
<p>- Il parametro ConcentratedTopology è impostato su True</p>
<p>- Il parametro EnableReferSupport è impostato su False mentre RTCPActiveCalls e RTCPCallsOnHold sono impostati su False oppure EnableReferSupport è impostato su True</p>
<p>Se EnableBypass è True e EnableReferSupport è False, le chiamate di bypass che vengono successivamente trasferite diventeranno non di bypass.</p>
<p>Affinché il bypass multimediale funzioni per un determinato trunk, è necessario che venga abilitato globalmente oltre che per il trunk in questione. Utilizzare il cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong> per abilitare il bypass multimediale globalmente.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro viene impostato su True, le chiamate in uscita che non ricevono risposta dal gateway entro 10 secondi verranno instradate al trunk successivo disponibile. Se non sono presenti trunk aggiuntivi, la chiamata verrà automaticamente eliminata. In un'organizzazione con reti e risposte dei gateway lente, esiste il rischio che le chiamate vengano eliminate inutilmente.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se il parametro viene impostato su True, il routing vocale in base al luogo viene abilitato per le chiamate che utilizzano i trunk SIP e sono gestite dalla raccolta specificata di impostazioni di configurazione dei trunk SIP. Quando si utilizza il routing vocale in base al luogo, la posizione dell'utente che effettua la chiamata e la posizione dell'utente che riceve la chiamata vengono tenute in considerazione quando le chiamate vengono instradate. Se la proprietà è impostata su True (il valore predefinito è False), è necessario impostare anche la proprietà NetworkSiteId.</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se il provider di servizi è un operatore di telefonia mobile.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se i trunk SIP supportano la voce online. Con la voce online, gli utenti hanno un account Lync Server locale ma la segreteria telefonica ospitata da Office 365. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Definisce se inoltrare le chiamate di emergenza con Presence Information Data Format Location Object (PIDF-LO) tramite il gateway definito. Impostare questo parametro su True se le chiamate di emergenza devono essere instradate a un provider di servizi di emergenza certificato (la posizione verrà trasmessa con la chiamata).</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se questo trunk supporta la ricezione di richieste Refer da Mediation Server.</p>
<p>Il bypass multimediale può essere abilitato solo nei seguenti casi:</p>
<p>- Il parametro ConcentratedTopology è impostato su True</p>
<p>- Il parametro EnableReferSupport è impostato su False mentre RTCPActiveCalls e RTCPCallsOnHold sono impostati su False oppure EnableReferSupport è impostato su True</p>
<p>Se EnableBypass è True e EnableReferSupport è False, le chiamate di bypass che vengono successivamente trasferite diventeranno non di bypass.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se i trunk SIP supportano o meno RTP latching. RTP latching è una tecnologia che consente la connettività RTP/RTCP tramite un dispositivo o un firewall NAT (Network ddress translator). Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Specifica se il timer sessione è abilitato. I timer sessione consentono di determinare se una determinata sessione è ancora attiva.</p>
<p>Anche se questo parametro è impostato su False, i timer di sessione possono essere applicabili se per la connessione remota è abilitato un timer di sessione. In tal caso Mediation Server risponde ai probe del timer di sessione dall'entità remota.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, il gateway PSTN, IP-PBX o SBC nel provider di servizi incrementano il volume dell'audio nei flussi vocali inviati a Mediation Server o ai client Lync Server. Se questo valore è impostato su False, l'audio verrà aumentato in Mediation Server (per le chiamate non di bypass) o nei client Lync Server (per le chiamate di bypass).</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se le informazioni sulla cronologia delle chiamate verranno inoltrate attraverso il trunk. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'intestazione P-Asserted-Identity (PAI) verrà inoltrata insieme alla chiamata. L'intestazione PAI fornisce un modo per verificare l'identità del chiamante. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>UInt32</p></td>
<td><p>Il numero massimo di risposte instradate che un gateway PSTN, IP-PBX o SBC nel provider di servizi può ricevere per un invito inviato a Mediation Server.</p>
<p>Valore predefinito: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>ID sito del sito di rete associato alla nuova raccolta di impostazioni di configurazione dei trunk. Se la proprietà EnableLocationRestriction è impostata su True, il routing vocale in base al luogo che utilizza questo trunk verrà gestito utilizzando le impostazioni configurate per il sito specificato. È possibile recuperare gli ID del sito di rete mediante questo comando:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta delle regole di conversione dei numeri di chiamata in uscita assegnate al trunk. È possibile recuperare informazioni sulle regole disponibili eseguendo il comando seguente:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di regole di conversione dei numeri di telefono che si applicano alle chiamate gestite mediante il routing in uscita (chiamate instradate a destinazioni PBX o PSTN).</p>
<p>Sebbene l'elenco e le regole possano essere creati direttamente con questo cmdlet, è consigliabile creare le regole di conversione in uscita mediante il cmdlet <strong>New-CsOutboundTranslationRule</strong>, che crea la regola e la assegna alla configurazione trunk con ambito corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di utilizzi PSTN assegnati al trunk. È possibile recuperare informazioni sugli utilizzi disponibili eseguendo il comando seguente:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se il parametro viene impostato su True, Mediation Server rimuoverà i segni più (+) iniziali dagli URI prima di inviarli al provider di servizi.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo parametro determina se i pacchetti RTCP vengono inviati dal gateway PSTN, da IP-PBX o da SBC al provider di servizi per le chiamate attive. Una chiamata attiva in questo contesto è una chiamata in cui il flusso dei supporti è consentito almeno in una direzione. Se RTCPActiveCalls è impostato su True, Mediation Server o il client Lync Server possono terminare una chiamata se non riceve i pacchetti RTCP per un periodo che superi 30 secondi.</p>
<p>Se si disabilitano i controlli per i supporti RTCP ricevuti per le chiamate attive negli elementi di Lync Server, si rimuove un importante strumento per rilevare un peer rimosso, pertanto questa operazione deve essere eseguita solo se necessaria.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo parametro determina se i pacchetti RTCP continuano a essere inviati attraverso il trunk per le chiamate messe in attesa e non è previsto il flusso di pacchetti di supporti in alcuna direzione. Se la musica di attesa è abilitata nel client Lync Server o nel trunk, la chiamata verrà considerata attiva e questa proprietà verrà ignorata. In queste circostanze utilizzare il parametro RTCPActiveCalls.</p>
<p>Se si disabilitano i controlli per i supporti RTCP ricevuti per le chiamate attive negli elementi di Lync Server, si rimuove un importante strumento per rilevare un peer rimosso, pertanto questa operazione deve essere eseguita solo se necessaria.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un elenco di regole di conversione del codice di risposta SIP applicate ai codici di risposta ricevuti da un gateway PSTN, da IP-PBX o da SBC nel provider di servizi. Queste regole consentono all'amministratore di mappare i codici di risposta SIP a valori compresi tra 400 e 699 ricevuti su un trunk a nuovi valori più coerenti con Lync Server.</p>
<p>È possibile creare questo elenco e le regole corrispondenti direttamente tramite questo cmdlet. È tuttavia consigliabile creare le regole di conversione del codice di risposta SIP mediante la chiamata del cmdlet <strong>New-CsSipResponseCodeTranslationRule</strong>. Tale cmdlet crea la regola e la assegna alla configurazione del trunk con l'ambito corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SRTPMode</p></td>
<td><p>Il valore di questo parametro specifica il livello di supporto del protocollo SRTP per la protezione del traffico multimediale tra Mediation Server e il gateway PSTN, il sistema IP-PBX o il servizio SBC nel provider dei servizi. Nel caso del bypass multimediale, questo valore deve essere compatibile con l'impostazione di EncryptionLevel nella configurazione degli elementi multimediali. La configurazione degli elementi multimediali viene definita utilizzando il cmdlet <strong>New-CsMediaConfiguration</strong> e il cmdlet <strong>Set-CsMediaConfiguration</strong>.</p>
<p>Valori validi:</p>
<p>- Obbligatorio: è necessario utilizzare la crittografia SRTP.</p>
<p>- Facoltativo: SRTP verrà utilizzato se supportato dal gateway.</p>
<p>- Non supportato: la crittografia SRTP non è supportata, pertanto non verrà utilizzata.</p>
<p>Si noti che SRTPMode viene utilizzato solo se il gateway è configurato per l'uso di TLS (Transport Layer Security). Se il gateway è configurato con il protocollo TCP (Transmission Control Protocol) per il trasporto, SRTPMode viene impostato internamente su NotSupported.</p>
<p>Valore predefinito: Obbligatorio</p></td>
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

Nessuno.

## Tipi restituiti

Crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)

