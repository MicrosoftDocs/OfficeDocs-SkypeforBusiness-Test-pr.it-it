---
title: Set-CsAccessEdgeConfiguration
TOCTitle: Set-CsAccessEdgeConfiguration
ms:assetid: f3108b59-1ab2-4288-a470-57d741e7e569
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413017(v=OCS.15)
ms:contentKeyID: 49302445
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAccessEdgeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori di proprietà di una raccolta esistente di impostazioni di configurazione di Access Edge Server per computer che eseguono servizio Access Edge. Il servizio Access Edge in esecuzione in tali computer (definiti anche Edge Server) consente agli utenti all'esterno della rete interna di comunicare con gli utenti all'interno della rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAccessEdgeConfiguration [-AllowAnonymousUsers <$true | $false>] [-AllowFederatedUsers <$true | $false>] [-AllowOutsideUsers <$true | $false>] [-CertificatesDeletedPercentage <UInt32>] [-DiscoveredPartnerReportPeriodMinutes <UInt32>] [-DiscoveredPartnerStandardRate <UInt32>] [-EnableArchivingDisclaimer <$true | $false>] [-EnableDiscoveredPartnerContactsLimit <$true | $false>] [-EnableUserReplicator <$true | $false>] [-Identity <XdsIdentity>] [-KeepCrlsUpToDateForPeers <$true | $false>] [-MarkSourceVerifiableOnOutgoingMessages <$true | $false>] [-MaxAcceptedCertificatesStored <UInt32>] [-MaxContactsPerDiscoveredPartner <UInt32>] [-MaxRejectedCertificatesStored <UInt32>] [-OutgoingTlsCountForFederatedPartners <UInt32>] <COMMON PARAMETERS>

    Set-CsAccessEdgeConfiguration [-AllowAnonymousUsers <$true | $false>] [-AllowFederatedUsers <$true | $false>] [-AllowOutsideUsers <$true | $false>] [-CertificatesDeletedPercentage <UInt32>] [-DefaultRouteFqdn <String>] [-DiscoveredPartnerReportPeriodMinutes <UInt32>] [-DiscoveredPartnerStandardRate <UInt32>] [-EnableArchivingDisclaimer <$true | $false>] [-EnableDiscoveredPartnerContactsLimit <$true | $false>] [-EnableUserReplicator <$true | $false>] [-IsPublicProvider <$true | $false>] [-KeepCrlsUpToDateForPeers <$true | $false>] [-MarkSourceVerifiableOnOutgoingMessages <$true | $false>] [-MaxAcceptedCertificatesStored <UInt32>] [-MaxContactsPerDiscoveredPartner <UInt32>] [-MaxRejectedCertificatesStored <UInt32>] [-OutgoingTlsCountForFederatedPartners <UInt32>] [-UseDefaultRouting <SwitchParameter>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] <COMMON PARAMETERS>

    Set-CsAccessEdgeConfiguration [-AllowAnonymousUsers <$true | $false>] [-AllowFederatedUsers <$true | $false>] [-AllowOutsideUsers <$true | $false>] [-BeClearingHouse <$true | $false>] [-CertificatesDeletedPercentage <UInt32>] [-DiscoveredPartnerReportPeriodMinutes <UInt32>] [-DiscoveredPartnerStandardRate <UInt32>] [-DiscoveredPartnerVerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-EnableArchivingDisclaimer <$true | $false>] [-EnableDiscoveredPartnerContactsLimit <$true | $false>] [-EnablePartnerDiscovery <$true | $false>] [-EnableUserReplicator <$true | $false>] [-KeepCrlsUpToDateForPeers <$true | $false>] [-MarkSourceVerifiableOnOutgoingMessages <$true | $false>] [-MaxAcceptedCertificatesStored <UInt32>] [-MaxContactsPerDiscoveredPartner <UInt32>] [-MaxRejectedCertificatesStored <UInt32>] [-OutgoingTlsCountForFederatedPartners <UInt32>] [-UseDnsSrvRouting <SwitchParameter>] <COMMON PARAMETERS>

    Set-CsAccessEdgeConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono modificate due proprietà delle impostazioni di configurazione dell'Access Edge Server: la proprietà AllowAnonymousUsers è impostata su True e la proprietà VerificationLevel è impostata su UseSourceVerification.

    Set-CsAccessEdgeConfiguration -AllowAnonymousUsers $True -VerificationLevel "UseSourceVerification"

## ESEMPIO 2

Il comando indicato nell'esempio 2 consente di modificare il metodo di routing per l'Edge Server in routing predefinito. A tale scopo, il comando deve includere sia il parametro UseDefaultRouting che il parametro DefaultRouteFqdn, insieme al valore del parametro che specifica il nome di dominio completo dell'Edge Server.

    Set-CsAccessEdgeConfiguration -UseDefaultRouting -DefaultRouteFqdn "atl-edge-001.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 viene modificato il metodo di routing per l'Edge Server in routing del server DNS. Questo richiede l'utilizzo di due parametri: UseDnsSrvRouting (senza alcun valore del parametro) ed EnablePartnerDiscovery (con il valore del parametro $True).

    Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -EnablePartnerDiscovery $True

## Descrizione dettagliata

Gli Edge Server (definiti anche server proxy di accesso) consentono agli utenti di estendere le funzionalità di Lync Server agli utenti che non hanno effettuato l'accesso alla rete interna. Ad esempio, in caso di utenti remoti, i quali sono utenti autenticati che effettuano l'accesso a Lync Server tramite Internet piuttosto che tramite la rete interna, sarà necessario configurare un Edge Server al fine di consentire l'accesso a questi utenti. Analogamente, i server perimetrali sono obbligatori se si intende stabilire la federazione con un'altra organizzazione o assegnare agli utenti i diritti per comunicare con persone che possiedono account con un servizio di messaggistica istantanea quale Yahoo\!, AOL o MSN. Gli Access Edge Server sono presenti sulla rete perimetrale e vengono utilizzati per effettuare e convalidare le connessioni SIP tra gli utenti all'interno e all'esterno della rete interna.

In Lync Server, gli Access Edge Server vengono gestiti utilizzando una singola raccolta globale delle impostazioni di configurazione e il cmdlet **Set-CsAccessEdgeConfiguration** consente di modificare tali impostazioni globali. Le proprietà possono essere modificate a seconda del tipo di routing selezionato per i server perimetrali. Ad esempio, se si sceglie di utilizzare il routing del servizio Domain Name System (DNS), sarà possibile visualizzare e modificare i valori di proprietà BeClearinghouse ed EnablePartnerDiscovery. Se si utilizza il routing predefinito, questi due valori di proprietà non saranno disponibili. Sarà invece possibile visualizzare e modificare i valori di proprietà VerificationLevel ed IsPublicProvider.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsAccessEdgeConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAccessEdgeConfiguration"}

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
<td><p><em>AllowAnonymousUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti anonimi (ovvero gli utenti non autenticati) è consentito attraversare il firewall e partecipare alle riunioni e alle conferenze. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti interni è consentito comunicare con gli utenti dei domini federati. Questa proprietà determina inoltre se gli utenti interni possono comunicare con gli utenti in uno scenario di dominio diviso. (In un dominio diviso, alcuni utenti dispongono di account ospitati a livello locale, mentre altri utenti dispongono di account ospitati in remoto). Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowOutsideUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti possono accedere a Lync Server tramite Internet, includendo sia gli utenti anonimi sia gli utenti remoti che tentano di accedere al sistema. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>BeClearingHouse</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli Edge Server vengono connessi direttamente ad altre organizzazioni. Il valore predefinito è False. Non è consigliabile modificare questo parametro, a meno che non siano state fornite istruzioni in merito dal personale di supporto Microsoft.</p></td>
</tr>
<tr class="odd">
<td><p><em>CertificatesDeletedPercentage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il valore predefinito è 20.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultRouteFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo (FQDN) del server utilizzato per le richieste della federazione. Questo parametro è obbligatorio se si utilizza il routing predefinito.</p>
<p>Notare che è necessario eliminare tutti i provider di hosting e tutti i provider pubblici per poter assegnare una nuova route predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>DiscoveredPartnerReportPeriodMinutes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il valore predefinito è 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>DiscoveredPartnerStandardRate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il valore predefinito è 20.</p></td>
</tr>
<tr class="even">
<td><p><em>DiscoveredPartnerVerificationLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>Imposta il livello di verifica per i messaggi inviati verso e dal individuato. I valori consentiti sono:</p>
<p>* AlwaysVerifiable</p>
<p>* AlwaysUnverifiable</p>
<p>* UseSourceVerification</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableArchivingDisclaimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i server perimetrali inviano l'intestazione della notifica dell'archiviazione ai partner federati e ai partner fornitori di servizi di accesso a terze parti. Questa notifica (la quale informa gli utenti che le conversazioni di messaggistica istantanea potrebbero essere archiviate) può essere visualizzata nella finestra di conversazione di un utente federato o di un utente fornitore di servizi di accesso a terze parti. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDiscoveredPartnerContactsLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Il valore predefinito è True ($True).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePartnerDiscovery</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, Lync Server utilizzerà i record DNS per provare ed individuare i domini partner non riportati nell'elenco AllowedDomains. Se False, Lync Server attuerà esclusivamente la federazione con i domini individuati nell'elenco AllowedDomains. Questo parametro è obbligatorio se si utilizza il routing del servizio DNS. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableUserReplicator</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco delle impostazioni di configurazione di Access Edge da restituire. Poiché è possibile avere esclusivamente una singola istanza globale di queste impostazioni, non è necessario includere il parametro Identity quando si esegue la chiamata al cmdlet <strong>Set-CsAccessEdgeConfiguration</strong>. Tuttavia, per modificare le impostazioni globali è possibile utilizzare la seguente sintassi: -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DisplayAccessEdgeSettingsDnsSrvRouting o DisplayAccessEdgeSettingsDefaultRoute</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>IsPublicProvider</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Deve essere impostato su True se la route predefinita richiede una licenza di messaggistica istantanea pubblica.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCrlsUpToDateForPeers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Determina se gli Edge Server effettuano un controllo periodico degli elenchi di revoche di certificati (CRL) per i certificati dei domini federati. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>MarkSourceVerifiableOnOutgoingMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, i messaggi in uscita vengono contrassegnati come verificabili, consentendo ai domini federati di determinare il livello di verifica di ciascun messaggio. Se False, tutti i messaggi in uscita vengono contrassegnati come non verificabili. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxAcceptedCertificatesStored</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo consentito di certificati memorizzati nella cache da Edge Server. Il valore predefinito è 1000.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxContactsPerDiscoveredPartner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di contatti consentiti per partner individuati. Il valore predefinito è 1000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxRejectedCertificatesStored</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di certificati rifiutati memorizzati nella cache di Edge Server. Il valore predefinito è 500.</p></td>
</tr>
<tr class="even">
<td><p><em>OutgoingTlsCountForFederatedPartners</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifica il numero massimo di connessioni Transport Layer Security (TLS) che possono essere utilizzate per ciascun partner federato. Il numero minimo di connessioni TLS è 1 e il numero massimo è 4. Per impostazione predefinita, OutgoingTlsCountForFederatedPartners è impostato su 4. Non è consigliabile modificare questo parametro, a meno che non siano state fornite istruzioni in merito dal personale di supporto Microsoft.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseDefaultRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Indica che gli amministratori devono specificare il nome di dominio completo del server utilizzato per inviare e ricevere richieste della federazione. Se si include il parametro UseDefaultRouting, è necessario includere anche il parametro DefaultRouteFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>UseDnsSrvRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Indica che gli Edge Server dovrebbero basarsi sui record SRV DNS durante l'invio e la ricezione delle richieste della federazione. Questo è il metodo di routing predefinito.</p></td>
</tr>
<tr class="odd">
<td><p><em>VerificationLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>Se si utilizza il routing predefinito, la proprietà VerificationLevel viene utilizzata per monitorare e valutare il livello di verifica dei messaggi in arrivo. I valori validi sono:</p>
<p>AlwaysVerifiable: tutte le richieste ricevute sulla route predefinita vengono contrassegnate come verificate. Se l'intestazione della verifica non è presente, verrà aggiunta automaticamente al messaggio.</p>
<p>AlwaysUnverifiable: i messaggi vengono inviati solo se il destinatario (l'utente al quale è destinato il messaggio) ha configurato una voce di controllo di accesso per la persona che ha inviato il messaggio.</p>
<p>UseSourceVerification: la verifica dei messaggi si basa sul livello di verifica incluso nel messaggio. Se non è presente alcuna intestazione della verifica, il messaggio verrà contrassegnato come non verificato.</p></td>
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

Nessuno. Il cmdlet **Set-CsAccessEdgeConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Set-CsAccessEdgeConfiguration** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

