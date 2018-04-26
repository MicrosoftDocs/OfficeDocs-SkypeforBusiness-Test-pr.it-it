---
title: Set-CsMeetingRoom
TOCTitle: Set-CsMeetingRoom
ms:assetid: 3dd02280-6407-4e17-929c-7070f8d1c3cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204831(v=OCS.15)
ms:contentKeyID: 49300296
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMeetingRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di una sala riunioni esistente di Lync Server 2013. Una sala riunioni è un dispositivo per conferenze progettato per gestire scenari di collaborazione e videoconferenze in piccole sale conferenze. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsMeetingRoom -Identity <UserIdParameter> [-AcpInfo <MultiValuedProperty>] [-AudioVideoDisabled <$true | $false>] [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-HostedVoiceMail <$true | $false>] [-LineServerURI <String>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrivateLine <String>] [-RemoteCallControlTelephonyEnabled <$true | $false>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 aggiorna il valore LineUri assegnato alla sala riunioni RedmondMeetingRoom.

    Set-CsMeetingRoom -Identity "RedmondMeetingRoom" -LineUri "tel:+12065551219"

## Esempio 2

Nell'esempio 2 viene temporaneamente disabilitata la sala riunioni RedmondMeetingRoom. Per ottenere questo risultato, viene impostata la proprietà Enabled su False ($False).

    Set-CsMeetingRoom -Identity "RedmondMeetingRoom" -Enabled $False

Per abilitare di nuovo la sala riunioni, è sufficiente impostare la proprietà Enabled su True ($True):

    Set-CsMeetingRoom -Identity "RedmondMeetingRoom" -Enabled $True

## Esempio 3

Nell'esempio 3 vengono temporaneamente disabilitate tutte le sale riunioni dell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsMeetingRoom** senza parametri. In questo modo viene restituita una raccolta di tutte le sale riunioni disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsMeetingRoom**, che disabilita temporaneamente ogni sala riunioni della raccolta.

    Get-CsMeetingRoom | Set-CsMeetingRoom -Enabled $False

## Esempio 4

Nell'esempio 4 tutte le sale riunioni dell'organizzazione vengono configurate in modo da utilizzare l'archiviazione di Lync Server 2013 anziché l'archiviazione di Microsoft Exchange Server. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsMeetingRoom** per restituire una raccolta di tutte le sale riunioni disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsMeetingRoom**, che utilizza il cmdlet ExchangeArchivingPolicy per configurare ogni sala riunioni della raccolta per l'utilizzo dell'archiviazione di Lync Server.

    Get-CsMeetingRoom | Set-CsMeetingRoom -ExchangeArchivingPolicy "UseLyncArchivingPolicy"

## Descrizione dettagliata

In Lync Server le sale riunioni sono accessori autonomi per computer che vengono installati nelle sale conferenze e offrono funzionalità avanzate per riunioni, ad esempio:

  - Accesso alle riunioni con un singolo tocco

  - Raccolta video multiview

  - Lavagne abilitate per il tocco sulla parte anteriore dello schermo della sala riunioni

  - Integrazione del calendario per l'accesso alle riunioni pianificate

  - Condivisione e scambio di contenuto

Per gestire questi nuovi dispositivi endpoint, è necessario inoltre creare e abilitare un account di cassetta postale per la risorsa Microsoft Exchange Server 2013 per il dispositivo e quindi abilitarlo per Lync Server 2013. Si noti che per Lync Server non sono disponibili cmdlet per la creazione o la rimozione di sale riunioni. È necessario invece utilizzare il cmdlet [Enable-CsMeetingRoom](enable-csmeetingroom.md) per abilitare le sale riunioni e il cmdlet [Disable-CsMeetingRoom](disable-csmeetingroom.md) per disabilitarle. Per poter abilitare la sala riunioni, l'account per la risorsa deve essere già presente. Disabilitando una sala riunioni viene solo rimossa la sala riunioni dalla raccolta di sale riunioni, non viene eliminato l'account di cassetta postale per la risorsa.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMeetingRoom"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Set-CsMeetingRoom** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>UserIdParameter</p></td>
<td><p>Indica l'identità della sala riunioni da modificare. Le identità delle sale riunioni in genere vengono specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP della sala riunioni, 2) il nome dell'entità utente (UPN) della sala riunioni, 3) il nome di dominio e il nome di accesso della sala riunioni nel formato dominio\accesso (ad esempio litwareinc\room14) e 4) il nome visualizzato di Active Directory della sala riunioni (ad esempio Room 14). È inoltre possibile fare riferimento all'account della sala riunioni utilizzando il relativo nome distinto Active Directory.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AcpInfo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>MultiValuedProperty</p></td>
<td><p>Consente di assegnare a una sala riunioni uno o più provider di servizi di audioconferenza di terze parti. È tuttavia consigliabile utilizzare il cmdlet <strong>Set-UserAcp</strong> per assegnare provider di servizi di audioconferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioVideoDisabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se alla sala riunioni è consentito effettuare chiamate audio/video (A/V) utilizzando Lync 2013. Se si imposta il parametro su True, verranno applicate limitazioni significative alla sala riunioni per l'invio e la ricezione di messaggi istantanei.</p>
<p>Non è possibile disabilitare le comunicazioni A/V se una sala riunioni è attualmente abilitata per il controllo delle chiamate remote, VoIP aziendale e/o soft routing IP-PBX (Internet Protocol Private Branch Exchange).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sulle sale riunioni. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer, ad esempio atl-dc-001, o dal nome di dominio completo (FQDN), ad esempio atl-cd-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se la sala riunioni è stata abilitata per Lync Server 2013. Se si imposta questo valore su False, la sala riunioni non potrà più accedere a Lync Server. Se invece si imposta il valore su True, vengono riabilitati i privilegi di accesso della sala riunioni.</p>
<p>Se si disabilita un account utilizzando il parametro Enabled, le informazioni associate a tale account (inclusi i criteri assegnati e l'eventuale abilitazione della sala riunioni per VoIP aziendale e/o il controllo delle chiamate remote) vengono mantenute. Se in seguito si riabilita l'account utilizzando il parametro Enabled, le informazioni sull'account associate verranno ripristinate. Questo comportamento è diverso dall'utilizzo del cmdlet <strong>Disable-CsMeetingRoom</strong> per disabilitare un account di sala riunioni. Quando si esegue Disable-CsMeetingRoom, tutti i dati di Lync Server associati a tale account vengono eliminati.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se la sala riunioni è stata abilitata per VoIP aziendale, ovvero l'implementazione Microsoft del protocollo VoIP (Voice over Internet Protocol). Con VoIP aziendale le sale riunioni possono effettuare telefonate via Internet anziché utilizzare la rete telefonica standard.</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica come e dove verranno archiviate le sessioni di messaggistica istantanea e conferenze della sala riunioni. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* NoArchiving</p>
<p>* ArchivingToExchange</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedVoiceMail</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà abilitato per le chiamate effettuate alla segreteria telefonica della sala riunioni il routing a una versione ospitata del servizio Microsoft Exchange Server 2013. Impostando questa opzione su True inoltre si consente alle sale riunioni di effettuare una chiamata direttamente alla segreteria telefonica di un altro utente.</p></td>
</tr>
<tr class="even">
<td><p><em>LineServerURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>URI del gateway telefonico di controllo delle chiamate remote assegnato alla sala riunioni. LineServerUri è l'URI del gateway, preceduto da &quot;sip:&quot;, ad esempio:</p>
<p>-LineServerUri &quot;sip:rccgateway@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Numero di telefono assegnato alla sala riunioni. L'URI (Uniform Resource Identifier) di linea deve essere specificato utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;, ad esempio:</p>
<p>-LineUri &quot;TEL:+14255551297&quot;</p>
<p>L'eventuale numero di interno deve essere aggiunto alla fine dell'URI di linea, ad esempio:</p>
<p>-LineUri &quot;TEL:+14255551297;ext=51297&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto sala riunioni che rappresenta la sala riunioni da modificare. Per impostazione predefinita, il cmdlet <strong>Set-CsMeetingRoom</strong> non passa oggetti tramite pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateLine</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Numero di telefono della linea telefonica privata della sala riunioni. Una linea privata è un numero di telefono che non è pubblicato in Servizi di dominio Active Directory e che quindi non è immediatamente disponibile per altre persone. Questa linea privata inoltre ignora la maggior parte delle regole di routing per le chiamate in entrata. Una chiamata a una linea privata ad esempio non viene inoltrata ai delegati di una sala riunioni. Le linee private sono spesso utilizzate per le telefonate personali o per le chiamate di affari che non riguardano gli altri membri del team.</p>
<p>La linea privata deve essere specificata utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;, ad esempio:</p>
<p>-PrivateLine &quot;TEL:+14255551297&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RemoteCallControlTelephonyEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se la sala riunioni è stata abilitata per la telefonia con controllo delle chiamate remote. Se è abilitata per il controllo delle chiamate remote, una sala riunioni può utilizzare Lync Server 2013 per rispondere alle chiamate effettuate al telefono da tavolo. È inoltre possibile effettuare telefonate utilizzando Lync. Queste chiamate si basano sulla rete telefonica standard, denominata anche PSTN (Public Switched Telephone Network). Per effettuare e ricevere telefonate su Internet, la sala riunioni deve essere abilitata per VoIP aziendale. Per informazioni dettagliate, vedere il parametro EnterpriseVoiceEnabled.</p>
<p>Per essere abilitata per il controllo delle chiamate remote, una sala riunioni deve disporre inoltre sia di LineUri che di LineServerUri.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco (simile a un indirizzo di posta elettronica) che consente alla sala riunioni di comunicare utilizzando dispositivi SIP come Lync 2013. L'indirizzo SIP deve utilizzare il prefisso sip: e un dominio SIP valido, ad esempio:</p>
<p>-SipAddress &quot;sip:room14@litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsMeetingRoom** accetta le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsMeetingRoom** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom.

## Vedere anche

#### Ulteriori risorse

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)

