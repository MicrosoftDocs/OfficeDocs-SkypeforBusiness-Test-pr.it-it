---
title: 'Lync Server 2013: Processo di distribuzione per i dispositivi mobili'
TOCTitle: Processo di distribuzione per i dispositivi mobili
ms:assetid: 5a1cebda-c14b-4ff4-9c36-f7caa868160f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690023(v=OCS.15)
ms:contentKeyID: 49300673
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per i dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013. It is noted accordingly.

In questa sezione viene descritta la sequenza di passaggi necessari per distribuire la funzionalità di mobilità di Lync Server 2013.

### Processo di distribuzione della mobilità

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Autorizzazioni</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Creare record DNS (Domain Name System)</p></td>
<td><ul>
<li><p>Creare un record interno CNAME o A (host, AAAA se IPv6) DNS per risolvere l'URL del servizio di individuazione automatica interno.</p></li>
<li><p>Creare un record esterno CNAME o A (host, AAAA se IPv6) DNS per risolvere l'URL del servizio di individuazione automatica esterno.</p></li>
</ul></td>
<td><p>Domain Admins</p>
<p>DnsAdmins</p></td>
<td><p><a href="lync-server-2013-creating-dns-records-for-the-autodiscover-service.md">Creazione di record DNS per il servizio di individuazione automatica in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Modificare i certificati</p></td>
<td><p>Aggiungere voci di nomi alternativi soggetto ai certificati seguenti per supportare connessioni sicure per gli utenti mobili:</p>
<ul>
<li><p>Certificato del Server Director</p></li>
<li><p>Certificato del pool Front End</p></li>
<li><p>Certificato del proxy inverso</p></li>
</ul></td>
<td><p>Amministratore locale</p></td>
<td><p><a href="lync-server-2013-modifying-certificates-for-mobility.md">Modifica dei certificati per i dispositivi mobili in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurare il proxy inverso</p></td>
<td><ul>
<li><p>Assegnare certificati aggiornati con i nomi alternativi soggetto al listener SSL (Secure Sockets Layer).</p></li>
<li><p>Riconfigurare la regola di pubblicazione Web per l'URL del servizio di individuazione automatica esterno.</p></li>
<li><p>Assicurarsi che esista una regola di pubblicazione Web per l'URL dei servizi Web esterni di Lync Server 2013 nel pool Front End.</p></li>
</ul>
<p>Oppure</p>
<ul>
<li><p>Se si sceglie di utilizzare HTTP per la richiesta di individuazione automatica iniziale e non si aggiornano gli elenchi dei nomi alternativi soggetto per i certificati, configurare una nuova regola di pubblicazione Web o riconfigurare una regola di pubblicazione esistente per la porta 80 HTTP.</p></li>
</ul></td>
<td><p>Amministratore locale</p></td>
<td><p><a href="lync-server-2013-configuring-the-reverse-proxy-for-mobility.md">Configurazione del proxy inverso per i dispositivi mobili in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Testare la distribuzione per dispositivi mobili per Lync 2010 Mobile utilizzando il servizio Mobility Mcx</p></td>
<td><p>Eseguire <strong>Test-CsMcxP2PIM</strong> per testare l'invio di un messaggio istantaneo da una persona a un'altra.</p>
<p>Per un elenco completo delle opzioni, vedere la documentazione del cmdlet Lync Server Management Shell per <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsMcxP2PIM">Test-CsMcxP2PIM</a>.</p></td>
<td><p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-verifying-your-mobility-deployment.md">Verifica della distribuzione per dispositivi mobili in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Testare la distribuzione per dispositivi mobili per i client Lync 2013 Mobile tramite i componenti Web UCWA</p></td>
<td><p>Utilizzare il cmdlet <strong>Test-CsUcwaConference</strong> per testare e verificare che gli utenti predefiniti per il test o una coppia di utenti effettivi possano utilizzare UCWA per creare una conferenza e parteciparvi.</p>
<p>Per un elenco completo delle opzioni, vedere la documentazione del cmdlet Lync Server Management Shell per <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsUcwaConference">Test-CsUcwaConference</a>.</p></td>
<td><p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-verifying-your-mobility-deployment.md">Verifica della distribuzione per dispositivi mobili in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare il sistema per le notifiche push</p></td>
<td><ul>
<li><p>Per Lync Server 2013server perimetrali aggiungere un provider di hosting online Lync Server e configurare la federazione del provider di hosting.</p></li>
<li><p>Per Lync Server 2010server perimetrali aggiungere un provider di hosting online Lync Server e configurare la federazione del provider di hosting.</p></li>
<li><p>Per Office Communications Server 2007 R2server perimetrali aggiungere un partner federato.</p></li>
<li><p>Se si desidera supportare le notifiche push tramite una rete Wi-Fi, configurare un regola del firewall in uscita per la porta TCP 5223.</p></li>
<li><p>Utilizzare il cmdlet <strong>Set-CsPushNotificationConfiguration</strong> per abilitare le notifiche push al servizio APNS (Apple Push Notification Service ) e MPNS (Microsoft Push Notification Service). Questa funzionalità è disabilitata per impostazione predefinita.</p></li>
<li><p>Utilizzare il cmdlet <strong>Test-CsFederatedPartner</strong> per testare la configurazione di federazione e il cmdlet <strong>Test-CsMCXPushNotification</strong> per il testing delle notifiche push.</p>
<div class="alert">

> [!NOTE]
> Le notifiche push sono utilizzate per i client Lync 2010 Mobile in dispositivi Apple e Windows Phone<BR>Le notifiche push sono necessarie solo per i client Lync 2013 Mobile in Windows Phone


</div></li>
</ul></td>
<td><p>RtcUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-configuring-for-push-notifications.md">Configurazione delle notifiche push in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurare i criteri per dispositivi mobili</p></td>
<td><p>Utilizzare il cmdlet <strong>Set-CsMobilityPolicy</strong> per consentire o non consentire:</p>
<ul>
<li><p>Chiamata tramite ufficio</p></li>
<li><p>L'abilitazione di audio/video IP</p></li>
<li><p>La richiesta di una connessione Wi-Fi per audio e/o video IP</p></li>
</ul></td>
<td><p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configuring-mobility-policy.md">Configurazione dei criteri per dispositivi mobili in Lync Server 2013</a></p></td>
</tr>
</tbody>
</table>

