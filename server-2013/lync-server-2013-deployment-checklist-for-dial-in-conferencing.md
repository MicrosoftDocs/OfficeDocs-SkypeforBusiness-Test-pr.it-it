---
title: 'Lync Server 2013: Elenco di controllo di distribuzione per le conferenze telefoniche con accesso esterno'
TOCTitle: Elenco di controllo di distribuzione per le conferenze telefoniche con accesso esterno
ms:assetid: 9c8d3ebe-0d70-4a61-9bd0-522286cddd9a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412726(v=OCS.15)
ms:contentKeyID: 49301455
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per le conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I componenti necessari per le conferenze telefoniche con accesso esterno vengono distribuiti insieme al carico di lavoro delle conferenze. Per poter configurare le conferenze telefoniche con accesso esterno, è necessario distribuire VoIP aziendale o un Mediation Server e un gateway PSTN (Public Switched Telephone Network).

Prima che gli utenti possano accedere dal PSTN per partecipare a una conferenza audio/video è necessario eseguire tutti i passaggi illustrati nella tabella seguente.


> [!NOTE]
> Se si sta eseguendo la migrazione da Office Communications Server 2007 R2, è necessario applicare all'ambiente Office Communications Server 2007 R2 gli aggiornamenti più recenti.



### Processo di distribuzione delle conferenze telefoniche con accesso esterno

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
<td><p><strong>Creare una topologia che includa il carico di lavoro delle conferenze, compresi un Mediation Server e un gateway PSTN, e distribuire il pool Front End o il server Standard Edition</strong>.</p></td>
<td><ol>
<li><p>Eseguire Generatore di topologie per configurare la topologia. Durante questa operazione, selezionare l'opzione relativa alle conferenze telefoniche con accesso esterno.</p></li>
<li><p>Pubblicare la topologia e distribuire il pool Front End o il server Standard Edition.</p></li>
<li><p>Se necessario, creare un Mediation Server autonomo e associarlo a un gateway PSTN.</p>
<div class="alert">

> [!NOTE]
> Questo passaggio è necessario solo se non si distribuisce VoIP aziendale e non si colloca il Mediation Server su Enterprise EditionFront End Server o sul server Standard Edition. Se si distribuisce VoIP aziendale, è necessario installare e configurare i Mediation Server e i gateway PSTN nell'ambito della distribuzione di VoIP aziendale. Se si colloca il Mediation Server, è necessario installare e configurare il Mediation Server come parte della distribuzione del pool Front End o del server Standard Edition.


</div></li>
</ol></td>
<td><p>Domain Admins</p>
<p>RTCUniversalServerAdmins</p>
<p>Amministratore</p></td>
<td><ul>
<li><p><a href="lync-server-2013-deploying-lync-server.md">Distribuzione di Lync Server 2013</a></p></li>
<li><p>Per creare un pool di Mediation Server autonomo: <a href="lync-server-2013-deploying-mediation-servers-and-defining-peers.md">Distribuzione di Mediation Server e definizione di peer in Lync Server 2013</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Configurare i dial plan</strong></p></td>
<td><p>Per dial plan si intende un insieme di regole di normalizzazione che consentono di convertire i numeri di telefono composti da una località specifica in un unico formato standard (E.164) ai fini dell'autorizzazione del telefono e del routing della chiamata. Lo stesso numero di telefono composto da diverse località può, in base ai rispettivi dial plan, essere risolto in numeri in formato E.164 diversi, appropriati per ogni località. Se si distribuisce VoIP aziendale i dial plan vengono impostati nell'ambito di tale distribuzione ed è necessario solo verificare che ammettano le conferenze telefoniche con accesso esterno. Se non si distribuisce VoIP aziendale, è necessario impostare i dial plan per le conferenze telefoniche con accesso esterno.</p>
<p>Utilizzare il Pannello di controllo di Lync Server 2013 o Lync Server Management Shell per impostare i dial plan come illustrato di seguito:</p>
<ol>
<li><p>Creare uno o più dial plan per il routing dei numeri di telefono per l'accesso esterno.</p></li>
<li><p>Assegnare un dial plan predefinito a ogni pool. Impostare <strong>Area conferenza telefonica con accesso esterno</strong> sulla località geografica a cui si applica il dial plan. L'area associa il dial plan ai numeri di accesso esterno.</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-dial-plans-for-dial-in-conferencing.md">Configurare dial plan per le conferenze telefoniche con accesso esterno in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Verificare che ai dial plan siano state assegnate aree</strong></p></td>
<td><p>Eseguire i cmdlet <strong>Get-CsDialPlan</strong> e <strong>Set-CsDialPlan</strong> per assicurarsi che a tutti i dial plan sia stata assegnata un'area.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-make-sure-dial-plans-have-assigned-regions.md">Verificare che ai dial plan in Lync Server 2013 siano state assegnate aree</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(Facoltativo) Verificare o modificare i requisiti relativi al PIN utente</strong></p></td>
<td><p>Usare il Pannello di controllo di Lync Server 2013 o Lync Server Management Shell per visualizzare o modificare i <strong>Criteri PIN</strong> per le conferenze. È possibile specificare la lunghezza minima del PIN, il numero massimo di tentativi di accesso, la scadenza del PIN e se i formati comuni sono consentiti o meno.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-verify-pin-policy-settings.md">(Facoltativo) Verificare le impostazioni dei criteri per il PIN in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Configurare i criteri di conferenza per il supporto delle conferenze telefoniche con accesso esterno</strong></p></td>
<td><p>Usare il Pannello di controllo di Lync Server 2013 o Lync Server Management Shell per configurare le impostazioni dei <strong>Criteri conferenza</strong> . Specificare se:</p>
<ul>
<li><p>La connessione remota conferenza PSTN è abilitata.</p></li>
<li><p>Gli utenti possono invitare partecipanti anonimi.</p></li>
<li><p>Gli utenti non autenticati possono partecipare a una conferenza utilizzando chiamate in uscita. Con le chiamate in uscita il server per conferenze telefona all'utente, il quale accederà alla conferenza rispondendo al telefono.</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-conferencing-policy-for-dial-in.md">Configurare i criteri di conferenza per l'accesso esterno in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong>Configurare i numeri di accesso esterno</strong></p></td>
<td><p>Utilizzare il Pannello di controllo di Lync Server 2013 o la Lync Server Management Shell per impostare numeri di accesso esterno che gli utenti possono chiamare per accedere alle conferenze e specificare le aree che associano il numero di accesso ai dial plan appropriati. I primi tre numeri di accesso per l'area specificata dal dial plan dell'organizzatore vengono inclusi nell'invito alla conferenza. Tutti i numeri di accesso sono disponibili nella pagina Impostazioni conferenza telefonica con accesso esterno.</p>
<div class="alert">

> [!NOTE]
> Dopo aver creato i numeri di accesso esterno, è possibile usare il cmdlet <STRONG>Set-CsDialInConferencingAccessNumber</STRONG> per modificare il nome visualizzato degli oggetti contatto di Active Directory in modo che gli utenti possano identificare più facilmente il numero di accesso corretto.


</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-dial-in-conferencing-access-numbers.md">Configurare i numeri di accesso per le conferenze telefoniche con accesso esterno in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>(Facoltativo) Verificare le impostazioni delle conferenze telefoniche con accesso esterno</strong></p></td>
<td><p>Utilizzare il <strong>Get-CsDialinConferencingAccessNumber</strong> per cercare i dial plan con un'area di conferenza telefonica con accesso esterno non utilizzata da alcun numero di accesso e i numeri di telefono ai quali non è assegnata un'area.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p>
<p>CsViewOnlyAdministrator</p>
<p>CsHelpDesk</p></td>
<td><p><a href="lync-server-2013-optional-verify-dial-in-conferencing-settings.md">(Facoltativo) Verificare le impostazioni delle conferenze telefoniche con accesso esterno in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(Facoltativo) Modificare il mapping dei tasti per i comandi DTMF</strong></p></td>
<td><p>Utilizzare il cmdlet <strong>Set-CsDialinConferencingDtmfConfiguration</strong> per modificare i tasti utilizzati per i comandi in multifrequenza (DTMF), che i partecipanti possono utilizzare per controllare le impostazioni della conferenza, ad esempio disattivare e riattivare l'audio o bloccare e sbloccare la conferenza.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-modify-key-mapping-for-dtmf-commands.md">(Facoltativo) Modificare il mapping dei tasti per i comandi DTMF in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>(Facoltativo) Modificare il comportamento degli annunci di partecipazione e abbandono delle conferenze</strong></p></td>
<td><p>Utilizzare il cmdlet <strong>Set-CsDialinConferencingConfiguration</strong> per modificare il funzionamento degli annunci quando i partecipanti prendono parte alle conferenze o ne escono.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-enable-and-disable-conference-join-and-leave-announcements.md">(Facoltativo) Abilitare e disabilitare gli annunci di partecipazione e abbandono delle conferenze in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(Facoltativo) Verificare le conferenze telefoniche con accesso esterno</strong></p></td>
<td><p>Utilizzare il cmdlet <strong>Test-CsDialInConferencing</strong> per verificare che i numeri di accesso per il pool specificato funzionino correttamente.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-verify-dial-in-conferencing.md">(Facoltativo) Verificare le conferenze telefoniche con accesso esterno in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Distribuire il componente aggiuntivo per riunioni online per Lync 2013</strong></p></td>
<td><p>Distribuire il componente aggiuntivo per riunioni online per Lync 2013 in modo che gli utenti possano pianificare conferenze che supportano l'accesso esterno. Il componente aggiuntivo per riunioni online per Lync 2013 viene installato automaticamente quando si installa Lync 2013</p></td>
<td><p>Administrators</p></td>
<td><p><a href="lync-server-2013-deploy-the-online-meeting-add-in-for-lync-2013.md">Distribuire il componente aggiuntivo per riunioni online per Lync 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong>Configurare le impostazioni degli account utente</strong></p></td>
<td><p>Usare il Pannello di controllo di Lync Server 2013 o Lync Server Management Shell per configurare il valore <strong>URI linea</strong> di telefonia come numero di telefono normalizzato univoco, ad esempio tel:+14255550200.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsAdministrator</p>
<p>CsUserAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-user-account-settings.md">Configurare le impostazioni degli account utente in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>(Scelta consigliata) Configurare le directory conferenza</p></td>
<td><p>Usare il cmdlet <strong>New-CsConferenceDirectory</strong> per creare una directory conferenza ogni 999 utenti del pool.</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-dial-in-conferencing-requirements.md">Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013</a> <a href="recommended-create-conference-directories.md">(Scelta consigliata) Creare le directory conferenze</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(Facoltativo) Inviare il messaggio di benvenuto agli utenti delle conferenze telefoniche con accesso esterno e impostare il PIN iniziale</strong></p></td>
<td><p>Utilizzare lo script <strong>Set-CsPinSendCAWelcomeMail</strong> per impostare i PIN iniziali degli utenti e inviare un messaggio di benvenuto tramite posta elettronica contenente il PIN iniziale e un collegamento alla pagina Impostazioni conferenza telefonica con accesso esterno.</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-optional-welcome-users-to-dial-in-conferencing.md">(Facoltativo) Presentazione della funzionalità di conferenza telefonica con accesso esterno agli utenti in Lync Server 2013</a></p></td>
</tr>
</tbody>
</table>

