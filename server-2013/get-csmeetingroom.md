---
title: Get-CsMeetingRoom
TOCTitle: Get-CsMeetingRoom
ms:assetid: ce361cb8-042c-4708-8f9c-7e67a34a570d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205277(v=OCS.15)
ms:contentKeyID: 49302019
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMeetingRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle sale riunioni di Lync Server 2013 configurate per l'utilizzo nell'organizzazione. Una sala riunioni è un dispositivo per conferenze progettato per gestire videoconferenze e scenari di collaborazione in piccole sale conferenze. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsMeetingRoom [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 consente di restituire informazioni su tutte le sale riunioni configurate per l'utilizzo nell'organizzazione.

    Get-CsMeetingRoom

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per una singola sala riunioni: il sistema con l'indirizzo SIP sip:RedmondMeetingRoom@litwareinc.com.

    Get-CsMeetingRoom -Identity "sip:RedmondMeetingRoom@litwareinc.com"

## Esempio 3

Il comando illustrato nell'esempio 3 consente di restituire le informazioni per tutte le sale riunioni a cui sono stati assegnati i criteri vocali RedmondVoicePolicy per ogni singolo utente. A tale scolo, il comando include il parametro Filter e il valore filtro {VoicePolicy –eq "RedmondVoicePolicy} che limita i dati restituiti alle sale riunioni per le quali la proprietà VoicePolicy è uguale a (-eq) RedmondVoicePolicy.

    Get-CsMeetingRoom -Filter {VoicePolicy -eq "RedmondVoicePolicy"}

## Descrizione dettagliata

In Lync Server le sale riunioni sono accessori autonomi per computer che vengono installati nelle sale conferenze e offrono funzionalità avanzate per riunioni, ad esempio:

  - Accesso alle riunioni con un singolo tocco

  - Raccolta video multiview

  - Lavagne abilitate per il tocco sulla parte anteriore dello schermo della sala riunioni

  - Integrazione del calendario per l'accesso alle riunioni pianificate

  - Condivisione e scambio di contenuto

Per gestire questi nuovi dispositivi endpoint, è necessario inoltre creare e abilitare un account di cassetta postale per la risorsa Microsoft Exchange Server 2013 per il dispositivo e quindi abilitarlo per Lync Server 2013. Si noti che per Lync Server non sono disponibili cmdlet per la creazione o la rimozione di sale riunioni. È necessario invece utilizzare il cmdlet [Enable-CsMeetingRoom](enable-csmeetingroom.md) per abilitare le sale riunioni e il cmdlet [Disable-CsMeetingRoom](disable-csmeetingroom.md) per disabilitarle. Per poter abilitare la sala riunioni, l'account per la risorsa deve essere già presente. Disabilitando una sala riunioni viene solo rimossa la sala riunioni dalla raccolta di sale riunioni, non viene eliminato l'account di cassetta postale per la risorsa.

Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di interfaccia della riga di comando Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsMeetingRoom"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsMeetingRoom** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet <strong>Get-CsMeetingRoom</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti contatto.</p>
<p>Per utilizzare il parametro Credential è necessario creare per prima cosa un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di connettersi al controller di dominio specificato per recuperare le informazioni sulla sala riunioni. Per connettersi a un determinato controller di dominio, includere il parametro DomainController seguito dal nome del computer, ad esempio atl-dc-001, o dal relativo nome di dominio completo (FQDN), ad esempio atl-dc-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti filtrando in base ad attributi specifici di Lync Server. È ad esempio possibile limitare i dati restituiti alle sale riunioni a cui sono stati assegnati criteri vocali specifici o a quelle a cui non ne sono stati assegnati.</p>
<p>Il parametro Filter è basato sulla stessa sintassi di filtro di Windows PowerShell utilizzata dal cmdlet Where-Object. Ad esempio, un filtro che restituisce solo le sale a cui sono stati assegnati i criteri vocali RedmondVoicePolicy è simile al seguente:</p>
<p>{VoicePolicy -eq &quot;RedmondVoicePolicy&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica il valore Identity della sala riunioni da recuperare. I valori Identity delle sale riunioni vengono in genere specificati utilizzando uno di quattro formati: 1) indirizzo SIP della sala 2) nome dell'entità utente della sala (UPN) 3) nome di accesso e nome di dominio della sala, nel formato dominio\accesso, ad esempio litwareinc\room14 e 4) nome visualizzato Active Directory della sala, ad esempio Sala 14.</p>
<p>È anche possibile fare riferimento a un account sala utilizzando il nome distinto Active Directory della sala.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come valore Identity della sala. Ad esempio, il valore Identity &quot;*Redmond*&quot; restituisce tutte le sale aventi un nome visualizzato contenente il valore in forma di stringa &quot;Redmond&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti filtrando i base ad attributi specifici di Active Directory generici, ovvero attributi non specifici di Lync Server. È ad esempio possibile limitare i dati restituiti alle sale riunioni appartenenti a un reparto specifico. Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione di filtri. Ad esempio, un filtro che restituisce solo le sale riunioni trovate nella città di Redmond è simile al seguente:</p>
<p>-LdapFilter &quot;l=Redmond&quot;</p>
<p>In questa sintassi &quot;l&quot; (L minuscola) rappresenta l'attributo Active Directory (locality); &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore del filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di restituire informazioni sulle sale riunioni in un contenitore o unità organizzativa specifica. Il parametro OU restituisce dati dalle unità organizzative specificate e da eventuali unità secondarie. Ad esempio, se l'unità organizzativa Finanze presenta due unità secondarie, AccountsPayable e AccountsReceivable, verranno restituite le sale riunioni per ognuna di queste tre unità organizzative.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio:</p>
<p>-OU &quot;OU=MeetingRooms,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette sale riunioni, indipendentemente dal numero di sale riunioni presenti nella foresta, includere il parametro ResultSize e impostare il valore del parametro su 7. Non vi è alcun modo di garantire quali sale verranno restituite.</p>
<p>Le dimensioni del risultato possono essere impostate su qualsiasi numero intero compreso tra 0 e 2147483647, incluso. Se impostate su 0 il comando verrà eseguito ma non verranno restituiti dati. Se ResultSize viene impostato su 7 ma nella foresta sono presenti solo tre sale riunioni, verranno restituite quelle tre sale riunioni senza errore.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsMeetingRoom** accetta un valore in forma di stringa da pipeline che rappresenta il valore Identity di un account utente abilitato come sala riunione di Lync Server 2013.

## Tipi restituiti

Il cmdlet **Get-CsMeetingRoom** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom.

## Vedere anche

#### Ulteriori risorse

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

