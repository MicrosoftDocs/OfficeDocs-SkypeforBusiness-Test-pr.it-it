---
title: Set-CsTenantHybridConfiguration
TOCTitle: Set-CsTenantHybridConfiguration
ms:assetid: 805ac9ee-df40-40e1-baaa-adffb6bd8cf6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994046(v=OCS.15)
ms:contentKeyID: 52062196
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantHybridConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Usato in uno scenario ibrido per dare accesso agli utenti ospitati in Microsoft Lync Online a caratteristiche di VoIP aziendali quali bypass multimediale, Enhanced 9-1-1 e parcheggio di chiamata. Uno scenario ibrido, detto anche scenario di dominio condiviso, è una distribuzione di Lync Server in cui alcuni utenti dispongono di account ospitati in un'implementazione locale, mentre altri dispongono di account in Lync Online.

Questo cmdlet può essere usato solo con Skype for Business online.

## Sintassi

    Set-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-PeerDestination <string>] [-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]Set-CsTenantHybridConfiguration [-Tenant <guid>] [-PeerDestination <string>][-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Instance <psobject>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

## Esempi

## Esempio 1

Il comando mostrato nell'esempio 1 imposta l'URL interno del servizio per la raccolta globale di impostazioni di configurazione ibrida del tenant. Per configurare un'impostazione globale, includere il parametro Identity con il valore "global".

    Set-CsTenantHybridConfiguration -Identity "global" - HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Esempio 2

Nell'esempio 2, l'URL interno del servizio viene configurato per un tenant specifico. In questo esempio, il tenant è caratterizzato dell'ID "bf19b7db-6960-41e5-a139-2aa373474354". Quando a un singolo tenant viene esplicitamente assegnato un valore di proprietà, al tenant verranno applicate le impostazioni di configurazione ibrida specifiche del tenant anziché le impostazioni globali.

    Set-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Esempio 3

Il comando mostrato nell'esempio 3 configura l'URL del servizio interno per tutti i tenant dell'organizzazione. A tale scopo, per prima cosa il comando usa il cmdlet **Get-CsTenant** per restituire una raccolta di tutti i tenant disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet **ForEach-Object**, a sua volta, esegue il cmdlet **Set-CsTenantHybridConfiguration** su tutti i tenant della raccolta, impostando l'URL del servizio interno di ogni tenant su "https://internal.litwareinc.com".

    Get-CsTenant | ForEach-Object {Set-CsTenantHybridConfiguration -Tenant $_.TenantID -HybridConfigServiceInternalUrl "https://internal.litwareinc.com"}

## Descrizione dettagliata

In una distribuzione ibrida, o di dominio condiviso, in un'organizzazione sono presenti sia utenti ospitati in Lync Online, sia utenti con account ospitati in Lync Server. Per impostazione predefinita, gli utenti ospitati in Lync Online non hanno accesso all'intera gamma di funzionalità offerte da VoIP aziendale. Il motivo è che i server di Lync Online non dispongono di accesso diretto alla distribuzione di Lync Server locale e alle informazioni di configurazione di rete. Tra l'altro, gli utenti di Lync Online non dispongono di accesso predefinito a funzionalità quali:

  - Enhanced 9-1-1, il servizio di Lync Server usato per le chiamate telefoniche di emergenza.

  - Parcheggio di chiamata, il servizio di Lync Server che consente agli utenti di mettere in attesa una chiamata su un telefono e quindi riprenderla da un altro telefono.

  - Bypass multimediale, che consente alle chiamate da e verso la rete PSTN di ignorare il Mediation Server, minimizzando così la transcodifica e la latenza di rete.

  - Conferenza telefonica con accesso esterno e con chiamata in uscita su rete PSTN, che consente agli utenti di partecipare alla parte audio di una conferenza online usando un normale telefono PSTN o un dispositivo mobile.

  - Applicazione Response Group, che consente di instradare automaticamente le chiamate telefoniche a entità come il supporto tecnico o la linea del servizio clienti. Per impostazione predefinita, gli utenti di Lync Online non possono fungere da agenti di Response Group.

Per fornire accesso a tali funzionalità di VoIP aziendale agli utenti di Lync Online, gli amministratori devono assegnare i valori appropriati ad impostazioni di configurazione ibrida quali gli URL dei servizi Web interno ed esterno e il nome di dominio completo (FQDN) dell'Access Edge Server. Questi valori, che possono essere configurati solo usando il cmdlet **Set-CsTenantHybridConfiguration**, forniscono ai server di Lync Online le informazioni necessarie per l'uso delle caratteristiche di VoIP aziendale avanzate.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p></p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HybridConfigServiceExternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio Web esterno.</p></td>
</tr>
<tr class="even">
<td><p><em>HybridConfigServiceInternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio Web interno.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione ibrida del tenant da modificare. Poiché esiste il limite di una sola raccolta globale di impostazioni di configurazione ibrida, l'unica raccolta che può essere modificata usando il parametro Identity è la raccolta globale:</p>
<p>-Identity global</p>
<p>Per modificare le impostazioni per un singolo tenant, usare il parametro Tenant anziché il parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>PeerDestination</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo dell'Access Edge Server locale.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant per cui modificare le impostazioni di configurazione ibrida. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Eseguendo questo comando è possibile fare in modo che venga restituito l'ID di ogni tenant:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in ambienti ibridi.</p></td>
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

Nessuno. Il cmdlet **Set-CsTenantHybridConfiguration** non accetta l'input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsTenantHybridConfiguration** modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

