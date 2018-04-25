---
title: New-CsHostingProvider
TOCTitle: New-CsHostingProvider
ms:assetid: 6874cc14-d250-43d4-8868-43cd8d202e9c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398490(v=OCS.15)
ms:contentKeyID: 49300844
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsHostingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo provider di hosting per l'utilizzo nella propria organizzazione. Un provider di hosting è un'organizzazione privata di terze parti che fornisce servizi di messaggistica istantanea, informazioni sulla presenza e altri servizi correlati a un dominio con il quale si desidera attuare una federazione. I provider di hosting come Microsoft Lync Online 2010 si differenziano dai provider pubblici, ad esempio Yahoo\!, MSN e AOL, in quanto non offrono servizi al pubblico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsHostingProvider -Enabled <$true | $false> -Identity <XdsGlobalRelativeIdentity> -ProxyFqdn <String> [-AutodiscoverUrl <String>] [-IsLocal <$true | $false>] [-SipClientPort <UInt64>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] <COMMON PARAMETERS>

    New-CsHostingProvider -Enabled <$true | $false> -EnabledSharedAddressSpace <$true | $false> -HostsOCSUsers <$true | $false> -Identity <XdsGlobalRelativeIdentity> -ProxyFqdn <String> [-AutodiscoverUrl <String>] [-IsLocal <$true | $false>] [-SipClientPort <UInt64>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene creato un nuovo provider di hosting con identità (Identity) Fabrikam.com. Oltre a specificare l'identità, il comando include gli altri due parametri obbligatori: ProxyFqdn, che specifica il server proxy utilizzato da Fabrikam.com, ed Enabled, che indica se il nuovo provider di hosting è abilitato per l'utilizzo. Se si tralascia qualche parametro obbligatorio, il cmdlet **New-CsHostingProvider** richiede di immettere tali valori prima di continuare.

    New-CsHostingProvider -Identity Fabrikam.com -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True

## ESEMPIO 2

Con l'esempio 2 viene dimostrato come creare un nuovo provider di hosting per l'uso in uno scenario a dominio diviso. Un dominio diviso è un dominio in cui alcuni account Lync Server vengono gestiti localmente mentre altri account sono gestiti dal provider di hosting. Per creare questo tipo di provider di hosting è necessario includere i tre parametri obbligatori (Identity, ProxyFqdn ed Enabled). Inoltre è necessario includere (e impostare su True) entrambe i parametri HostsOCSUsers ed EnabledSharedAddressSpace. Per creare un provider di dominio diviso che ospiti servizi non di Lync Server (ad esempio Microsoft Exchange), includere questi stessi parametri impostando però HostsOCSUsers su False.

    New-CsHostingProvider -Identity Fabrikam.com -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True -HostsOCSUsers $True -EnabledSharedAddressSpace $True

## Descrizione dettagliata

La federazione consente a due organizzazioni di instaurare una relazione di trust che facilita la comunicazione tra i due gruppi. Quando si attua una federazione, gli utenti delle due organizzazioni federate possono inviarsi messaggi istantanei, sottoscrivere servizi di notifica della presenza e comunicare in altro modo utilizzando applicazioni SIP come Lync 2013. Lync Server consente tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

Un provider di hosting è un'organizzazione che fornisce servizi di comunicazione SIP ad altre organizzazioni, ad esempio Fabrikam, Inc. può ospitare utenti di Contoso, Northwind Traders e Wingtip Toys. Quando si stabilisce una relazione di federazione con un provider di hosting, si definisce in realtà una federazione con tutte le organizzazioni ospitate da quel provider. Ad esempio, se un'organizzazione si associa tramite federazione a Fabrikam, gli utenti dell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Contoso, Northwind Traders e Wingtip Toys.

I provider di hosting vengono utilizzati inoltre in scenari di dominio diviso. In uno scenario di dominio diviso alcuni utenti di Lync Server dispongono di account ospitati in locale, ovvero ospitati nell'implementazione locale di Lync Server. Altri utenti possono avere i propri account ospitati in remoto presso provider di hosting di terze parti. La federazione con il provider di hosting consente agli utenti in locale e in remoto di comunicare tra loro.

Per attuare la federazione con un provider di hosting di terze parti è necessario creare e abilitare un nuovo provider di hosting. Inoltre, il provider di terze parti dovrà creare una relazione di federazione con la propria organizzazione. Il cmdlet **New-CsHostingProvider** consente di impostare tre tipi di relazioni con il provider di hosting:

Federazione diretta con il provider di hosting. Per creare questo tipo di relazione è necessario includere i tre parametri obbligatori Identity, ProxyFqdn ed Enabled.

Dominio diviso in cui sono ospitati i servizi di Lync Server. Per creare questo tipo di relazione è necessario includere i tre parametri obbligatori. Inoltre è necessario impostare entrambe le proprietà EnabledSharedAddressSpace e HostsOCSUsers su True.

Dominio diviso in cui sono ospitati servizi non di Lync Server (come Microsoft Exchange). Per creare questo tipo di relazione è necessario includere i tre parametri obbligatori. Inoltre è necessario impostare la proprietà EnabledSharedAddressSpace su True e HostsOCSUsers su False.

Quando si crea un nuovo provider di hosting, sia l'identità sia il nome di dominio completo del proxy per quel provider devono essere univoci: non è possibile avere due provider di hosting (o persino un provider di hosting e un provider pubblico) che condividono un'identità e/o un nome di dominio completo del proxy.

Non è inoltre possibile attuare la federazione con un provider di hosting se gli server perimetrali sono configurati per utilizzare il routing predefinito anziché il routing del server DNS (Domain Name System).

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsHostingProvider** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsHostingProvider"}

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
<td><p><em>Enabled</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la connessione di rete fra il dominio dell'organizzazione e il provider di hosting è abilitata. Finché il valore non è impostato su True, le due organizzazioni non potranno scambiarsi messaggi. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledSharedAddressSpace</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il provider di hosting viene utilizzato nello scenario di un dominio combinato. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>HostsOCSUsers</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il provider di hosting è utilizzato per ospitare gli account di Lync Server. Se impostato su False, indica che il provider ospita altri tipi di account, ad esempio gli account Microsoft Exchange. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco del provider di hosting da creare. L'identità è un valore stringa, ad esempio, può essere il nome di dominio completo (FQDN) del provider di hosting (ad esempio fabrikam.com) o il nome dell'azienda che fornisce i servizi (Fabrikam, Inc.).</p>
<p>Le identità dei provider di hosting devono essere univoche. Il comando avrà esito negativo se si tenta di creare un nuovo provider di hosting quando esiste già un provider con la stessa identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo del server proxy utilizzato dal provider di hosting. Questo valore non può essere modificato. Se il provider di hosting cambia server proxy o se si commette un errore durante la prima specifica del nome di dominio completo del proxy è necessario eliminare e ricreare la voce per il provider.</p></td>
</tr>
<tr class="even">
<td><p><em>AutodiscoverUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL per il servizio di individuazione automatica utilizzato da un provider di hosting che ospita account di Lync Server. Il servizio di individuazione automatica consente alle applicazioni client di determinare la modalità di accesso alle risorse, ad esempio il pool principale di un utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>IsLocal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il server proxy utilizzato dal provider di hosting è contenuto all'interno della propria topologia di Lync Server. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipClientPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Porta utilizzata dal provider per la comunicazione con i client SIP. Il valore predefinito è 443. Per impostazione predefinita, il parametro SipClientPort non viene visualizzato quando si esegue il cmdlet <strong>Get-CsHostingProvider</strong>. Per visualizzarlo, utilizzare un comando simile al seguente:</p>
<p>Get-CsHostingProvider | Select-Object *</p></td>
</tr>
<tr class="even">
<td><p><em>VerificationLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>Indica il livello di verifica consentito per i messaggi inviati e ricevuti dal provider ospitato. È necessario impostare VerificationLevel su uno dei seguenti valori:</p>
<p>AlwaysVerifiable. Indica che tutti i messaggi inviati dal provider di hosting sono considerati verificabili. Ciò significa che nessuno dei messaggi provenienti dal provider di hosting verrà rifiutato.</p>
<p>AlwaysUnverifiable. Indica che tutti i messaggi inviati dal provider di hosting sono considerati non verificabili. I messaggi verranno trasmessi solo se l'utente del provider di hosting è incluso nell'elenco contatti.</p>
<p>UseSourceVerification. Si basa sul livello di verifica incluso nei messaggi inviati dal provider di hosting. Se il livello non è specificato, il messaggio verrà rifiutato in quanto non verificabile.</p>
<p>Il valore predefinito è AlwaysVerifiable.</p></td>
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

Nessuno. Il cmdlet **New-CsHostingProvider** non accetta input tramite pipeline.

## Tipi restituiti

Consente di creare nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

