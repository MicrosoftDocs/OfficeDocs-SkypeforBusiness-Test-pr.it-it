---
title: New-CsWebServiceConfiguration
TOCTitle: New-CsWebServiceConfiguration
ms:assetid: 6225cf8d-b669-464e-9848-a292953e3a3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398440(v=OCS.15)
ms:contentKeyID: 49300765
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2014-06-05_

Crea una nuova raccolta di impostazioni di configurazione dei servizi Web. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsWebServiceConfiguration -Identity <XdsIdentity> [-AllowAnonymousAccessToLWAConference <$true | $false>] [-AllowExternalAuthentication <$true | $false>] [-AutoLaunchLyncWebAccess <$true | $false>] [-CASigningKeyLength <UInt64>] [-Confirm [<SwitchParameter>]] [-CrossDomainAuthorizationList <PSListModifier>] [-DefaultValidityPeriodHours <UInt64>] [-EnableCertChainDownload <$true | $false>] [-EnableGroupExpansion <$true | $false>] [-Force <SwitchParameter>] [-InferCertChainFromSSL <$true | $false>] [-InMemory <SwitchParameter>] [-MACResolverUrl <String>] [-MaxCSRKeySize <UInt64>] [-MaxGroupSizeToExpand <UInt32>] [-MaxValidityPeriodHours <UInt64>] [-MinCSRKeySize <UInt64>] [-MinValidityPeriodHours <UInt64>] [-SecondaryLocationSourceUrl <String>] [-ShowAlternateJoinOptionsExpanded <$true | $false>] [-ShowDownloadCommunicatorAttendeeLink <$true | $false>] [-ShowJoinUsingLegacyClientLink <$true | $false>] [-TrustedCACerts <PSListModifier>] [-UseCertificateAuth <$true | $false>] [-UseDomainAuthInLWA <$true | $false>] [-UsePinAuth <$true | $false>] [-UseWindowsAuth <None | Negotiate | NTLM>] [-UseWsFedPassiveAuth <$true | $false>] [-WhatIf [<SwitchParameter>]] [-WsFedPassiveMetadataUri <String>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 crea una nuova raccolta delle impostazioni di configurazione di servizi Web per il sito Redmond (-Identity site:Redmond). L'esempio include due parametri opzionali: EnableGroupExpansion, impostato su False ($False), e UseCertificateAuth, impostato su True ($True). Questi due parametri sono utilizzati rispettivamente per disabilitare l'espansione gruppo e abilitare l'utilizzo dei certificati per l'autenticazione.

Il comando avrà esito negativo se per il sito Redmond è già stata creata una raccolta di impostazioni di configurazione di servizi Web, poiché i siti sono limitati a una singola raccolta di impostazioni di configurazione di servizi Web.

    New-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $False -UseCertificateAuth $True

## ESEMPIO 2

L'esempio 2 è una variante del comando mostrato nell'esempio 1. In questo caso però la nuova raccolta di impostazioni di configurazione dei servizi Web viene creata inizialmente solo in memoria e applicata al sito Redmond soltanto in un secondo momento. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsWebServiceConfiguration** per creare una raccolta di impostazioni per il sito Redmond. Il parametro InMemory viene incluso per garantire che la raccolta venga creata solo in memoria, senza essere immediatamente applicata al sito Redmond. Dal momento che le impostazioni esistono solo in memoria, è necessario archiviarle in una variabile, in questo caso una variabile denominata $x.

Con i comandi 2 e 3 nell'esempio vengono recuperate le impostazioni di configurazione virtuali e vengono modificati i valori delle proprietà EnableGroupExpansion e UseCertificateAuth. Dopo aver apportato queste modifiche, l'ultimo comando utilizza il cmdlet **Set-CsWebServiceConfiguration** per recuperare le impostazioni virtuali e applicarle al sito Redmond. Se non si chiama il cmdlet **Set-CsWebServiceConfiguration**, le nuove impostazioni non vengono assegnate al sito. Le impostazioni di configurazione dei servizi Web virtuali invece scompariranno al termine della sessione di Windows PowerShell o all'eliminazione della variabile $x.

    $x = New-CsWebServiceConfiguration -Identity site:Redmond -InMemory
    $x.EnableGroupExpansion = $False 
    $x.UseCertificateAuth = $True
    Set-CsWebServiceConfiguration -Instance $x

## ESEMPIO 3

I comandi illustrati nell'esempio 3 aggiungono il dominio http://fabrikam.com all'elenco dei domini autorizzati per una nuova raccolta di impostazioni di configurazione di servizi Web creata per il sito Redmond. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsWebOrigin** per creare un oggetto dominio per fabrikam.com. L'oggetto dominio risultante viene archiviato in una variabile denominata $x.

Il secondo comando nell'esempio utilizza il cmdlet **New-CsWebServiceConfiguration** per creare le impostazioni di configurazione del servizio Web per il sito Redmond. La sintassi -CrossDomainAuthorizationList $x aggiunge http://fabrikam.com alla raccolta di domini autorizzati per l'esecuzione di script tra domini.

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    New-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $x

## ESEMPIO 4

Nell'esempio 4 viene illustrato come aggiungere più domini autorizzati a una nuova raccolta di impostazioni di configurazione di servizi Web. Per aggiungere più domini, è necessario creare più oggetti dominio, archiviando ognuno in una variabile separata. Nell'esempio 4 l'oggetto dominio per http://fabrikam.com viene archiviato in una variabile denominata $x, mentre l'oggetto dominio per http://contoso.com viene archiviato in una variabile denominata $y.

Dopo aver creato tutti gli oggetti dominio, è sufficiente includere ogni nome di variabile nel valore del parametro CrossDomainAuthorizationList, ad esempio:

–CrossDomainAuthorizationList $x, $y

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    $y = New-CsWebOrigin -Url "http://contoso.com"
    New-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $x, $y

## Descrizione dettagliata

Molti componenti di Lync Server sono basati sul Web: questi componenti utilizzano i servizi Web o le pagine Web per eseguire le attività. Gli utenti ad esempio utilizzano un servizio Web quando cercano nuovi contatti nella Rubrica o quando utilizzano la funzionalità di espansione gruppo per visualizzare i singoli membri di un gruppo di distribuzione. Analogamente, componenti quali le conferenze telefoniche con accesso esterno e Lync Server utilizzano le pagine Web come interfaccia tra Lync Server e gli utenti.

I cmdlet **CsWebServiceConfiguration** consentono agli amministratori di gestire le impostazioni di configurazione di servizi Web in tutta l'organizzazione. Tali impostazioni includono la gestione dell'espansione dei gruppi, delle impostazioni dei certificati e dei metodi di autenticazione consentiti. Poiché nell'ambito globale, del sito e del servizio si possono configurare impostazioni differenti, anche se solo per il servizio Servizi Web, è possibile personalizzare le funzionalità di servizi Web per utenti e postazioni differenti.

Le nuove impostazioni di configurazione di servizi Web vengono create tramite il cmdlet **New-CsWebServiceConfiguration**. Queste impostazioni possono essere create nell'ambito del sito o del servizio (e solo per il servizio Servizi Web); il comando avrà esito negativo se si tenta di creare una nuova raccolta con ambito globale. Analogamente, il comando avrà esito negativo se, ad esempio si tenta di creare una nuova raccolta nel sito Redmond che già ospita una raccolta di impostazioni del servizio Web.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsWebServiceConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWebServiceConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di servizi Web da creare. Per creare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;site:Redmond&quot;. Per creare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;. Eventuali impostazioni create nell'ambito del servizio devono essere assegnate al servizio Server Web.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowAnonymousAccessToLWAConference</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), gli utenti anonimi possono partecipare a conferenze di Lync Web App.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalAuthentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True (valore predefinito), è possibile utilizzare l'autenticazione OAuth per autenticare gli utenti esterni.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoLaunchLyncWebAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>L'utilizzo di questo parametro è deprecato con la versione locale di Lync Server 2013.</p>
<p>Se si imposta questo parametro su True, verrà utilizzato automaticamente Lync Web App come popup Web predefinito per partecipare a una conferenza online, purché vengano soddisfatti i prerequisiti per l'utilizzo di Lync Web App, ad esempio l'installazione di Silverlight e la visualizzazione delle finestre popup in Internet Explorer.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>CASigningKeyLength</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Consente di impostare la dimensione della chiave di firma dell'Autorità di certificazione, vale a dire la chiave privata utilizzata dall'Autorità per firmare i certificati digitali. La lunghezza della chiave di firma può essere qualsiasi valore intero compreso tra 2048 e 16384 byte; il valore predefinito è 2048.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CrossDomainAuthorizationList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di domini autorizzati a ospitare applicazioni Web che inviano richieste di script tra domini alla distribuzione di Lync Server 2013.</p>
<p>I domini da aggiungere all'elenco devono essere creati utilizzando il cmdlet New-CsWebOrigin e quindi aggiunti alla nuova raccolta di impostazioni di configurazione dei servizi Web. Si noti inoltre che è necessario anteporre il prefisso http: o https: ai nomi dei domini. Per ulteriori informazioni, vedere l'esempio 3 in questo argomento della Guida.</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultValidityPeriodHours</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Quando si utilizza l'autenticazione del certificato, i client possono richiedere il periodo di validità del certificato (in ore). DefaultValidityPeriodHours rappresenta il tempo di validità di un certificato se il client non ne richiede uno personalizzato.</p>
<p>DefaultValidityPeriodHours può essere un qualsiasi valore intero compreso tra 8 e 8760 ore (pari a 365 giorni). Il valore predefinito è 4320 (180 giorni).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCertChainDownload</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True, i server a cui viene presentato un certificato di autenticazione scaricheranno la catena di certificati per tale certificato. La catena di certificati rintraccia un singolo certificato fino all'Autorità di certificazione (CA) che lo ha emesso. I certificati non saranno accettati per l'autenticazione se l'Autorità di certificazione del certificato non è considerata attendibile.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableGroupExpansion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, l'espansione gruppo sarà abilitata in Lync Server. Con l'espansione gruppo, gli utenti possono configurare un gruppo di distribuzione come un contatto e quindi &quot;espandere&quot; il gruppo. Dopo l'espansione di un gruppo, gli utenti possono visualizzare tutti i singoli membri di un gruppo e le relative informazioni sulla presenza correnti.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InferCertChainFromSSL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True, i server utilizzeranno le informazioni del certificato incluse nel protocollo SSL (Secure Sockets Layer) per determinare l'Autorità di certificazione emittente. I certificati non saranno accettati per l'autenticazione se l'Autorità di certificazione del certificato non è considerata attendibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<td><p>Consente di impostare la dimensione massima della chiave di richiesta di firma del certificato (CSR). Una chiave CSR è un messaggio inviato da un richiedente a un'Autorità di certificazione per richiedere un certificato digitale. La dimensione massima può essere impostata su qualsiasi valore intero compreso tra 1024 e 16384. Il valore predefinito è 16384.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxGroupSizeToExpand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Rappresenta il numero massimo di persone visualizzate quando un gruppo viene espanso. Ad esempio, se MaxGroupSizeToExpand viene impostato su 75, all'espansione del gruppo saranno visualizzati solo i primi 75 membri del gruppo.</p>
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
<td><p>Consente di impostare la dimensione minima della chiave di richiesta di firma del certificato (CSR). La dimensione minima può essere impostata su qualsiasi valore intero compreso tra 1024 e 16384. Il valore predefinito è 16384.</p></td>
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
<td><p>URL di un servizio Web in grado di elaborare una richiesta di posizione. Questo servizio è generalmente utilizzato solo se le richieste di posizione non possono essere risolte in locale.</p></td>
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
<p>Se impostato su True (valore predefinito), gli utenti che accedono a una riunione utilizzando un'applicazione client diversa da Lync visualizzeranno un collegamento che li invita a scaricare Lync Web App.</p></td>
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
<td><p>Raccolta di certificati che rappresenta le catene di certificati considerati attendibili dal server Web. I nuovi certificati aggiunti alla raccolta devono essere creati tramite il cmdlet <strong>New-CsWebTrustedCACertificate</strong>.</p>
<p>La raccolta non viene utilizzata se la proprietà InferCertChainFromSSL è impostata su True.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCertificateAuth</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True (valore predefinito), i client possono essere autenticati utilizzando i certificati. Impostare questo valore su False ($False) per disabilitare l'autenticazione del certificato.</p></td>
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
<td><p>Se l'impostazione è True (valore predefinito), i client possono essere autenticati utilizzando i PIN. Impostare questo valore su False ($False) per disabilitare l'autenticazione mediante PIN.</p></td>
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

Nessuno. Il cmdlet **New-CsWebServiceConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsWebServiceConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

