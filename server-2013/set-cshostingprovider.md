---
title: Set-CsHostingProvider
TOCTitle: Set-CsHostingProvider
ms:assetid: 709567e3-1af6-4829-b9ce-5f488f9db372
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398532(v=OCS.15)
ms:contentKeyID: 49300934
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsHostingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un provider di hosting attualmente in uso nella propria organizzazione. Un provider di hosting è un'organizzazione di terze parti che fornisce servizi di messaggistica istantanea, informazioni sulla presenza e altri servizi correlati a un dominio con il quale si desidera attuare una federazione. I provider di hosting come Microsoft Lync Online 2010 si differenziano dai provider pubblici, ad esempio Yahoo\!, MSN e AOL, in quanto non offrono servizi al pubblico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsHostingProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutodiscoverUrl <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-EnabledSharedAddressSpace <$true | $false>] [-Force <SwitchParameter>] [-HostsOCSUsers <$true | $false>] [-IsLocal <$true | $false>] [-SipClientPort <UInt64>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene modificato il provider di hosting con l'identità Fabrikam.com. In questo esempio la proprietà VerificationLevel è impostata su AlwaysUnverifiable.

    Set-CsHostingProvider -Identity "Fabrikam.com" -VerificationLevel "AlwaysUnverifiable"

## ESEMPIO 2

Nell'esempio 2 è riportata una variazione del comando mostrato nell'esempio 1; in questo caso, tuttavia, il livello di verifica per tutti i provider di hosting è impostato su AlwaysUnverifiable. Per ottenere tale risultato, viene utilizzato innanzitutto **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting configurati per l'utilizzo nell'organizzazione. La raccolta viene inviata tramite pipe a **Set-CsHostingProvider**, che modifica la proprietà VerificationLevel di tutti provider contenuti nella raccolta.

    Get-CsHostingProvider | Set-CsHostingProvider -VerificationLevel "AlwaysUnverifiable"

## ESEMPIO 3

Nell'esempio 3 tutti i provider di hosting attualmente configurati per l'utilizzo nell'impostazione di un dominio combinato vengono modificati in modo tale da non poter più essere utilizzati per la federazione con dominio combinato. In questo esempio, viene per prima cosa chiamato **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider che soddisfano due criteri: 1) la proprietà HostsOCSUsers equivale a True; 2) la proprietà EnabledSharedAddressSpace è uguale a True. Questa raccolta filtrata viene quindi inviata tramite pipe a **Set-CsHostingProvider**, che a sua volta imposta entrambe le proprietà EnabledSharedAddressSpace e HostsOCSUsers su False. Una volta effettuata questa operazione, tutti i provider di hosting della raccolta risultano abilitati per la federazione, tuttavia, non potranno più essere utilizzati nello scenario di un dominio combinato.

    Get-CsHostingProvider | Where-Object {$_.EnabledSharedAddressSpace -eq $True -and $_.HostsOCSUsers -eq $True} | Set-CsHostingProvider -EnabledSharedAddressSpace $False -HostsOCSUsers $False

## Descrizione dettagliata

La federazione è un mezzo attraverso il quale due organizzazioni possono stabilire una relazione di trust per agevolare la comunicazione tra i due gruppi. Quando viene stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere le notifiche di presenza e comunicare tra loro in altri modi utilizzando le applicazioni SIP, ad esempio Microsoft Lync 2013. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni, 2) federazione tra un'organizzazione e un provider pubblico e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

Un provider di hosting è un'organizzazione che fornisce servizi di comunicazione SIP ad altre organizzazioni, ad esempio Fabrikam, Inc. può ospitare utenti di Contoso, Northwind Traders e Wingtip Toys. Quando si stabilisce una relazione di federazione con un provider di hosting, si definisce in realtà una federazione con tutte le organizzazioni ospitate da quel provider. Ad esempio, se un'organizzazione si associa tramite federazione a Fabrikam, gli utenti dell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Contoso, Northwind Traders e Wingtip Toys.

I provider di hosting vengono inoltre utilizzati in scenari di dominio diviso. In uno scenario di questo tipo alcuni utenti di Lync Server hanno gli account ospitati in locale, ovvero ospitati nell'implementazione locale di Lync Server. Altri utenti dispongono invece di account gestiti in remoto dal provider di hosting di terze parti. La federazione con il provider di hosting consente agli utenti in locale e in remoto di comunicare tra loro.

Per attuare la federazione con un provider di hosting di terze parti è necessario creare e abilitare un nuovo provider di hosting. Inoltre, il provider di terze parti dovrà creare una relazione di federazione con la propria organizzazione. Una volta creato un provider di hosting, è possibile utilizzare il cmdlet **Set-CsHostingProvider** per modificarne le proprietà. Ad esempio, è possibile utilizzare questo cmdlet per modificare il nome di dominio completo (FQDN) del server proxy del provider oppure per modificare il livello di verifica del provider.

Non è possibile attuare la federazione con un provider di hosting se gli server perimetrali sono configurati per utilizzare il routing predefinito anziché il routing del server DNS (Domain Name System).

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsHostingProvider** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsHostingProvider"}

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
<td><p><em>AutodiscoverUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL per il servizio di individuazione automatica utilizzato da un provider di hosting che ospita Lync Server. Il servizio di individuazione automatica consente alle applicazioni client come Microsoft Lync Mobile di determinare la modalità di accesso alle risorse, come il pool principale di un utente.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la connessione di rete fra il dominio dell'organizzazione e il provider di hosting è abilitata. Finché il valore non è impostato su True, le due organizzazioni non potranno scambiarsi messaggi. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledSharedAddressSpace</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il provider di hosting viene utilizzato nello scenario di un dominio combinato. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>HostsOCSUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il provider di hosting viene utilizzato per ospitare gli account di Lync Server. Se impostato su False, indica che il provider ospita altri tipi di account, ad esempio account di Microsoft Exchange Server. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Un identificatore univoco per il provider di hosting da modificare. L'identità può essere il nome di dominio completo (FQDN) del provider di hosting (ad esempio fabrikam.com) o il nome dell'azienda che fornisce i servizi (Fabrikam, Inc.).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DisplayHostingProvider</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>IsLocal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il server proxy utilizzato dal provider di hosting è contenuto all'interno della propria topologia di Lync Server. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>SipClientPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Porta utilizzata dal provider per la comunicazione con i client SIP. Il valore predefinito è 443. Per impostazione predefinita, il parametro SipClientPort non viene visualizzato quando si esegue il cmdlet Get-CsHostingProvider. Per visualizzarlo, utilizzare un comando simile al seguente:</p>
<p>Get-CsHostingProvider | Select-Object *</p></td>
</tr>
<tr class="odd">
<td><p><em>VerificationLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>Indica il livello di verifica consentito per i messaggi inviati e ricevuti dal provider ospitato. È necessario impostare VerificationLevel su uno dei seguenti valori:</p>
<p>AlwaysVerifiable. Indica che tutti i messaggi inviati dal provider di hosting sono considerati verificabili. Ciò significa che nessuno dei messaggi provenienti dal provider di hosting verrà rifiutato.</p>
<p>AlwaysUnverifiable. Indica che tutti i messaggi inviati dal provider di hosting sono considerati non verificabili. I messaggi verranno trasmessi solo se l'utente del provider di hosting è incluso nell'elenco contatti.</p>
<p>UseSourceVerification. Si basa sul livello di verifica incluso nei messaggi inviati dal provider di hosting. Se il livello non è specificato, il messaggio verrà rifiutato in quanto non verificabile.</p>
<p>Il valore predefinito è AlwaysVerifiable.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider. **Set-CsHostingProvider** consente di accettare le istanze da pipeline dell'oggetto provider di hosting.

## Tipi restituiti

**Set-CsHostingProvider** non restituisce alcun oggetto o valore. Il cmdlet, invece, consente di configurare le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)

