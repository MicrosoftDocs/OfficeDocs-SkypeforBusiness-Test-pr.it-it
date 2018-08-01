---
title: 'Lync Server 2013: Processo di distribuzione per Response Group'
TOCTitle: Processo di distribuzione per Response Group
ms:assetid: d390c8a1-dc6e-44d8-b386-2be1fca9877c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205270(v=OCS.15)
ms:contentKeyID: 49302080
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione viene fornita una panoramica delle fasi e delle operazioni necessarie per la distribuzione dell' applicazione Response Group.

### Processo di distribuzione di Response Group

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
<td><p>Installazione dell' applicazione Response Group</p></td>
<td><p>L' applicazione Response Group viene installata e attivata per impostazione predefinita quando si distribuisce VoIP aziendale.</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-deploying-enterprise-voice.md">Distribuzione di VoIP aziendale in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Installazione dei componenti per Response Group</p></td>
<td><p>I cmdlet di Lync Server, il Pannello di controllo di Lync Server, lo Strumento di configurazione di Response Group, la console di accesso e di disconnessione degli agenti e il servizio Web client di Response Group vengono installati come parte dei servizi Web. I servizi Web vengono installati quando si distribuisce un pool Enterprise Edition o un server Standard Edition.</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-deploying-lync-server.md">Distribuzione di Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Abilitazione degli utenti per Lync 2013 e per VoIP aziendale</p></td>
<td><p>Abilitare gli utenti che saranno gli agenti di Lync Server e VoIP aziendale. Gli utenti devono essere abilitati per poter essere aggiunti a gruppi di agenti. Gli utenti in genere vengono abilitati per Lync Server durante la distribuzione di Enterprise Edition o server Standard Edition. Gli utenti vengono abilitati per VoIP aziendale durante la distribuzione di VoIP aziendale.</p></td>
<td><p>RTCUniversalUserAdmins</p>
<p>CsUserAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md">Disabilitare o abilitare nuovamente gli account utente per Lync Server</a></p>
<p><a href="lync-server-2013-enable-users-for-enterprise-voice.md">Abilitare gli utenti per VoIP aziendale in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Creazione e configurazione di Response Group, costituiti da gruppi di agenti, code e flussi di lavoro</p></td>
<td><ol>
<li><p>Utilizzare il Pannello di controllo di Lync Server o Lync Server Management Shell per eseguire le operazioni seguenti:</p>
<ol>
<li><p>Creare e configurare gruppi di agenti.</p></li>
<li><p>Creare e configurare code.</p></li>
</ol></li>
<li><p>Facoltativamente, utilizzare Lync Server Management Shell per creare l'orario di ufficio e le festività per Response Group predefiniti.</p></li>
<li><p>Utilizzare lo Strumento di configurazione di Response Group o Lync Server Management Shell per creare flussi di lavoro, ovvero gruppi di risposta o flussi di chiamate IVR (Interactive Voice Response), inclusi l'orario di ufficio e le festività per Response Group personalizzati.</p>


> [!NOTE]
> Per accedere allo Strumento di configurazione di Response Group, è possibile utilizzare il Pannello di controllo di Lync Server.


</li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p>
<p>CsResponseGroupManager</p></td>
<td><p><a href="lync-server-2013-create-response-group-agent-groups.md">Creare gruppi di agenti per Response Group in Lync Server 2013</a></p>
<p><a href="lync-server-2013-create-response-group-queues.md">Creare code di Response Group in Lync Server 2013</a></p>
<p><a href="lync-server-2013-optional-define-response-group-business-hours.md">Definire l'orario di ufficio dei Response Group (facoltativo) in Lync Server 2013</a></p>
<p><a href="lync-server-2013-optional-define-response-group-holiday-sets.md">Definire gli insiemi di festività dei Response Group (facoltativo)</a></p>
<p><a href="lync-server-2013-create-or-modify-a-workflow.md">Creare o modificare un flusso di lavoro</a></p></td>
</tr>
<tr class="odd">
<td><p>(Facoltativo) Personalizzazione delle impostazioni a livello di applicazione</p></td>
<td><p>Utilizzare Lync Server Management Shell per personalizzare la configurazione della musica di attesa predefinita, il file audio della musica di attesa predefinito, il periodo di tolleranza di richiamata degli agenti e la configurazione del contesto chiamata.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-managing-application-level-response-group-settings.md">Gestione delle impostazioni dei Response Group a livello di applicazione</a></p></td>
</tr>
<tr class="even">
<td><p>(Facoltativo) Delega della gestione dei Response Group</p></td>
<td><p>Assegnare agli utenti il ruolo CsResponseGroupManager per delegare la configurazione dei Response Group. I responsabili dei Response Group possono quindi configurare i Response Group che sono stati loro assegnati.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Verifica della distribuzione di Response Group</p></td>
<td><p>Testare le risposte alle chiamate nei flussi di lavoro del gruppo di risposta e del sistema IVR per verificare che la configurazione funzioni come previsto.</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
</tbody>
</table>

