---
title: Elenco di controllo di distribuzione per Web Conferencing
TOCTitle: Elenco di controllo di distribuzione per Web Conferencing
ms:assetid: 9908ebe0-e5d3-4920-b9b1-85021f7e69e9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205104(v=OCS.15)
ms:contentKeyID: 49301435
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per Web Conferencing

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Come per la distribuzione degli altri componenti di Lync Server 2013, la distribuzione di Web Conferencing richiede l'uso di Generatore di topologie per creare e pubblicare una topologia che incorpori i servizi per conferenze.

## Sequenza di distribuzione

È possibile distribuire i servizi per conferenze contemporaneamente alla distribuzione della topologia iniziale oppure dopo aver distribuito almeno un pool Front End o server Standard Edition.

## Processo di distribuzione dei servizi per conferenze

Nella tabella seguente è disponibile una panoramica dei passaggi necessari per distribuire i servizi per conferenza in una topologia esistente.


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
<td><p>I servizi per conferenze vengono eseguiti sui Front End Server in un pool Front End e nei server Standard Edition. Non sono necessari ulteriori requisiti hardware o software oltre a quelli necessari per installare questi server.</p>

> [!NOTE]
> Lync Server 2013 usa Office Web Apps e Server Office Web Apps per gestire la condivisione e il rendering di presentazioni di PowerPoint. Per informazioni sull'installazione e la configurazione di Server Office Web Apps, vedere <A href="lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md">Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013</A>.


</td>
<td><p>Utente del dominio membro del gruppo Administrators locale</p></td>
<td><p><a href="lync-server-2013-supported-hardware.md">Hardware supportato per Lync Server 2013</a> nella documentazione relativa alla supportabilità</p>
<p><a href="lync-server-2013-server-software-and-infrastructure-support.md">Supporto dell'infrastruttura e del software server in Lync Server 2013</a> nella documentazione relativa alla supportabilità</p>
<p><a href="lync-server-2013-determining-your-system-requirements.md">Determinazione dei requisiti di sistema per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p>
<p><a href="lync-server-2013-technical-requirements-for-archiving.md">Requisiti tecnici per l'archiviazione in Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><strong>Creare la topologia interna appropriata per supportare i servizi per conferenze</strong></p></td>
<td><p>Eseguire il Generatore di topologie per aggiungere i servizi per conferenze alla topologia e quindi pubblicarla.</p></td>
<td><p>Per definire una topologia, un account membro del gruppo Users locale</p>
<p>Per pubblicare la topologia, un account membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins e provvisto di autorizzazioni di controllo completo (lettura/scrittura/modifica) sulla condivisione di file da usare per l'archivio file di Lync Server 2013 (così che il Generatore di topologie possa configurare gli elenchi DACL necessari)</p></td>
<td><p><a href="lync-server-2013-define-and-configure-a-topology-in-topology-builder.md">Definire e configurare una topologia in Generatore di topologie per Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p><strong>Configurare i criteri e il supporto per i servizi per conferenze</strong></p></td>
<td><p>Usare Pannello di controllo di Lync Server 2013 o Lync Server Management Shell per configurare le impostazioni dei servizi per conferenze.</p></td>
<td><p>Gruppo RTCUniversalServerAdmins (solo Windows PowerShell) o assegnare utenti al ruolo [] o CSAdministrator</p></td>
<td><p><a href="lync-server-2013-conferencing-policies.md">Criteri conferenza in Lync Server 2013</a> nella documentazione sulle operazioni.</p></td>
</tr>
</tbody>
</table>


Lync Server 2013 ora include l'impostazione **MaxUploadFileSizeMb**, che limita le dimensioni dei file caricabili durante una riunione. Il valore predefinito per questa impostazione è di 500 MB. È possibile modificare **MaxUploadFileSizeMb** mediante il cmdlet **Set-CsConferencingConfiguration**.

**MaxUploadFileSizeMb** non limita l'impostazione di caricamento dei file per Lync Web App. Il limite delle dimensioni per il caricamento dei file per Lync Web App è impostato su circa 30 MB ed è controllato dal file web.config di IIS: /DataCollabWeb/Int\[Ext\]/Handler/web.config. Per configurare il limite di caricamento dei file per Lync Web App, aggiornare `maxRequestLength` e `maxAllowedContentLength` nel file web.config come visualizzato sotto.

    <system.web>
        <!-- 
            Since this handler is used to upload files to DMCU the request size (in kilobytes) 
            has to fit max allowed file size uploaded by LWA client.
            The timeout has to reflect the min client bandwidth. Timeout of 600 secs 
            and 512 Kbits of *client* bandwidth would result into aproximately 30 Mbytes 
            for LWA upload size limit.
        -->
          <httpRuntime maxRequestLength="500000" executionTimeout="600" />
    
    
    
                    <security>
                    <requestFiltering>
                               <requestLimits maxAllowedContentLength="524288000" />
                    </requestFiltering>
                    </security>

È necessario aggiornare il file web.config per ogni Front End Server.

