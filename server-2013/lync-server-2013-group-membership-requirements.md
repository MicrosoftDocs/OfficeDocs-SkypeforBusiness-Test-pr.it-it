---
title: 'Lync Server 2013: Requisiti di appartenenza ai gruppi'
TOCTitle: Requisiti di appartenenza ai gruppi
ms:assetid: 01876843-8717-4e72-baf5-866ac8cceee6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204623(v=OCS.15)
ms:contentKeyID: 49299488
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di appartenenza ai gruppi per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella seguente vengono riepilogati il gruppo o i gruppi a cui deve appartenere una persona per eseguire l'installazione, la gestione e la risoluzione dei problemi di Lync Server 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Eseguibile Lync Server 2013</th>
<th>Appartenenze ai gruppi richieste</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Setup.exe</strong> – File eseguibile che avvia l'installazione degli strumenti di amministrazione di Lync Server 2013.</p></td>
<td><p>Membro del gruppo Administrators locale nel computer da cui viene eseguito il file. Membro del gruppo Domain Users per la lettura delle informazioni in Servizi di dominio Active Directory. Questo livello di autorizzazione è necessario perché l'installazione automatica dei pacchetti MSI richiesti nel computer locale richiede privilegi che consentano la lettura e scrittura di risorse del computer locale protette, come le directory Programmi e l'hive Local Machine del Registro di sistema.</p>
<div class="alert">

> [!TIP]
> È inoltre possibile delegare le autorizzazioni per l'installazione a utenti o gruppi a cui non si desidera concedere l'appartenenza al gruppo Domain Admins. Per informazioni dettagliate, vedere <a href="lync-server-2013-granting-setup-permissions.md">Concessione di autorizzazioni di installazione in Lync Server 2013</a> nella documentazione relativa alla distribuzione. 

</div></td>
</tr>
<tr class="even">
<td><p><strong>Deploy.exe</strong> – Chiamato da setup.exe, deploy.exe è responsabile per la distribuzione dei componenti software per i ruoli del server.</p></td>
<td><p>Membro del gruppo Administrators locale nel computer da cui viene eseguito il file. Membro del gruppo Domain Users per la lettura delle informazioni in Servizi di dominio Active Directory. Questo livello di autorizzazione è necessario perché l'installazione automatica dei pacchetti MSI richiesti nel computer locale richiede privilegi che consentano la lettura e scrittura di risorse del computer locale protette, come le directory Programmi e l'hive Local Machine del Registro di sistema. È necessaria l'appartenenza al gruppo RtcUniversalReadOnlyAdmins per leggere l' archivio di gestione centrale.</p>
<div class="alert">

> [!NOTE]
> Se si esegue sistema operativo Windows Vista o sistema operativo Windows 7, verrà visualizzata una richiesta di Controllo dell'account utente per confermare che si desidera procedere all'installazione. Se si è connessi con un account utente standard, sarà necessario che qualcuno membro del gruppo Administrators locale fornisca le credenziali quando viene richiesto di specificare un account che dispone delle autorizzazioni per l'installazione del software.


</div></td>
</tr>
<tr class="odd">
<td><p><strong>Bootstrapper.exe</strong> – Chiamato da setup.exe, bootstrapper.exe è responsabile della distribuzione e configurazione dei ruoli del server.</p></td>
<td><p>Membro del gruppo Administrators locale nel computer da cui viene eseguito il file. Membro del gruppo RTCUniversalServerAdmins per l'esecuzione di Bootstrapper.exe. Membro del gruppo Utenti di dominio per la lettura di informazioni in AD DS. Questo livello di autorizzazione è necessario perché l'installazione automatica dei pacchetti MSI richiesti nel computer locale richiede privilegi che consentano la lettura e scrittura di risorse del computer locale protette, come le directory Programmi e l'hive Local Machine del Registro di sistema.</p></td>
</tr>
<tr class="even">
<td><p><strong>TopologyBuilder</strong> : interfaccia utente basata su procedure guidate per creare, visualizzare, modificare e convalidare le topologie di Lync Server 2013.</p></td>
<td><p>Membro del gruppo Administrators locale nel computer da cui viene eseguito il file per visualizzare la topologia. Membro del gruppo RTCUniversalServerAdmins per modificare le impostazioni di configurazione. Membro del gruppo RTCUniversalServerAdmins e del gruppo Domain Admins oppure membro del gruppo RTCUniversalServerAdmins (solo se al gruppo sono state concesse le autorizzazioni per la delega dell'installazione) per pubblicare la topologia. Per informazioni dettagliate sulla delega delle autorizzazioni per l'installazione in modo da consentire ai membri del gruppo RTCUniversalServerAdmins di pubblicare la topologia senza essere membri del gruppo Domain Admins, vedere <a href="lync-server-2013-granting-setup-permissions.md">Concessione di autorizzazioni di installazione in Lync Server 2013</a> nella documentazione relativa alla distribuzione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AdminUIHost</strong> : interfaccia utente grafica basata sul Web per la gestione di Lync Server 2013.</p></td>
<td><p>Membro del gruppo CsAdministrator o di un altro ruolo di controllo di accesso basato sui ruoli a cui viene assegnata la specifica attività amministrativa. Il Pannello di controllo di Lync Server 2013 implementa le modifiche di configurazione tramite l'esecuzione di cmdlet Lync Server 2013 Management Shell. Per un elenco dei ruoli predefiniti e dei cmdlet che i membri sono autorizzati a eseguire, vedere <a href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerShell.exe con il modulo Lync Server 2013 caricato</strong> – Strumento di amministrazione della riga di comando con cmdlet specifici per la gestione di Lync Server 2013.</p></td>
<td><p>Membro del gruppo CsAdministrator o di un altro ruolo di controllo di accesso basato sui ruoli a cui viene assegnato il cmdlet specifico. Per un elenco dei ruoli predefiniti e dei cmdlet che i membri sono autorizzati a eseguire, vedere <a href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p>
<p>Oppure membro di uno o più dei gruppi seguenti, a seconda del cmdlet:</p>
<ul>
<li><p>RTCUniversalServerAdmins</p></li>
<li><p>RTCUniversalUserAdmins</p></li>
<li><p>RTCUniversalReadOnlyAdmins</p></li>
</ul></td>
</tr>
</tbody>
</table>

