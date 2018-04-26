---
title: Set-CsWebServiceConfiguration
TOCTitle: Set-CsWebServiceConfiguration
ms:assetid: 5aa0316d-afd8-4cc2-b606-0e720e6ab021
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398396(v=OCS.15)
ms:contentKeyID: 49300677
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWebServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2014-06-05_

Modifica una raccolta esistente di impostazioni di configurazione dei servizi Web. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsWebServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsWebServiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowAnonymousAccessToLWAConference <$true | $false>] [-AllowExternalAuthentication <$true | $false>] [-AutoLaunchLyncWebAccess <$true | $false>] [-CASigningKeyLength <UInt64>] [-Confirm [<SwitchParameter>]] [-CrossDomainAuthorizationList <PSListModifier>] [-DefaultValidityPeriodHours <UInt64>] [-EnableCertChainDownload <$true | $false>] [-EnableGroupExpansion <$true | $false>] [-Force <SwitchParameter>] [-InferCertChainFromSSL <$true | $false>] [-MACResolverUrl <String>] [-MaxCSRKeySize <UInt64>] [-MaxGroupSizeToExpand <UInt32>] [-MaxValidityPeriodHours <UInt64>] [-MinCSRKeySize <UInt64>] [-MinValidityPeriodHours <UInt64>] [-SecondaryLocationSourceUrl <String>] [-ShowAlternateJoinOptionsExpanded <$true | $false>] [-ShowDownloadCommunicatorAttendeeLink <$true | $false>] [-ShowJoinUsingLegacyClientLink <$true | $false>] [-TrustedCACerts <PSListModifier>] [-UseCertificateAuth <$true | $false>] [-UseDomainAuthInLWA <$true | $false>] [-UsePinAuth <$true | $false>] [-UseWindowsAuth <None | Negotiate | NTLM>] [-UseWsFedPassiveAuth <$true | $false>] [-WhatIf [<SwitchParameter>]] [-WsFedPassiveMetadataUri <String>]

## Esempi

## ESEMPIO 1

Nell'Esempio 1, viene abilitata l'espansione dei gruppi per le impostazioni di configurazione di servizi Web applicate al sito Redmond (-Identity site:Redmond). Per ottenere questo risultato, si specifica la proprietà EnableGroupExpansion e si imposta il parametro su True.

    Set-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $True

## ESEMPIO 2

Nell'esempio 2 il periodo massimo di validità per tutte le impostazioni di configurazione di servizi Web applicate nell'ambito del sito viene impostato su 16 ore. A tale scopo, viene prima chiamato il cmdlet **Get-CsWebServiceConfiguration** insieme al parametro Filter. Il filtro "site:\*" restituisce solo i dati relativi alle impostazioni la cui identità (Identity) inizia con i caratteri "site:". Questa raccolta quindi viene inviata tramite pipe al cmdlet **Set-CsWebServiceConfiguration**, che imposta il valore 16 per la proprietà MaxValidityPeriodHours di ogni singolo elemento della raccolta.

    Get-CsWebServiceConfiguration -Filter "site:*" | Set-CsWebServiceConfiguration -MaxValidityPeriodHours 16

## ESEMPIO 3

Nell'esempio 3 la dimensione di espansione gruppo è impostata su 400 per ogni raccolta di impostazioni di configurazione dei servizi Web per cui è consentita l'espansione gruppo. A tale scopo, viene chiamato il cmdlet **Get-CsWebServiceConfiguration** senza alcun parametro aggiuntivo in modo da restituire una raccolta di tutte le impostazioni di configurazione dei servizi Web utilizzate nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableGroupExpansion equivale a True. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsWebServiceConfiguration**, che imposta il valore 400 per la proprietà MaxGroupSizeToExpand di ogni singolo elemento della raccolta.

    Get-CsWebServiceConfiguration | Where-Object {$_.EnableGroupExpansion -eq $True} | Set-CsWebServiceConfiguration -MaxGroupSizeToExpand 400

## ESEMPIO 4

Il comando riportato nell'esempio 4 mostra come le impostazioni globali dei servizi Web possono essere configurate in modo che a ogni persona che partecipa a una riunione utilizzando un'applicazione client diversa da Lync venga prima mostrato un collegamento a un sito dove è possibile scaricare Lync Web App. Per ottenere questo risultato, viene incluso il parametro ShowDownloadCommunicatorAttendeeLink impostandolo su True.

    Set-CsWebServiceConfiguration -Identity global -ShowDownloadCommunicatorAttendeeLink $True 

## ESEMPIO 5

I comandi illustrati nell'esempio 5 aggiungono il dominio http://fabrikam.com a una raccolta esistente di impostazioni di configurazione dei servizi Web. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsWebOrigin** per creare un oggetto dominio per fabrikam.com. L'oggetto dominio risultante viene archiviato in una variabile denominata $x.

Nel secondo comando nell'esempio viene utilizzato il cmdlet **Set-CsWebServiceConfiguration** per aggiungere http://fabrikam.com alle impostazioni di configurazione dei servizi Web applicate al sito Redmond. La sintassi @{Add=$x} aggiunge il dominio ai domini già presenti nella raccolta di domini autorizzati per l'esecuzione di script tra domini. Per sostituire una raccolta esistente solo con http://fabrikam.com, utilizzare la sintassi @{Replace=$x}.

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    Set-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList @{Add=$x}

## ESEMPIO 6

Nell'esempio 6 il primo dominio elencato nella raccolta di domini autorizzati per l'esecuzione di script tra domini viene rimosso dalle impostazioni di configurazione dei servizi Web per il sito Redmond. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-CsWebServiceConfiguration** per restituire le impostazioni correnti per il sito Redmond. Questi valori vengono archiviati in una variabile denominata $x.

Nel secondo comando viene utilizzato il metodo RemoveAt per rimuovere il primo dominio dalla proprietà CrossDomainAuthorizationList. I domini vengono archiviati in questa proprietà come matrici. Al primo dominio è assegnato un numero di indice 0, al secondo è assegnato un numero di indice 1 e così via. Per rimuovere il secondo dominio (numero di indice 1) dalla proprietà CrossDomainAuthorizationList, utilizzare la sintassi seguente:

$x.CrossDomainAuthorizationList.RemoveAt(1)

Si noti che il comando 2 rimuove il dominio dalla copia del sito Redmond archiviata nella variabile $x e non dal sito stesso. Per rimuovere effettivamente il dominio dal sito Redmond, il terzo comando dell'esempio utilizza il cmdlet **Set-CsWebServiceConfiguration** e il parametro Instance per sovrascrivere le impostazioni per il sito Redmond con le impostazioni archiviate in $x.

    $x = Get-CsWebServiceConfiguration -Identity "site:Redmond"
    $x.CrossDomainAuthorizationList.RemoveAt(0)
    Set-CsWebServiceConfguration -Instance $x

## ESEMPIO 7

Il comando illustrato nell'esempio 7 modifica le impostazioni di configurazione dei servizi Web per il sito Redmond rimuovendo tutti i domini autorizzati per l'esecuzione di script tra domini. A tale scopo, viene impostata la proprietà CrossDomainAuthorizationList su un valore Null ($Null).

    Set-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $Null

## Descrizione dettagliata

Molti componenti di Lync Server sono basati sul Web: questi componenti utilizzano i servizi Web o le pagine Web per eseguire le attività. Gli utenti utilizzano ad esempio un servizio Web quando cercano nuovi contatti nella Rubrica o quando utilizzano l'espansione gruppo per visualizzare i singoli membri di un gruppo di distribuzione. Analogamente, componenti quali le conferenza telefoniche con accesso esterno e il Pannello di controllo di Lync Server utilizzano le pagine Web come interfaccia tra Lync Server e gli utenti.

I cmdlet **CsWebServiceConfiguration** consentono agli amministratori di gestire le impostazioni di configurazione dei servizi Web per tutta l'organizzazione. Questo include anche la gestione di espansione gruppo, delle impostazioni dei certificati e dei metodi di autenticazione consentiti. Poiché è possibile configurare impostazioni diverse nell'ambito globale, del sito e del servizio (sebbene solo per i servizi Web), è possibile personalizzare le funzionalità dei servizi Web per utenti diversi e posizioni diverse. I cmdlet **CsWebServiceConfiguration** consentono agli amministratori di gestire le impostazioni di configurazione dei servizi Web in tutta l'organizzazione. Questo include anche la gestione di espansione gruppo, delle impostazioni dei certificati e dei metodi di autenticazione consentiti. Poiché è possibile configurare impostazioni diverse nell'ambito globale, del sito e del servizio (solo per i servizi Web), è possibile personalizzare le funzionalità dei servizi Web per utenti diversi e posizioni diverse.

È possibile specificare impostazioni personalizzate (ad esempio, periodi di validità personalizzati per i certificati) nel momento in cui si crea una nuova raccolta di impostazioni di configurazione di servizi Web. In alternativa, è possibile modificare le proprietà di una raccolta esistente utilizzando il cmdlet **Set-CsWebServiceConfiguration**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsWebServiceConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsWebServiceConfiguration"}

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
<td><p><em>AllowAnonymousAccessToLWAConference</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, gli utenti anonimi possono partecipare a conferenze di Lync Web App.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExternalAuthentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True (valore predefinito), è possibile utilizzare l'autenticazione OAuth per autenticare gli utenti esterni.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AutoLaunchLyncWebAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>L'utilizzo di questo parametro è deprecato con la versione locale di Lync Server 2013.</p>
<p>Se si imposta questo parametro su True, verrà utilizzato automaticamente Lync Web App come popup Web predefinito per partecipare a una conferenza online, purché vengano soddisfatti i prerequisiti per l'utilizzo di Lync Web App, ad esempio l'installazione di Silverlight e la visualizzazione delle finestre popup in Internet Explorer.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>CASigningKeyLength</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Impostare la dimensione della chiave di firma CA, la chiave privata utilizzata da una CA per firmare i certificati digitali. La lunghezza della chiave di firma può essere impostata su qualsiasi numero intero compreso tra 2048 e 16384 byte; il valore predefinito è 2048.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CrossDomainAuthorizationList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di domini autorizzati a ospitare applicazioni Web che inviano richieste di script tra domini alla distribuzione di Lync Server 2013.</p>
<p>I domini da aggiungere all'elenco devono essere creati utilizzando il cmdlet New-CsWebOrigin e quindi aggiunti alla nuova raccolta di impostazioni di configurazione dei servizi Web. Si noti inoltre che è necessario anteporre il prefisso http: o https: ai nomi dei domini. Per ulteriori informazioni, vedere gli esempi 5, 6 e 7 in questo argomento della Guida.</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultValidityPeriodHours</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Quando si utilizza l'autenticazione del certificato, i client possono richiedere il periodo di validità del certificato (in ore). DefaultValidityPeriodHours rappresenta il tempo di validità di un certificato se il client non ne richiede uno personalizzato.</p>
<p>DefaultValidityPeriodHours può essere un qualsiasi valore intero compreso tra 8 e 8760 ore (pari a 365 giorni). Il valore predefinito è 4320 (180 giorni).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCertChainDownload</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True, i server a cui viene presentato un certificato di autenticazione scaricheranno la catena di certificati per tale certificato. La catena di certificati rintraccia un singolo certificato fino all'Autorità di certificazione (CA) che lo ha emesso. I certificati non saranno accettati per l'autenticazione se l'Autorità di certificazione del certificato non è considerata attendibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableGroupExpansion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, l'espansione gruppo sarà abilitata in Lync. Con l'espansione gruppo, gli utenti possono configurare un gruppo di distribuzione come contatto e quindi &quot;espandere&quot; il gruppo. Dopo l'espansione di un gruppo, gli utenti possono vedere i singoli membri di un gruppo e le relative informazioni sulla presenza.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione di servizi Web da modificare. Per modificare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per modificare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Per modificare le impostazioni configurate nell'ambito globale, utilizzare la sintassi seguente: -identity global.</p>
<p>Se non viene utilizzato il parametro Identity, il cmdlet <strong>Set-CsWebServiceConfiguration</strong> modificherà automaticamente la raccolta globale.</p></td>
</tr>
<tr class="even">
<td><p><em>InferCertChainFromSSL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True, i server utilizzeranno le informazioni del certificato incluse nel protocollo SSL (Secure Sockets Layer) per determinare l'Autorità di certificazione emittente. I certificati non saranno accettati per l'autenticazione se l'Autorità di certificazione del certificato non è considerata attendibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto WebServiceSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MACResolverUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL di un servizio Web in grado di eseguire la risoluzione MAC (Media Access Control). La risoluzione MAC consiste nell'utilizzare l'indirizzo MAC di un client connesso e nel restituire gli ID di porta e di chassis del commutatore di rete a cui è connesso il client. La risoluzione MAC viene utilizzata dal servizio di chiamate di emergenza Enhanced 9-1-1.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCSRKeySize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Consente di impostare la dimensione massima della chiave di richiesta di firma del certificato (CSR). Una richiesta CSR è un messaggio inviato da un richiedente a una CA per richiedere un certificato digitale. La dimensione di una chiave CSR può essere impostata su qualsiasi numero intero compreso tra 1024 e 16384 byte. Il valore predefinito è 16384.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxGroupSizeToExpand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Rappresenta il numero massimo di persone che verrà visualizzato quando si espande un gruppo. Ad esempio, se MaxGroupSizeToExpand è impostato su 75, verranno visualizzati solo i primi 75 membri del gruppo ogni volta che il gruppo viene espanso.</p>
<p>MaxGroupSizeToExpand può essere impostata su qualsiasi valore intero compreso tra 1 e 1000 (compresi). Il valore predefinito è 100.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxValidityPeriodHours</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Quando si utilizza l'autenticazione del certificato, i client possono richiedere il periodo di validità del certificato (in ore). MaxValidityPeriodHours rappresenta il tempo massimo in cui un client può effettuare la richiesta.</p>
<p>MaxValidityPeriodHours può essere un qualsiasi valore intero compreso tra 8 e 8760 ore (pari a 365 giorni). Il valore predefinito è 8760.</p></td>
</tr>
<tr class="even">
<td><p><em>MinCSRKeySize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Consente di impostare la dimensione minima della chiave CSR (Certificate Signing Request). La dimensione minima può essere impostata su qualsiasi valore intero compreso tra 1024 e 16384. Il valore predefinito è 16384.</p></td>
</tr>
<tr class="odd">
<td><p><em>MinValidityPeriodHours</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Quando si utilizza l'autenticazione del certificato, i client possono richiedere il periodo di validità del certificato (in ore). MinValidityPeriodHours rappresenta il tempo minimo in cui un client può effettuare la richiesta.</p>
<p>MinValidityPeriodHours può essere un qualsiasi valore intero compreso tra 8 e 4320 ore (pari a 180 giorni). Il valore predefinito è 8.</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLocationSourceUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL di un servizio Web in grado di elaborare una richiesta di percorso. Questo servizio viene utilizzato solo quando le richieste di percorso non possono essere risolte localmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowAlternateJoinOptionsExpanded</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>L'utilizzo di questo parametro è deprecato con la versione locale di Lync Server 2013.</p>
<p>Se si imposta questo parametro su True, verranno espanse e visualizzate automaticamente agli utenti opzioni alternative per partecipare a una conferenza online, ad esempio Office Communicator 2007 R2. Se invece si imposta il parametro su False (valore predefinito), queste opzioni saranno comunque disponibili, ma l'utente dovrà visualizzare manualmente l'elenco.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDownloadCommunicatorAttendeeLink</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>L'utilizzo di questo parametro è deprecato con la versione locale di Lync Server 2013.</p>
<p>Se l'impostazione è True (valore predefinito), gli utenti che partecipano a una riunione online utilizzando un'applicazione client diversa da Lync visualizzeranno un collegamento che punta al download di Lync Web App.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowJoinUsingLegacyClientLink</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>L'utilizzo di questo parametro è deprecato con la versione locale di Lync Server 2013.</p>
<p>Se impostato su True, gli utenti che accedono a una riunione con un'applicazione client diversa da Lync avranno la possibilità di accedere alla riunione con l'applicazione client utilizzata. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedCACerts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di certificati che rappresenta le catene di certificati considerati attendibili dal server Web. I nuovi certificati aggiunti alla raccolta devono essere creati con il cmdlet <strong>New-CsWebTrustedCACertificate</strong>.</p>
<p>La raccolta non viene utilizzata se la proprietà InferCertChainFromSSL è impostata su True.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCertificateAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (il valore predefinito), i client possono essere autenticati con i certificati. Impostare questo valore su False per disabilitare l'autenticazione dei certificati.</p></td>
</tr>
<tr class="even">
<td><p><em>UseDomainAuthInLWA</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, è possibile usare l'autenticazione di dominio come sistema di autenticazione per gli utenti di Lync Web App.</p></td>
</tr>
<tr class="odd">
<td><p><em>UsePinAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (il valore predefinito), i client possono essere autenticati con i numeri PIN. Impostare questo valore su False per disabilitare l'autenticazione dei PIN.</p></td>
</tr>
<tr class="even">
<td><p><em>UseWindowsAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Web.UseWindowsAuth</p></td>
<td><p>Determina se e come saranno autenticati gli utenti utilizzando l'autenticazione di Windows, vale a dire impiegando le stesse credenziali utilizzate per l'accesso a Windows. I valori validi sono:</p>
<p>Negotiate: il client e il server collaborano per determinare il protocollo di autenticazione appropriato (Kerberos o NTLM).</p>
<p>NTLM: l'autenticazione di Windows è consentita solo utilizzando il protocollo NTLM.</p>
<p>None: l'autenticazione di Windows non è consentita.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseWsFedPassiveAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, viene consentita l'autenticazione passiva, ovvero l'autenticazione degli utenti mediante reindirizzamento dell'URL o l'utilizzo di collegamenti intelligenti. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>WsFedPassiveMetadataUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URI utilizzato dal protocollo del richiedente Web WS-federation.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings. Il cmdlet **Set-CsWebServiceConfiguration** accetta gli input tramite pipeline dell'oggetto impostazioni dei servizi Web.

## Tipi restituiti

Il cmdlet **Set-CsWebServiceConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)

