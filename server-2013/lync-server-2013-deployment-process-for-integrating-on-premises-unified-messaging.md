---
title: "Lync Server 2013: Processo di distribuzione per l'integrazione della messaggistica unificata locale"
TOCTitle: Processo di distribuzione per l'integrazione della messaggistica unificata locale con Lync Server
ms:assetid: 269a4436-f09f-415b-96ab-49a64370a385
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425737(v=OCS.15)
ms:contentKeyID: 49299965
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per l'integrazione della messaggistica unificata locale con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Se si desidera integrare la Messaggistica unificata di Exchange con Lync Server 2013, è necessario eseguire le attività descritte in questo argomento. Ricordarsi inoltre di leggere le procedure consigliate per la pianificazione e la distribuzione illustrate in [Linee guida per l'integrazione della messaggistica unificata locale con Lync Server 2013](lync-server-2013-guidelines-for-integrating-on-premises-unified-messaging.md). In questo argomento si presuppone che Lync Server 2013 sia stato distribuito con un Mediation Server collocato e che gli utenti siano stati abilitati per Lync Server 2013, ma non necessariamente che siano stati eseguiti tutti i passaggi di distribuzione e configurazione necessari per abilitare VoIP aziendale, come descritto in [Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md) nella documentazione relativa alla distribuzione.

## Processo di integrazione di messaggistica unificata

> [!IMPORTANT]  
> È importante rivolgersi agli amministratori di Exchange dell'organizzazione per verificare le attività da eseguire per garantire un'integrazione rapida e corretta.


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
<th>Gruppi e ruoli obbligatori</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Distribuire uno dei prodotti seguenti:</p><ul><li><p>Microsoft Exchange Server 2007 Service Pack 1 (SP2) o Service Pack più recente</p></li><li><p>Microsoft Exchange Server 2010 o service pack più recente</p></li><li><p>Microsoft Exchange Server 2013</p></li></ul></td>
<td><p>Se si usa Microsoft Exchange Server 2013, installare i ruoli di Exchange Server seguenti nella stessa foresta di Lync Server 2013 o in una foresta diversa:</p><ul><li><p>Accesso client</p></li><li><p>Cassetta postale</p></li></ul>
<p>Se Microsoft Exchange Server 2013 e Messaggistica unificata di Exchange sono installati in foreste diverse, configurare ogni foresta di Exchange in modo che consideri attendibile la foresta di Lync Server 2013.</p>
<p>Se si usa Exchange 2010, installare i ruoli di Exchange Server seguenti nella stessa foresta di Lync Server 2013 o in una foresta diversa:</p><ul><li><p>Messaggistica unificata</p></li><li><p>Trasporto Hub</p></li><li><p>Accesso client</p></li><li><p>Cassetta postale</p></li></ul>
<p>Se Lync Server 2013 e Messaggistica unificata di Exchange sono installati in foreste diverse, configurare ogni foresta di Exchange in modo che consideri attendibile la foresta di Lync Server 2013.</p></td>
<td><p>Amministratori dell'organizzazione (se è il primo Exchange Server dell'organizzazione)</p>
<p>-OPPURE-</p>
<p>Amministratore dell'organizzazione di Exchange (se non è il primo Exchange Server dell'organizzazione)</p></td>
<td><p>Per informazioni sulla versione di Exchange di cui si dispone, vedere la documentazione appropriata:</p>
<dl>
<dt><span></span></dt>
<dd><p>Documentazione relativa alla distribuzione di Exchange Server 2007 all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268694">http://go.microsoft.com/fwlink/p/?LinkId=268694</a>.</p>
</dd>
<dt><span></span></dt>
<dd><p>Documentazione relativa alla distribuzione di Exchange Server 2010 o del Service Pack più recente all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268695">http://go.microsoft.com/fwlink/p/?LinkId=268695</a>.</p>
</dd>
<dt><span></span></dt>
<dd><p>Pianificazione e distribuzione di Microsoft Exchange Server 2013 all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=266569">http://go.microsoft.com/fwlink/p/?LinkId=266569</a>.</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Installare i certificati.</p></td>
<td><p>Scaricare e installare i certificati per ogni server di Messaggistica unificata di Exchange da un'autorità di certificazione radice attendibile. I certificati sono necessari per le connessioni MTLS (Mutual Transport Level Security) tra i server che eseguono Messaggistica unificata di Exchange e Lync Server 2013.</p></td>
<td><p>Administrators</p></td>
<td><p><a href="lync-server-2013-configure-certificates-on-the-server-running-microsoft-exchange-server-unified-messaging.md">Configurare i certificati nel server che esegue la messaggistica unificata di Microsoft Exchange Server</a></p></td>
</tr>
<tr class="odd">
<td><p>Creare e configurare un nuovo dial plan SIP di Messaggistica unificata di Exchange.</p></td>
<td><p>Nel server di Messaggistica unificata di Exchange creare un dial plan SIP basato sui requisiti di distribuzione specifici dell'organizzazione.</p></td>
<td><p>Amministratore dell'organizzazione di Exchange</p></td>
<td><p>Per Exchange 2007 SP1 o Service Pack più recente, vedere &quot;Come creare un dial plan di messaggistica unificata URI SIP&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268632">http://go.microsoft.com/fwlink/p/?linkId=268632</a>.</p>
<p>Per Exchange 2010 o Service Pack più recente, vedere &quot;Creare un dial plan di messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268674">http://go.microsoft.com/fwlink/p/?linkId=268674</a>.</p>
<p>Per Exchange 2013, vedere Messaggistica unificata all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=266579">http://go.microsoft.com/fwlink/p/?LinkId=266579</a>.</p></td>
</tr>
<tr class="even">
<td><p>Configurare le impostazioni di sicurezza per il dial plan SIP di Messaggistica unificata di Exchange.</p></td>
<td><p>Per crittografare il traffico VoIP aziendale, configurare le impostazioni di sicurezza nel dial plan SIP di Messaggistica unificata di Exchange come <strong>SIP con protezione</strong> o <strong>Protetto</strong>. Questo passaggio è particolarmente importante se nell'ambiente sono stati distribuiti o si prevede di distribuire dispositivi Lync Phone Edition. Per garantire il funzionamento di dispositivi Lync Phone Edition in un ambiente con l'integrazione di Messaggistica unificata di Exchange, le impostazioni di crittografia di Lync Server devono essere compatibili con le impostazioni di sicurezza del dial plan di Messaggistica unificata di Exchange. Per informazioni dettagliate, vedere la documentazione relativa alla distribuzione.</p></td>
<td><p>Amministratore dell'organizzazione di Exchange</p></td>
<td><p><a href="lync-server-2013-configure-unified-messaging-on-microsoft-exchange.md">Configurare la messaggistica unificata in Microsoft Exchange per Lync Server 2013</a></p>
<p>Per Exchange 2007 SP1 o Service Pack più recente, vedere anche:</p>
<p>&quot;Come configurare le impostazioni di protezione su un dial plan di messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268696">http://go.microsoft.com/fwlink/p/?LinkId=268696</a>.</p>
<p></p>
<p>Per Exchange 2010 o Service Pack più recente, vedere anche:</p>
<p>&quot;Configurare la protezione VoIP su un dial plan di messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268697">http://go.microsoft.com/fwlink/p/?LinkId=268697</a>.</p>
<p></p>
<p>Per Exchange 2013, vedere Messaggistica unificata all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=266579">http://go.microsoft.com/fwlink/p/?LinkId=266579</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Aggiungere server di Messaggistica unificata al dial plan SIP di Messaggistica unificata di Exchange.</p></td>
<td><p>Per consentire a un server di Messaggistica unificata appena installato di rispondere alle chiamate in arrivo e di elaborarle, è necessario aggiungere il server di Messaggistica unificata a un dial plan di Messaggistica unificata. In questo caso, aggiungere il server al dial plan SIP di Messaggistica unificata di Exchange.</p></td>
<td><p>Administrators</p>
<p>Amministratori di Exchange Server</p></td>
<td><p>Per Exchange 2007 SP1 o Service Pack più recente, vedere &quot;Come aggiungere un server di messaggistica unificata a un dial plan&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268681">http://go.microsoft.com/fwlink/p/?linkId=268681</a>.</p>
<p>Per Exchange 2010 o Service Pack più recente, vedere &quot;Visualizzare o configurare le proprietà di un server di messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268682">http://go.microsoft.com/fwlink/p/?linkId=268682</a>.</p>
<p></p>
<p>Per Exchange 2013, vedere Messaggistica unificata all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=266579">http://go.microsoft.com/fwlink/p/?LinkId=266579</a>.</p></td>
</tr>
<tr class="even">
<td><p>Configurare cassette postali con indirizzi SIP</p></td>
<td><p>Assegnare indirizzi SIP alle cassette postali di utenti VoIP aziendale che utilizzeranno le funzionalità di Messaggistica unificata di Exchange.</p></td>
<td><p>Amministratore di Lync Server 2013</p>
<p>Amministratore destinatari di Exchange</p></td>
<td><p>Per Exchange 2007 SP1 o Service Pack più recente, vedere &quot;Come aggiungere, rimuovere o modificare un indirizzo SIP per un utente abilitato alla messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268698">http://go.microsoft.com/fwlink/p/?LinkId=268698</a>.</p>
<p>Per Exchange 2010 o Service Pack più recente, vedere &quot;Modificare un indirizzo SIP per un utente abilitato alla messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268699">http://go.microsoft.com/fwlink/p/?LinkId=268699</a>.</p>
<p></p>
<p>Per Exchange 2013, vedere Messaggistica unificata all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=266579">http://go.microsoft.com/fwlink/p/?LinkId=266579</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Eseguire lo script exchucutil.ps1.</p></td>
<td><p>Sul server che esegue i servizi di Messaggistica unificata di Exchange, aprire Exchange Management Shell ed eseguire lo script exchucutil.ps1 che esegue le operazioni seguenti:</p><ul><li><p>Concede a Lync Server 2013 l'autorizzazione per leggere gli oggetti Servizi di dominio Active Directory di Messaggistica unificata di Exchange, in modo particolare i dial plan SIP creati nell'attività precedente.</p></li><li><p>Crea un oggetto gateway IP di messaggistica unificata in Active Directory per ogni pool Enterprise Edition di Lync Server 2013 o server Standard Edition che ospita gli utenti abilitati per VoIP aziendale.</p></li><li><p>Crea un gruppo di risposta di Messaggistica unificata di Exchange per ogni gateway. L'identificatore pilota del gruppo di risposta sarà il nome del dial plan associato al gateway corrispondente. Deve esistere un mapping uno a uno in caso di più dial plan.</p></li></ul></td>
<td><p>Amministratore dell'organizzazione di Exchange</p>
<p>Amministratore destinatari di Exchange</p></td>
<td><p><a href="lync-server-2013-configure-unified-messaging-on-microsoft-exchange.md">Configurare la messaggistica unificata in Microsoft Exchange per Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare i dial plan di Lync Server 2013.</p></td>
<td><p>Se si esegue l'integrazione con Exchange 2007 SP1 o Service Pack più recente oppure con Exchange 2010, creare un nuovo dial plan VoIP aziendale con un nome che corrisponde all'FQDN del dial plan di messaggistica unificata di Exchange.</p>
<div class="alert">

> [!NOTE]
> Sarà necessario eseguire questa operazione per ogni dial plan di messaggistica unificata.


</div>
<p>Se si esegue l'integrazione con Exchange 2010 SP1, verificare che siano stati configurati dial plan VoIP aziendale appropriati a livello globale/di sito o a livello di pool.</p>
<div class="alert">

> [!NOTE]
> Se si esegue l'integrazione con Exchange 2010 SP1, i nomi del dial plan di Lync Server e dei dial plan SIP di Messaggistica unificata di Exchange non devono necessariamente corrispondere.


</div></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-configuring-dial-plans.md">Configurazione dei dial plan in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Eseguire lo strumento di integrazione di Messaggistica unificata di Exchange.</p></td>
<td><p>In Lync Server 2013 eseguire <strong>ocsumutil.exe</strong>, che esegue le operazioni seguenti:</p><ul><li><p>Crea oggetti contatto Accesso sottoscrittore e Operatore automatico.</p></li><li><p>Verifica l'esistenza di un dial plan VoIP aziendale con un nome corrispondente all'FQDN del dial plan di messaggistica unificata di Exchange. Se si esegue Exchange 2010 SP1 o Service Pack più recente, i nomi dei dial plan non devono necessariamente corrispondere ed è possibile ignorare il relativo avviso generato dallo strumento.</p></li></ul>
<p>Questo strumento funziona analizzando le impostazioni di Active Directory per la messaggistica unificata di Exchange e consentendo all'amministratore di Lync Server 2013 di visualizzare, creare e modificare gli oggetti contatto.</p></td>
<td><p>RTCUniversalServerAdmins <em>e</em> TCUniversalUserAdmins</p>
<div class="alert">
> [!IMPORTANT]  
> Per eseguire correttamente ocsumutil.exe, l'utente deve appartenere a entrambi i gruppi.
</div>
<div class="alert">

> [!NOTE]
> Per creare oggetti contatto, l'utente che esegue ocsumutil.exe deve disporre dell'autorizzazione appropriata per l'unità organizzativa di Active Directory in cui sono archiviati i nuovi oggetti contatto. Questa autorizzazione può essere concessa eseguendo il cmdlet <STRONG>Grant-CsOUPermission</STRONG>. Per informazioni dettagliate, vedere la documentazione relativa a Lync Server Management Shell.


</div></td>
<td><p><a href="lync-server-2013-configure-lync-server-2013-to-work-with-unified-messaging-on-microsoft-exchange-server.md">Configurare Lync Server 2013 per l'utilizzo della messaggistica unificata in Microsoft Exchange Server</a></p></td>
</tr>
<tr class="even">
<td><p>Se necessario, eseguire altre operazioni di configurazione di VoIP aziendale.</p></td>
<td><p>Se le impostazioni di VoIP aziendale non sono state già configurate per i server o gli utenti, eseguire una o più delle operazioni seguenti:</p><ul><li><p>Distribuire e configurare</p>
<p>i gateway PSTN (Public Switched Telephone Network) e i Mediation Server</p></li><li><p>Definire criteri vocali, record di utilizzo PSTN e route di chiamate in uscita.</p></li><li><p>Abilitare gli utenti per VoIP aziendale.</p></li><li><p>Facoltativamente, configurare utenti specifici con i dial plan.</p></li></ul>
<p>A seconda delle funzionalità di VoIP aziendale abilitate, potrebbero essere necessarie altre operazioni di configurazione.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>RTCUniversalUserAdmins</p></td>
<td><p>Vedere gli argomenti nelle sezioni seguenti:</p><ul><li><p><a href="lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md">Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013</a></p></li><li><p><a href="lync-server-2013-deploying-enterprise-voice.md">Distribuzione di VoIP aziendale in Lync Server 2013</a></p></li></ul></td>
</tr>
<tr class="odd">
<td><p>Abilitare gli utenti VoIP aziendale per Messaggistica unificata di Exchange.</p></td>
<td><p>Nel server di Messaggistica unificata di Exchange verificare che sia stato creato un criterio cassetta postale di Messaggistica unificata e che a ogni utente sia assegnato un numero di interno univoco. Abilitare quindi l'utente per Messaggistica unificata.</p></td>
<td><p>Amministratore destinatari di Exchange</p></td>
<td><p>Per Exchange 2007 SP1 o Service Pack più recente, vedere &quot;Abilitare un utente per la messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268700">http://go.microsoft.com/fwlink/p/?LinkId=268700</a>.</p>
<p>Per Exchange 2010 o Service Pack più recente, vedere &quot;Abilitare un utente per la messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268701">http://go.microsoft.com/fwlink/p/?LinkId=268701</a>.</p>
<p></p>
<p>Per Exchange 2013, vedere Messaggistica unificata all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=266579">http://go.microsoft.com/fwlink/p/?LinkId=266579</a>.</p></td>
</tr>
</tbody>
</table>

