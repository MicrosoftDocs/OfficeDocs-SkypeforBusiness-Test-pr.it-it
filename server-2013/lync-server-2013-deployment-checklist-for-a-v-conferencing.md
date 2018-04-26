---
title: Elenco di controllo di distribuzione per A/V Conferencing
TOCTitle: Elenco di controllo di distribuzione per A/V Conferencing
ms:assetid: 6d47426f-6559-407b-9ac1-2453f0b7a2a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619183(v=OCS.15)
ms:contentKeyID: 49300901
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per A/V Conferencing

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Analogamente alla distribuzione degli altri componenti di Lync Server 2013, la distribuzione delle conferenze A/V richiede l'utilizzo di Generatore di topologie per la creazione e pubblicazione di una topologia che incorpori le funzioni di conferenza.

## Sequenza di distribuzione

È possibile distribuire il server della conferenza mentre si distribuisce la topologia iniziale o dopo avere distribuito almeno un pool Front End o server Standard Edition.

## Processo di distribuzione delle funzioni di conferenza

Nella tabella seguente viene fornita una panoramica dei passaggi da eseguire per distribuire il supporto per la conferenza in una topologia esistente.


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
<th>Ruoli e gruppi a cui è necessario appartenere</th>
<th>Documentazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Installare l'hardware e il software prerequisiti</strong></p></td>
<td><p>La conferenza è eseguita sui Front End Server di un pool Front End e server Standard Edition. Non esistono ulteriori requisiti di hardware o software oltre a quelli necessari per l'installazione di questi server.</p>
<div class="alert">

> [!NOTE]
> Lync Server 2013 utilizza Office Web Apps e Server Office Web Apps per la gestione della condivisione e del rendering delle presentazioni di PowerPoint. Per ulteriori dettagli sull'installazione e configurazione di Server Office Web Apps, vedere <A href="lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md">Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013</A>.


</div></td>
<td><p>Utente del dominio membro del gruppo Administrators locale</p></td>
<td><p><a href="lync-server-2013-supported-hardware.md">Hardware supportato per Lync Server 2013</a> nella documentazione relativa alla supportabilità</p>
<p><a href="lync-server-2013-server-software-and-infrastructure-support.md">Supporto dell'infrastruttura e del software server in Lync Server 2013</a> nella documentazione relativa alla supportabilità</p>
<p><a href="lync-server-2013-determining-your-system-requirements.md">Determinazione dei requisiti di sistema per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p>
<p><a href="lync-server-2013-technical-requirements-for-archiving.md">Requisiti tecnici per l'archiviazione in Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><strong>Creare la topologia interna appropriata per supportare le funzioni di conferenza</strong></p></td>
<td><p>Eseguire Generatore di topologie per aggiungere le funzioni di conferenza alla topologia, quindi pubblicarla.</p></td>
<td><p>Per definire una topologia, un account membro del gruppo Users locale</p>
<p>Per pubblicare la topologia, un account che sia membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins e che disponga delle autorizzazioni di controllo completo (lettura/scrittura/modifica) sulla condivisione file da utilizzare per l'archivio file di Lync Server 2013 file store (in modo che Generatore di topologie possa configurare gli elenchi DACL necessari)</p></td>
<td><p><a href="lync-server-2013-define-and-configure-a-topology-in-topology-builder.md">Definire e configurare una topologia in Generatore di topologie per Lync Server 2013</a> nella documentazione relativa alla distribuzione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Configurare i criteri e il supporto per le funzioni di conferenza</strong></p></td>
<td><p>Utilizzare Pannello di controllo di Lync Server 2013 o Lync Server Management Shell per configurare le impostazioni di conferenza.</p></td>
<td><p>Gruppo RTCUniversalServerAdmins (solo Windows PowerShell) oppure assegnare gli utenti al ruolo [] o CSAdministrator</p></td>
<td><p><a href="lync-server-2013-conferencing-policies.md">Criteri conferenza in Lync Server 2013</a> nella documentazione relativa alle operazioni.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Ulteriori risorse

[Panoramica delle conferenze in Lync Server 2013](lync-server-2013-overview-of-conferencing.md)  
[Definizione dei requisiti per le conferenze in Lync Server 2013](lync-server-2013-defining-your-requirements-for-conferencing.md)

