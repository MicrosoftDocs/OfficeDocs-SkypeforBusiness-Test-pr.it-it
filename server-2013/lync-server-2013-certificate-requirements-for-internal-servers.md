---
title: 'Lync Server 2013: Requisiti dei certificati per i server interni'
TOCTitle: Requisiti dei certificati per i server interni
ms:assetid: 0444cdbd-538c-43b1-b9a1-9d7d6cf818d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398094(v=OCS.15)
ms:contentKeyID: 49299531
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti dei certificati per i server interni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I server interni che eseguono Lync Server e che richiedono certificati sono server Standard Edition, Front End Server Enterprise Edition, Mediation Server e director. Nella tabella seguente sono riportati i requisiti dei certificati per tali server. È possibile utilizzare la Configurazione guidata certificati di Lync Server per richiedere questi certificati.

> [!tip]  
> I certificati con caratteri jolly sono supportati per i nomi alternativi del soggetto associati agli URL semplici nel pool Front End, nel Front End Server o nel Director. Per informazioni dettagliate sul supporto dei certificati con caratteri jolly, vedere <a href="lync-server-2013-wildcard-certificate-support.md">Supporto dei certificati con caratteri jolly in Lync Server 2013</a>.

Benché per i server interni sia consigliata un'autorità di certificazione (CA) globale (enterprise) interna, è inoltre possibile utilizzare una CA pubblica. Per l'elenco delle CA pubbliche che forniscono certificati conformi a requisiti specifici dei certificati per comunicazioni unificate e che hanno collaborato con Microsoft per garantire il funzionamento di tali certificati con la Configurazione guidata certificati di Lync Server, vedere l'articolo 929395 della Microsoft Knowledge Base, "Partner per certificati per comunicazioni unificate per Exchange Server e Communications Server" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=202834\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=202834%26clcid=0x410).

La comunicazione con altre applicazioni e server, ad esempio Exchange 2013, richiede un certificato supportato dalle altre applicazioni e prodotti. Per la versione 2013, Lync Server 2013 e altri prodotti server Microsoft, compresi Exchange 2013 e SharePoint Server, supportano il protocollo Open Authorization (OAuth) per l'autenticazione e l'autorizzazione server-server. Per informazioni dettagliate, vedere [Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.

Per le connessioni da client che eseguono il sistema operativo Windows 7, il sistema operativo Windows Server 2008, il sistema operativo Windows Server 2008 R2, il sistema operativo Windows Vista e Microsoft Lync Phone Edition, Lync Server 2013 include il supporto per (ma non richiede) i certificati firmati con la funzione hash crittografico SHA-256. Per supportare l'accesso esterno con SHA-256, il certificato esterno viene emesso da un'autorità di certificazione pubblica che utilizza SHA-256.

Nelle tabelle seguenti sono indicati i requisiti dei certificati in base al ruolo del server per i pool Front End e i server Standard Edition. Sono tutti certificati del server Web standard con chiave privata non esportabili.

Si noti che l'utilizzo chiavi avanzato nel server viene configurato automaticamente quando si utilizza la Configurazione guidata certificati per richiedere certificati.


> [!NOTE]
> Tutti i nomi descrittivi dei certificati devono essere univoci nell'archivio del computer.




> [!NOTE]
> Se nel DNS è stato configurato sipinternal.contoso.com o sipexternal.contoso.com, sarà necessario aggiungerlo nel campo Nome alternativo soggetto del certificato.



### Certificati per il server Standard Edition

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Certificato</th>
<th>Nome soggetto/ Nome comune</th>
<th>Nome alternativo soggetto</th>
<th>Esempio</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Predefinito</p></td>
<td><p>Nome di dominio completo (FQDN) del pool</p></td>
<td><p>FQDN del pool e FQDN del server</p>
<p>Se sono presenti più domini SIP ed è stata abilitata la configurazione automatica dei client, la Configurazione guidata certificati rileva e aggiunge l'FQDN di ogni dominio SIP supportato.</p>
<p>Se il pool rappresenta il server di accesso automatico per i client ed è richiesta la corrispondenza DNS (Domain Name System) esatta nei criteri di gruppo, saranno inoltre necessarie voci per sip.sipdomain (per ogni dominio SIP di cui si dispone).</p></td>
<td><p>SN=se01.contoso.com; SAN=se01.contoso.com</p>
<p>Se il pool rappresenta il server di accesso automatico per i client ed è richiesta la corrispondenza DNS esatta nei criteri di gruppo, sarà inoltre necessario utilizzare SAN=sip.contoso.com; SAN=sip.fabrikam.com</p></td>
<td><p>Nel caso del server Standard Edition, l'FQDN del server corrisponde all'FQDN del pool.</p>
<p>La procedura guidata rileva i domini SIP specificati durante la configurazione e li aggiunge automaticamente al nome alternativo del soggetto.</p>
<p>Questo certificato può essere utilizzato anche per l'autenticazione server-server.</p></td>
</tr>
<tr class="even">
<td><p>Interno Web</p></td>
<td><p>FQDN del server</p></td>
<td><p>Ognuno dei seguenti:</p><ul><li><p>FQDN Web interno, che corrisponde all'FQDN del server</p></li><li><p>URL semplici per le riunioni (meet)</p></li><li><p>URL semplice accesso esterno</p></li><li><p>URL semplice per l'accesso amministrativo (admin)</p>
<p></p></li><li><p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></li></ul>
<p></p></td>
<td><p>SN=se01.contoso.com; SAN=se01.contoso.com; SAN=meet.contoso.com; SAN=meet.fabrikam.com; SAN=dialin.contoso.com; SAN=admin.contoso.com</p>
<p>Nel caso di un certificato con caratteri jolly:</p>
<p>SN=se01.contoso.com; SAN=se01.contoso.com; SAN=*.contoso.com</p></td>
<td><p>Non è possibile sostituire l'FQDN Web interno in Generatore di topologie.</p>
<p>Se sono presenti più URL semplici per le riunioni, sarà necessario includerli tutti come nomi alternativi del soggetto.</p>
<p>Le voci con caratteri jolly sono supportate per le voci di URL semplici.</p></td>
</tr>
<tr class="odd">
<td><p>Esterno Web</p></td>
<td><p>FQDN del server</p></td>
<td><p>Ognuno dei seguenti:</p><ul><li><p>FQDN Web esterno</p></li><li><p>URL semplice accesso esterno</p></li><li><p>URL semplici riunione per ogni dominio SIP</p></li><li><p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></li></ul></td>
<td><p>SN=se01.contoso.com; SAN=webcon01.contoso.com; SAN=meet.contoso.com; SAN=meet.fabrikam.com; SAN=dialin.contoso.com</p>
<p>Nel caso di un certificato con caratteri jolly:</p>
<p>SN=se01.contoso.com; SAN=webcon01.contoso.com; SAN=*.contoso.com</p></td>
<td><p>Se sono presenti più URL semplici per le riunioni, sarà necessario includerli tutti come nomi alternativi del soggetto.</p>
<p>Le voci con caratteri jolly sono supportate per le voci di URL semplici.</p></td>
</tr>
</tbody>
</table>


### Certificati per il Front End Server in un pool Front End

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Certificato</th>
<th>Nome soggetto/ Nome comune</th>
<th>Nome alternativo soggetto</th>
<th>Esempio</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Predefinito</p></td>
<td><p>FQDN del pool</p></td>
<td><p>FQDN del pool e FQDN del server</p>
<p>Se sono presenti più domini SIP ed è stata abilitata la configurazione automatica dei client, la Configurazione guidata certificati rileva e aggiunge l'FQDN di ogni dominio SIP supportato.</p>
<p>Se il pool rappresenta il server di accesso automatico per i client ed è richiesta la corrispondenza DNS esatta nei criteri di gruppo, saranno inoltre necessarie voci per sip.sipdomain (per ogni dominio SIP di cui si dispone).</p></td>
<td><p>SN=eepool.contoso.com; SAN=eepool.contoso.com; SAN=ee01.contoso.com</p>
<p>Se il pool rappresenta il server di accesso automatico per i client ed è richiesta la corrispondenza DNS esatta nei criteri di gruppo, sarà inoltre necessario utilizzare SAN=sip.contoso.com; SAN=sip.fabrikam.com</p></td>
<td><p>La procedura guidata rileva i domini SIP specificati durante la configurazione e li aggiunge automaticamente al nome alternativo del soggetto.</p>
<p>Questo certificato può essere utilizzato anche per l'autenticazione server-server.</p></td>
</tr>
<tr class="even">
<td><p>Interno Web</p></td>
<td><p>FQDN del pool</p></td>
<td><p>Ognuno dei seguenti:</p><ul><li><p>FQDN Web interno, che NON corrisponde all'FQDN del server</p></li><li><p>FQDN del server</p></li><li><p>FQDN del pool di Lync</p></li><li><p>URL semplici per le riunioni (meet)</p></li><li><p>URL semplice accesso esterno</p></li><li><p>URL semplice per l'accesso amministrativo (admin)</p></li><li><p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></li></ul>
<p></p></td>
<td><p>SN=ee01.contoso.com; SAN=ee01.contoso.com; SAN=meet.contoso.com; SAN=meet.fabrikam.com; SAN=dialin.contoso.com; SAN=admin.contoso.com</p>
<p>Nel caso di un certificato con caratteri jolly:</p>
<p>SN=ee01.contoso.com; SAN=ee01.contoso.com; SAN=*.contoso.com</p></td>
<td><p>Se sono presenti più URL semplici per le riunioni, sarà necessario includerli tutti come nomi alternativi del soggetto.</p>
<p>Le voci con caratteri jolly sono supportate per le voci di URL semplici.</p></td>
</tr>
<tr class="odd">
<td><p>Esterno Web</p></td>
<td><p>FQDN del pool</p></td>
<td><p>Ognuno dei seguenti:</p><ul><li><p>FQDN Web esterno</p></li><li><p>URL semplice accesso esterno</p></li><li><p>URL semplice per l'accesso amministrativo (admin)</p></li><li><p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></li></ul></td>
<td><p>SN=ee01.contoso.com; SAN=webcon01.contoso.com; SAN=meet.contoso.com; SAN=meet.fabrikam.com; SAN=dialin.contoso.com</p>
<p>Nel caso di un certificato con caratteri jolly:</p>
<p>SN=ee01.contoso.com; SAN=webcon01.contoso.com; SAN=*.contoso.com</p></td>
<td><p>Se sono presenti più URL semplici per le riunioni, sarà necessario includerli tutti come nomi alternativi del soggetto.</p>
<p>Le voci con caratteri jolly sono supportate per le voci di URL semplici.</p></td>
</tr>
</tbody>
</table>


### Certificati per il Director

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Certificato</th>
<th>Nome soggetto/ Nome comune</th>
<th>Nome alternativo soggetto</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Predefinito</p></td>
<td><p>FQDN del pool di server Director</p></td>
<td><p>FQDN del Director, FQDN del pool di server Director</p>
<p>Se il pool rappresenta il server di accesso automatico per i client ed è richiesta la corrispondenza DNS esatta nei criteri di gruppo, saranno inoltre necessarie voci per sip.sipdomain (per ogni dominio SIP di cui si dispone).</p></td>
<td><p>SN=dir-pool.contoso.com; SAN=dir-pool.contoso.com; SAN=dir01.contoso.com</p>
<p>Se il pool di server Director rappresenta il server di accesso automatico per i client ed è richiesta la corrispondenza DNS esatta nei criteri di gruppo, sarà inoltre necessario utilizzare SAN=sip.contoso.com; SAN=sip.fabrikam.com</p></td>
</tr>
<tr class="even">
<td><p>Interno Web</p></td>
<td><p>FQDN del server</p></td>
<td><p>Ognuno dei seguenti:</p><ul><li><p>FQDN Web interno, che corrisponde all'FQDN del server</p></li><li><p>URL semplici per le riunioni (meet)</p></li><li><p>URL semplice accesso esterno</p></li><li><p>URL semplice per l'accesso amministrativo (admin)</p></li><li><p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></li></ul>
<p></p></td>
<td><p>SN=dir01.contoso.com; SAN=dir01.contoso.com; SAN=meet.contoso.com; SAN=meet.fabrikam.com; SAN=dialin.contoso.com; SAN=admin.contoso.com</p>
<p>SN=dir01.contoso.com; SAN=dir01.contoso.com SAN=*.contoso.com</p></td>
</tr>
<tr class="odd">
<td><p>Esterno Web</p></td>
<td><p>FQDN del server</p></td>
<td><p>Ognuno dei seguenti:</p><ul><li><p>FQDN Web esterno</p></li><li><p>URL semplice accesso esterno</p></li><li><p>URL semplice per l'accesso amministrativo (admin)</p></li><li><p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></li></ul></td>
<td><p>L'FQDN Web esterno del Director deve essere diverso dal pool Front End o dal Front End Server.</p>
<p>SN=dir01.contoso.com; SAN=directorwebcon01.contoso.com SAN=meet.contoso.com; SAN=meet.fabrikam.com; SAN=dialin.contoso.com</p>
<p>SN=dir01.contoso.com; SAN=directorwebcon01.contoso.com SAN=*.contoso.com</p></td>
</tr>
</tbody>
</table>


Se è presente un pool Mediation Server autonomo, ognuno dei Mediation Server in esso contenuti richiederà i certificati riportati nella tabella seguente. Se si colloca un Mediation Server nei Front End Server, saranno sufficienti i certificati riportati nella tabella "Certificati per il Front End Server in un pool Front End" più indietro in questo argomento.

### Certificati per il Mediation Server autonomo

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Certificato</th>
<th>Nome soggetto/ Nome comune</th>
<th>Nome alternativo soggetto</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Predefinito</p></td>
<td><p>FQDN del pool</p></td>
<td><p>FQDN del pool</p>
<p>FQDN del server membro del pool</p></td>
<td><p>SN=medsvr-pool.contoso.net; SAN=medsvr-pool.contoso.net; SAN=medsvr01.contoso.net</p></td>
</tr>
</tbody>
</table>


### Certificati per il Survivable Branch Appliance

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Certificato</th>
<th>Nome soggetto/ Nome comune</th>
<th>Nome alternativo soggetto</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Predefinito</p></td>
<td><p>FQDN del dispositivo</p></td>
<td><p>SIP.&lt;dominiosip&gt; (è necessaria una voce per ogni dominio SIP)</p></td>
<td><p>SN=sba01.contoso.net; SAN=sip.contoso.com; SAN=sip.fabrikam.com</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Supporto dei certificati con caratteri jolly in Lync Server 2013](lync-server-2013-wildcard-certificate-support.md)

