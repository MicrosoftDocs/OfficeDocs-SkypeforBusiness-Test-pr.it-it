---
title: Get-CsTenantHybridConfiguration
TOCTitle: Get-CsTenantHybridConfiguration
ms:assetid: 4b2e6781-8f46-4ba3-be76-3a95460e3132
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994034(v=OCS.15)
ms:contentKeyID: 52062156
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantHybridConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce i valori per le impostazioni di configurazione ibrida che consentono agli utenti ospitati in Microsoft Lync Online di accedere alle funzionalità di VoIP aziendale quali bypass multimediale, servizi di emergenza avanzati e parcheggio di chiamata. Uno scenario ibrido, detto anche scenario con dominio condiviso, è una distribuzione di Lync Server in cui alcuni utenti dispongono di account ospitati in locale, mentre altri dispongono di account in Lync Online.

Il cmdlet Get-CsTenantHybridConfiguration può essere usato solo con Skype for Business online.

## Sintassi

    Get-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-LocalStore] [<CommonParameters>]Get-CsTenantHybridConfiguration [-Tenant <guid>] [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Esempi

## Esempio 1

Il comando mostrato nell'esempio 1 restituisce i valori di proprietà per la raccolta globale di impostazioni di configurazione ibrida dei tenant.

    Get-CsTenantHybridConfiguration -Identity "Global"

## Esempio 2

Nell'esempio 2 vengono restituiti i valori di proprietà per le impostazioni di configurazione ibrida dei tenant personalizzate applicate al tenant con TenantId "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## Esempio 3

L'esempio 3 restituisce le informazioni di configurazione ibrida per tutti i tenant disponibili. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsTenant** per restituire una raccolta di tutti questi tenant. Questa raccolta viene quindi inviata tramite pipe al cmdlet**ForEach-Object** che esegue due operazioni su ogni tenant nella raccolta, uno alla volta. Prima di tutto, il cmdlet stampa il nome visualizzato di Active Directory per il tenant, assicurando così la facile identificazione di ogni raccolta di impostazioni. Il cmdlet **ForEach-Object** esegue poi il cmdlet **Get-CsTenantHybridConfiguration** per restituire le impostazioni di configurazione ibrida per il tenant in questione.

    Get-CsTenant | ForEach-Object {$_.DisplayName; Get-CsTenantHybridConfiguration -Tenant $_.TenantId}

## Descrizione dettagliata

In una distribuzione ibrida, o con dominio condiviso, in un'organizzazione sono presenti sia utenti ospitati in Lync Online, sia utenti con account ospitati nella versione locale di Lync Server. Per impostazione predefinita, gli utenti ospitati in Lync Online non hanno accesso all'intera gamma di funzionalità offerte da VoIP aziendale. Il motivo è che i server di Lync Online non dispongono di accesso diretto alla distribuzione di Lync Server locale e alle informazioni di configurazione di rete. Tra l'altro, gli utenti di Lync Online non dispongono di accesso predefinito a funzionalità quali:

  - Enhanced 9-1-1, il servizio di Lync Server usato per le chiamate telefoniche di emergenza.

  - Parcheggio di chiamata, il servizio di Lync Server che consente agli utenti di mettere in attesa una chiamata su un telefono e quindi riprenderla da un altro telefono.

  - Bypass multimediale, che consente alle chiamate da e verso la rete PSTN di ignorare il Mediation Server, minimizzando così la transcodifica e la latenza di rete.

  - Conferenza telefonica con accesso esterno e con chiamata in uscita su rete PSTN, che consente agli utenti di partecipare alla parte audio di una conferenza online usando un normale telefono PSTN o un dispositivo mobile.

  - Applicazione Response Group, che consente di instradare automaticamente le chiamate telefoniche a entità come il supporto tecnico o la linea del servizio clienti. Per impostazione predefinita, gli utenti di Lync Server non possono fungere da agenti di Response Group.

Per fornire accesso a tali funzionalità di VoIP aziendale agli utenti di Lync Online, gli amministratori devono assegnare i valori appropriati ad impostazioni di configurazione ibrida quali gli URL dei servizi Web interno ed esterno e il nome di dominio completo (FQDN) dell'Access Edge Server. Questi valori, che possono essere configurati solo usando il cmdlet **Set-CsTenantHybridConfiguration**, forniscono ai server di Lync Online le informazioni necessarie per l'uso delle caratteristiche di VoIP aziendale avanzate.

È possibile usare il cmdlet **Get-CsTenantHybridConfiguration** per restituire informazioni sulle impostazioni di configurazione ibrida dei tenant attualmente in uso nell'organizzazione.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di usare i caratteri jolly per restituire una raccolta di impostazioni di configurazione ibrida dei tenant. Poiché esiste il limite di una sola raccolta globale di impostazioni di configurazione ibrida, non è necessario usare il parametro Filter. Questa è comunque una sintassi valida per il cmdlet <strong>Get-CsTenantHybridConfiguration</strong>:</p>
<p>Get-CsTenantHybridConfiguration –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione ibrida dei tenant da restituire. Poiché esiste il limite di una sola raccolta globale di impostazioni di configurazione ibrida, l'unica raccolta che può essere restituita usando il parametro Identity è la raccolta globale:</p>
<p>-Identity global</p>
<p>Per modificare le impostazioni per un singolo tenant, usare il parametro Tenant anziché il parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione ibrida dei tenant dalla replica locale dell'archivio di gestione centrale, anziché l'archivio stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant per cui restituire le impostazioni di configurazione ibrida. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTenantHybridConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsTenantHybridConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration.

## Vedere anche

#### Ulteriori risorse

[Set-CsTenantHybridConfiguration](set-cstenanthybridconfiguration.md)

