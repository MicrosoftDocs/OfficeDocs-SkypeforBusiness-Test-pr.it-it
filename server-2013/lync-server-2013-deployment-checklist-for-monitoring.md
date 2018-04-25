---
title: 'Lync Server 2013: Elenco di controllo di distribuzione per il monitoraggio'
TOCTitle: Elenco di controllo di distribuzione per il monitoraggio
ms:assetid: 4e798370-277c-4391-84b4-13a972b45ca6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204874(v=OCS.15)
ms:contentKeyID: 49887557
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per il monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Anche se il monitoraggio è già installato e attivato in ciascun Front End Server, ci sono ancora alcuni passaggi da eseguire prima di poter iniziare a raccogliere dati di monitoraggio per Microsoft Lync Server 2013. Questi passaggi sono indicati nell'elenco di controllo seguente:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Fase</p></td>
<td><p>Passaggi</p></td>
<td><p>Ruolo e gruppo a cui è necessario appartenere</p></td>
<td><p>Documentazione</p></td>
</tr>
<tr class="even">
<td><p><strong>Installare l'hardware e il software prerequisiti</strong></p></td>
<td><p>Installare una versione supportata di Microsoft SQL Server nel computer con la funzione di archivio dati back-end per il monitoraggio.</p></td>
<td><p>Utente del dominio che è anche membro del gruppo degli amministratori locale.</p></td>
<td><p><a href="lync-server-2013-supported-hardware.md">Hardware supportato per Lync Server 2013</a> nella Guida relativa alla supportabilità</p>
<p><a href="lync-server-2013-server-software-and-infrastructure-support.md">Supporto dell'infrastruttura e del software server in Lync Server 2013</a> nella Guida relativa alla supportabilità</p></td>
</tr>
<tr class="odd">
<td><p><strong>Creare la topologia interna appropriata per supportare il monitoraggio</strong></p></td>
<td><p>Usare il Generatore di topologie di Lync Server 2013 per aggiungere database di monitoraggio alla topologia e quindi pubblicare la topologia aggiornata.</p></td>
<td><p>Per definire una topologia, un utente membro del gruppo degli utenti locale.</p>
<p>Per pubblicare la topologia, un utente membro del gruppo degli amministratori di dominio e del gruppo RTCUniversalServerAdmins.</p></td>
<td><p><a href="lync-server-2013-associating-a-monitoring-store-with-a-front-end-pool.md">Associazione di un archivio di monitoraggio a un pool Front End</a> nella Guida relativa alla distribuzione</p></td>
</tr>
<tr class="even">
<td><p><strong>Abilitare le impostazioni di monitoraggio appropriate</strong></p></td>
<td><p>Abilitare il monitoraggio della registrazione dettagli chiamata e/o della qualità percepita dagli utenti per l'ambito globale e/o di sito.</p></td>
<td><p>Un utente membro del gruppo RTCUniversalServerAdmins o a cui è assegnato un ruolo del controllo di accesso basato sui ruoli che consente l'accesso ai cmdlet CsCdrConfiguration e CsQoEConfiguration.</p></td>
<td><p><a href="lync-server-2013-configuring-call-detail-recording-and-quality-of-experience-settings.md">Configurazione delle impostazioni di Registrazione dettagli chiamata e Qualità percepita dagli utenti</a> nella Guida relativa alle operazioni</p></td>
</tr>
</tbody>
</table>

