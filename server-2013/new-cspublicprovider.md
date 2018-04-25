---
title: New-CsPublicProvider
TOCTitle: New-CsPublicProvider
ms:assetid: 0b2dcb40-13f8-4ce6-b537-527d34895ceb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398161(v=OCS.15)
ms:contentKeyID: 49299638
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una relazione federativa con un nuovo provider pubblico. Un provider pubblico è un'organizzazione che offre al grande pubblico servizi di messaggistica istantanea, presenza e altri servizi correlati. Lync Server viene fornito con tre provider pubblici configurati, ma non abilitati: Yahoo, AIM (AOL) e Messenger (MSN). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> -Enabled <$true | $false> -ProxyFqdn <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-IconUrl <String>] [-InMemory <SwitchParameter>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare una nuova relazione federativa con un provider pubblico con Identity Fabrikam. Oltre a specificare l'identità, occorre impostare anche altri due valori di proprietà e i corrispondenti parametri: ProxyFqdn (impostato su proxyserver.fabrikam.com) e Enabled (che, in questo caso, è impostato su True).

    New-CsPublicProvider -Identity "Fabrikam" -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True

## ESEMPIO 2

L'Esempio 2 dimostra come sia possibile creare un nuovo provider pubblico solo in memoria, modificarne le proprietà e quindi trasformare quel provider virtuale in un vero provider che può essere effettivamente utilizzato dall'organizzazione. A tal fine, il primo comando nell'esempio crea un provider pubblico con Identity Fabrikam. Oltre a includere i parametri necessari (–Identity, -ProxyFqdn e –Enabled), il comando aggiunge il parametro -InMemory; questo parametro crea solo in memoria un'istanza del provider, che viene quindi memorizzata in una variabile denominata $x.

Dopo la creazione dell'istanza del provider solo in memoria, il secondo comando dell'esempio modifica il valore VerificationLevel del provider virtuale. L'ultimo comando infine utilizza il cmdlet **Set-CsPublicProvider** per trasformare il provider virtuale, archiviato nella variabile $x, in un provider pubblico effettivo. Se non si chiama il cmdlet **Set-CsPublicProvider**, il provider effettivo non verrà creato. A sua volta, il provider virtuale verrà eliminato al momento della chiusura della sessione di Windows PowerShell o quando si elimina la variabile $x.

    $x = New-CsPublicProvider -Identity "Fabrikam" -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True -InMemory
    $x.VerificationLevel = "AlwaysUnverifiable"
    Set-CsPublicProvider -Instance $x

## Descrizione dettagliata

La federazione consente di stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Quando si attua una federazione, gli utenti delle due organizzazioni federate possono inviarsi messaggi istantanei, sottoscrivere servizi di notifica della presenza e comunicare in altro modo utilizzando applicazioni SIP come Lync 2013. Lync Server consente tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

Un provider pubblico è un'organizzazione che fornisce servizi di comunicazione SIP al pubblico. Quando si attua una federazione con un provider pubblico, la federazione viene in realtà estesa a chiunque disponga di un account ospitato da tale provider. Se ad esempio si attua una federazione con Messenger (MSN), gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di messaggistica istantanea Messenger.

Per federarsi con un provider di pubblico, è necessario creare e abilitare un nuovo provider pubblico. A sua volta, il provider pubblico dovrà creare una relazione federativa con la nuova organizzazione. Il cmdlet **Set-CsPublicProvider** consente di modificare i valori delle proprietà di tutti i provider pubblici configurati per l'utilizzo nella propria organizzazione.

Non è possibile stabilire una federazione con un provider pubblico se i propri Edge Server sono configurati per utilizzare il routing predefinito anziché il routing del server DNS.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsPublicProvider** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPublicProvider"}

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
<td><p>Indica se la relazione federativa tra l'organizzazione e il provider pubblico è attiva o meno. Se impostato su True, gli utenti dell'organizzazione saranno in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che hanno account ospitati dal provider pubblico. Se impostato su False, gli utenti dell'organizzazione non saranno in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che hanno account ospitati dal provider pubblico. È possibile abilitare e disabilitare le relazioni federative in qualsiasi momento utilizzando rispettivamente il cmdlet <strong>Enable-CsPublicProvider</strong> e il cmdlet <strong>Disable-CsPublicProvider</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il provider pubblico da creare. Il valore di questo parametro corrisponde in genere al nome del sito Web che fornisce i servizi, ad esempio Yahoo!, AOL o MSN.</p>
<p>Le identità devono essere univoche non solo nell'ambito dei provider pubblici, ma anche nell'ambito dei provider di hosting. Si supponga di creare un nuovo provider pubblico con Identity Fabrikam. Il comando utilizzato avrà esito negativo in presenza di un provider pubblico o di hosting che abbia già quell'identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Specifica il nome di dominio completo (FQDN), ad esempio proxyserver.fabrikam.com, del server proxy utilizzato dal provider pubblico.</p>
<p>Gli FQDN proxy devono essere univoci non solo nell'ambito dei provider pubblici, ma anche nell'ambito dei provider di hosting. Ad esempio, si supponga di creare un nuovo provider pubblico con FQDN proxy proxyserver.fabrikam.com. Questo comando avrà esito negativo, se esiste già un provider pubblico o di hosting con quello stesso FQDN proxy.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>IconUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL dell'icona utilizzata per indicare un contatto Microsoft Skype.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>VerificationLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>Indica come o se i messaggi inviati dal provider pubblico devono essere verificati per accertare che provengano effettivamente da quel provider. La proprietà VerificationLevel deve essere impostata su uno dei seguenti valori:</p>
<p>AlwaysVerifiable. Verranno accettati tutti i messaggi che risultano inviati da questo provider. Se nel messaggio non viene rilevata alcuna intestazione di verifica, questa verrà aggiunta da Lync Server. Questo è il valore predefinito.</p>
<p>AlwaysUnverifiable. Tutti i messaggi che risultano inviati da un provider pubblico vengono considerati non verificati. Verranno recapitati solo se inviati da una persona inclusa nell'elenco contatti del destinatario. Se ad esempio Ken Myer è incluso nell'elenco contatti di un utente, tale utente potrà ricevere i messaggi inviati da Ken Myer. Se Pilar Ackerman non è inclusa nell'elenco contatti dell'utente, l'utente non sarà in grado di ricevere i relativi messaggi. Si noti che gli utenti di Lync 2013 possono sostituire manualmente questa impostazione, abilitando la ricezione di messaggi da persone non incluse nel rispettivo elenco contatti.</p>
<p>UseSourceVerification. Utilizza l'intestazione di verifica aggiunta al messaggio dal provider pubblico. Se mancano le informazioni di verifica, il messaggio verrà rifiutato. L'utilizzo di questo valore è deprecato in Lync Server 2013.</p></td>
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

Nessuno. Il cmdlet **New-CsPublicProvider** non accetta input da pipeline.

## Tipi restituiti

Consente di creare nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

