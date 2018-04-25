---
title: 'Lync Server 2013: Accesso al sito di provisioning di connettività per messaggistica istantanea pubblica di Lync Server'
TOCTitle: Accesso al sito di provisioning di connettività per messaggistica istantanea pubblica di Lync Server
ms:assetid: 77a08234-6bcf-4f59-b43b-ee5fc1926585
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn440174(v=OCS.15)
ms:contentKeyID: 59602740
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Accesso al sito di provisioning di connettività per messaggistica istantanea pubblica di Lync Server da Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il processo di provisioning per la connettività Lync-Skype è stato modificato rispetto ai metodi di provisioning PIC precedenti. Il completamento di questo processo di provisioning può richiedere fino a 30 giorni. È consigliabile avviare subito il processo, prima di completare il resto dei passaggi descritti in questo documento. Una volta completato il processo di provisioning Lync-Skype per il proprio account, tale account verrà attivato e gli utenti idonei verranno abilitati alla connettività per messaggistica istantanea pubblica.

### Per eseguire il provisioning della connettività Lync-Skype, è necessario disporre delle informazioni seguenti:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Numero di contratto Microsoft</p></li>
<li><p>Nome di dominio completo (FQDN) del servizio Access Edge</p></li>
<li><p>Dominio o domini SIP (Session Initiation Protocol)</p></li>
<li><p>Eventuali FQDN aggiuntivi del servizio Access Edge</p></li>
<li><p>Informazioni di contatto</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Numero di contratto Microsoft</p></li>
<li><p>Nome di dominio completo (FQDN) del servizio Access Edge</p></li>
<li><p>Dominio o domini SIP (Session Initiation Protocol)</p></li>
<li><p>Eventuali FQDN aggiuntivi del servizio Access Edge</p></li>
<li><p>Informazioni di contatto</p></li>
</ol></td>
</tr>
</tbody>
</table>


### Per avviare il processo di provisioning per la connettività Lync-Skype:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Accedere al sito Web <strong>https://pic.lync.com</strong> utilizzando il Microsoft Windows Live ID.</p></li>
<li><p>Selezionare il tipo di contratto di licenza Microsoft.</p></li>
<li><p>Selezionare la casella di controllo, assicurandosi di avere letto e accettato i diritti di utilizzo del prodotto per Lync Server.</p></li>
<li><p>Nella pagina di <strong>avvio di una richiesta di provisioning</strong> fare clic sul collegamento appropriato per avviare una richiesta di provisioning:</p></li>
<li><p>Nella pagina di <strong>specifica delle informazioni di provisioning</strong> immettere il <strong>Servizio Access Edge (FQDN)</strong>. Ad esempio, <strong>accessedge.contoso.com</strong>.</p></li>
<li><p>Immettere uno o più nomi di dominio SIP, quindi fare clic su <strong>Aggiungi</strong>.</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sono richiesti almeno un Access Edge Server e un dominio SIP per completare il processo di provisioning. Il dominio SIP e l'Access Edge Server devono essere attivi, funzionanti e raggiungibili tramite rete.</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>Nell'elenco di <strong>Provider di servizi di messaggistica istantanea pubblici</strong> selezionare <strong>Skype</strong> e fare clic su <strong>Avanti</strong> per aggiungere le informazioni di contatto, quindi inviare la richiesta di provisioning.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Accedere al sito Web <strong>https://pic.lync.com</strong> utilizzando il Microsoft Windows Live ID.</p></li>
<li><p>Selezionare il tipo di contratto di licenza Microsoft.</p></li>
<li><p>Selezionare la casella di controllo, assicurandosi di avere letto e accettato i diritti di utilizzo del prodotto per Lync Server.</p></li>
<li><p>Nella pagina di <strong>avvio di una richiesta di provisioning</strong> fare clic sul collegamento appropriato per avviare una richiesta di provisioning:</p></li>
<li><p>Nella pagina di <strong>specifica delle informazioni di provisioning</strong> immettere il <strong>Servizio Access Edge (FQDN)</strong>. Ad esempio, <strong>accessedge.contoso.com</strong>.</p></li>
<li><p>Immettere uno o più nomi di dominio SIP, quindi fare clic su <strong>Aggiungi</strong>.</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sono richiesti almeno un Access Edge Server e un dominio SIP per completare il processo di provisioning. Il dominio SIP e l'Access Edge Server devono essere attivi, funzionanti e raggiungibili tramite rete.</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>Nell'elenco di <strong>Provider di servizi di messaggistica istantanea pubblici</strong> selezionare <strong>Skype</strong> e fare clic su <strong>Avanti</strong> per aggiungere le informazioni di contatto, quindi inviare la richiesta di provisioning.</p></li>
</ol></td>
</tr>
</tbody>
</table>


Dopo aver inviato la richiesta di provisioning, l'attivazione dell'account e l'abilitazione degli utenti alla connettività per messaggistica istantanea pubblica potrebbe richiedere fino a 30 giorni.

## Abilitazione della federazione e della connettività di messaggistica istantanea pubblica

Dopo aver inviato la richiesta di provisioning, è possibile concentrarsi sull'ambiente di Lync Server e le attività amministrative necessarie per configurare la connettività Lync-Skype. Le informazioni in questa sezione partono dal presupposto che l'amministratore di Lync Server abbia distribuito Lync Server e configurato l'accesso esterno. Per altre informazioni sulla configurazione dell'accesso esterno per Lync Server, vedere "Pianificazione dell'accesso utente esterno" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkID=273772](http://go.microsoft.com/fwlink/p/?linkid=273772) e "Distribuzione dell'accesso degli utenti esterni" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkID=27378](http://go.microsoft.com/fwlink/p/?linkid=27378).

Per preparare l'ambiente di Lync Server per la connettività Lync-Skype, l'amministratore di Lync Server deve eseguire le tre attività seguenti:

## 1\. Configurare federazione e PIC

La federazione è obbligatoria per consentire agli utenti di Skype di comunicare con quelli di Lync all'interno dell'organizzazione. Il servizio PIC (Public Instant Messaging Connectivity) è una classe di federazione e deve essere configurato per consentire agli utenti di Lync di comunicare con quelli di Skype. I servizi di federazione e PIC possono essere configurati tramite il Pannello di controllo di Lync Server, illustrato di seguito.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La federazione PIC non è più supportata da Live Communication Server 2005 SP1 o da Office Communications Server 2007. Le piattaforme supportate per la federazione PIC includono Lync Server 2013, Lync Server 2010 e Office Communications Server 2007 R2.</td>
</tr>
</tbody>
</table>


## 2\. Configurare almeno un criterio per il supporto dell'accesso utente federato

Un amministratore deve usare il Pannello di controllo di Lync Server per configurare uno o più criteri di accesso per gli utenti esterni per stabilire se gli utenti di Skype possono collaborare con utenti interni di Lync Server.

## 3\. Configurare l'impostazione per Lync del provider PIC di Skype

Un amministratore deve usare Lync Server Management Shell per configurare i criteri client di Lync per la visualizzazione di Skype come provider PIC aggiuntivo.


> [!NOTE]
> Gli utenti dei provider di servizi PIC (Public Instant Messaging Connectivity) non possono partecipare alle conferenze o alla messaggistica istantanea nell'organizzazione finché non si procede anche alla configurazione di almeno un criterio per il supporto della connettività di messaggistica istantanea pubblica (passaggio 2 di questa procedura).<BR>Per configurare i servizi di federazione e PIC, vedere "Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica" all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=306063">http://go.microsoft.com/fwlink/p/?LinkId=306063</A>.<BR>Per configurare almeno un criterio per il supporto dell'accesso utente federato, vedere "Configurare criteri per controllare l'accesso degli utenti pubblici" all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=306064">http://go.microsoft.com/fwlink/p/?LinkId=306064</A>.



1.  Aprire Lync Server Management Shell da un Lync Server Front End Server.

2.  Eseguire i due comandi seguenti:
    
      - Remove-CsPublicProvider -Identity Messenger
    
      - New-CsPublicProvider -Identity Skype -ProxyFqdn federation.messenger.msn.com -IconUrl "https://images.edge.messenger.live.com/Messenger\_16x16.png" -VerificationLevel 2 -Enabled 1

3.  Da un client Lync client adesso è possibile selezionare Skype come provider PIC e aggiungere un client Skype specificando il relativo account Microsoft. Inoltre, un utente Skype che ha eseguito l'unione e l'accesso con l'account Microsoft può inviare richieste di contatto agli utenti Lync. Per altre informazioni sugli account Microsoft, vedere [Cos'è un account Microsoft?](https://support.skype.com/it/faq/fa12059/what-is-a-microsoft-account). Per informazioni aggiuntive sull'aggiunta dei client a Lync, vedere [Uso della connettività Lync-Skype in Lync Server 2013 come utente finale](lync-server-2013-using-lync-skype-connectivity-as-an-end-user.md).

4.  Per informazioni dettagliate sulla modifica dei provider ospitati, vedere "Creare o modificare provider federati SIP ospitati" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=306065](http://go.microsoft.com/fwlink/p/?linkid=306065).

Sono così completate le attività amministrative da eseguire nel server per impostare la configurazione necessaria per la connettività Lync-Skype.

## Altre risorse

[Uso della connettività Lync-Skype in Lync Server 2013 come utente finale](lync-server-2013-using-lync-skype-connectivity-as-an-end-user.md)

[Provisioning guide for Lync-Skype connectivity in Lync Server 2013](lync-server-2013-provisioning-guide-for-lync-skype-connectivity.md)

