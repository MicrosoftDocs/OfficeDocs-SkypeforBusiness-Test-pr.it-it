---
title: 'Lync Server 2013: Elenco di controllo di distribuzione per il server Chat persistente'
TOCTitle: Elenco di controllo di distribuzione per il server Chat persistente
ms:assetid: b1108f8f-88a2-4660-8086-d25ba76f7239
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412851(v=OCS.15)
ms:contentKeyID: 49301688
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per il server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per distribuire il server Chat persistente di Lync Server 2013 è necessario utilizzare la sequenza di distribuzione corretta ed eseguire tutti i passaggi necessari.

## Sequenza di distribuzione

È possibile distribuire il server Chat persistente dopo la distribuzione della topologia iniziale, includendo almeno un pool Front End di Lync Server 2013 o un server Standard Edition di Lync Server 2013. In questo argomento viene descritto come distribuire il server Chat persistente aggiungendolo a una distribuzione esistente.

## Processo di distribuzione

Nella tabella seguente vengono descritti i passaggi di base da eseguire per distribuire il server Chat persistente, con l'indicazione di collegamenti che consentono di accedere a ulteriori informazioni.

### Processo di distribuzione del server Chat persistente

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attività</th>
<th>Passaggi</th>
<th>Appartenenze a gruppi e ruoli richiesti</th>
<th>Argomenti correlati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Installare l'hardware e il software prerequisiti</strong></p></td>
<td><p>Nell'hardware che soddisfa i requisiti di sistema installare gli elementi seguenti:</p><ul><li><p>Nei Front End Server del server Chat persistente:</p></li></ul><ul><li><p>Sistema operativo che soddisfa i requisiti di sistema seguenti</p></li><li><p>Prerequisiti software per i computer che eseguono Lync Server 2013</p></li><li><p>SQL Server nel server che ospiterà il database del server Chat persistente</p></li></ul>
<p>Se è necessaria la conformità di server Chat persistente:</p><ul><li><p>SQL Server nel server che ospiterà il database di conformità del server Chat persistente</p></li></ul></td>
<td><p>Tutti gli utenti membri del gruppo Administrators locale.</p></td>
<td><p><a href="lync-server-2013-supported-hardware.md">Hardware supportato per Lync Server 2013</a> nella documentazione relativa al supporto</p>
<p><a href="lync-server-2013-server-software-and-infrastructure-support.md">Supporto dell'infrastruttura e del software server in Lync Server 2013</a> nella documentazione relativa al supporto</p>
<p><a href="lync-server-2013-determining-your-system-requirements.md">Determinazione dei requisiti di sistema per Lync Server 2013</a></p>
<p><a href="lync-server-2013-technical-requirements-for-persistent-chat-server.md">Requisiti tecnici per il server Chat persistente in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong>Creare la topologia interna appropriata per supportare il server Chat persistente (e facoltativamente la conformità di Chat persistente)</strong></p></td>
<td><p>Eseguire Generatore di topologie per aggiungere un pool di server Chat persistente alla topologia:</p><ul><li><p>Aggiungere i componenti del server Chat persistente alla topologia</p></li><li><p>Creare un database di SQL Server per l'archivio del server Chat persistente (e un'istanza di SQL Server di backup per il ripristino di emergenza)</p></li><li><p>Definire un nuovo archivio file di Lync oppure utilizzare un archivio file di Lync esistente per i file del server Chat persistente</p></li><li><p>Associare il pool di Lync Server 2013 che può instradare le richieste a questo pool di server Chat persistente</p></li></ul>
<p>Se è necessaria la conformità di Chat persistente:</p><ul><li><p>Aggiungere l'archivio di conformità di Chat persistente</p></li><li><p>Selezionare la casella di controllo relativa alla definizione del pool di server Chat persistente per abilitare la conformità</p></li><li><p>Pubblicare la topologia</p></li></ul>
<p>Se si installa il server Chat persistente in un server Standard Edition, il nome di dominio completo (FQDN) del pool di server Chat persistente deve corrispondere al server Standard Edition e i database di SQL Server sono collocati nell'istanza di SQL Server Express nel server Standard Edition.</p></td>
<td><p>Per definire una topologia, un account membro del gruppo Users locale.</p>
<p>Per pubblicare la topologia, un account membro dei gruppi Domain Admins e RTCUniversalServerAdmins. L'utente inoltre deve disporre delle autorizzazioni di controllo completo (lettura/scrittura/modifica) sull'archivio file di Lync per i file del server Chat persistente (in modo che Generatore di topologie possa configurare gli elenchi DACL necessari).</p></td>
<td><p><a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p><strong>Distribuire il server Chat persistente</strong></p></td>
<td><p>Eseguire l'installazione di Lync Server in tutti i computer che eseguono il server Chat persistente. L'installazione del server Chat persistente è integrata nella Distribuzione guidata di Lync Server 2013, che fornisce le istruzioni seguenti:</p><ul><li><p>Distribuire l'archivio di gestione locale</p></li><li><p>Installare i servizi del server Chat persistente</p></li><li><p>Richiedere e assegnare i certificati</p></li><li><p>Eseguire e avviare i servizi</p></li></ul></td>
<td><p>Tutti gli utenti membri del gruppo Administrators locale.</p></td>
<td><p><a href="lync-server-2013-deploying-persistent-chat-server.md">Distribuzione del server Chat persistente in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="even">
<td><p><strong>Creare un amministratore di Chat persistente</strong></p></td>
<td><p>Aggiungere gli utenti al gruppo di sicurezza CsPersistentChatAdministrator.</p></td>
<td><p>Tutti gli utenti membri del gruppo degli amministratori di dominio.</p></td>
<td><p><a href="lync-server-2013-adding-a-persistent-chat-administrator.md">Aggiunta di un amministratore di Chat persistente in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p><strong>Configurare il server Chat persistente</strong></p></td>
<td><p>Configurare gli utenti:</p><ul><li><p>L'utente deve essere abilitato tramite criteri ad accedere al server Chat persistente. Per impostazione predefinita, i criteri sono disattivati per tutti gli utenti e possono essere definiti nell'ambito globale, del sito, del pool e dell'utente</p></li><li><p>Configurare le impostazioni</p></li></ul></td>
<td><p>L'utente deve essere membro di CsPersistentChatAdministrator. Per modificare i criteri, l'utente deve essere almeno membro di CsUserAdministrator.</p></td>
<td><p><a href="lync-server-2013-configuring-persistent-chat-server.md">Configurazione del server Chat persistente in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> È possibile distribuire uno o più pool di server Chat persistente. Sono supportati più pool di server Chat persistente per motivi legali e normativi in base ai quali i dati generati in una determinata area devono restare in tale area. Se ad esempio si distribuisce un pool di server Chat persistente a Chicago e un altro a Zurigo per conformità alle normative relative ai dati della Svizzera, gli utenti potranno connettersi alle chat room in entrambi i pool di server Chat persistente, purché dispongano dell'accesso.
