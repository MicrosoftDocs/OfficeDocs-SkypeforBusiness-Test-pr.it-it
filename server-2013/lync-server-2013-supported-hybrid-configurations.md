---
title: 'Lync Server 2013: Configurazioni ibride supportate'
TOCTitle: Configurazioni ibride supportate
ms:assetid: 5d456d6c-ad71-420c-b6d8-4d9cd0324f86
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945633(v=OCS.15)
ms:contentKeyID: 52062169
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazioni ibride di Lync Server 2013 supportate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile configurare le distribuzioni di Lync Server 2013 per l'integrazione con Microsoft Exchange Server 2010, Microsoft Exchange Server 2013 e SharePoint Server, sia in locale che online. Le funzionalità elencate nella tabella seguente sono supportate con tutti i client se non diversamente specificato. Per ulteriori informazioni sul supporto client, vedere [Tabelle di confronto dei client per Lync Server 2013](lync-server-2013-desktop-client-comparison-tables.md) e le tabelle di confronto dei client Lync Online in [Client per Lync Online](http://go.microsoft.com/fwlink/p/?linkid=281902).

## Integrazione con Exchange Server

Nella tabella seguente sono elencate le funzionalità supportate in una distribuzione ibrida in caso di integrazione con Microsoft Exchange Server.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Exchange in locale</th>
<th>Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Lync Server 2013 in locale</strong></p></td>
<td><ul>
<li><p>Messaggistica istantanea/presenza in Outlook</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-im-and-presence.md">Messaggistica istantanea e presenza in Lync Server 2013</a></p></li>
<li><p>Pianificazione e partecipazione a riunioni online tramite Outlook</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-integrating-with-microsoft-exchange-server-2013.md">Integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013</a></p></li>
<li><p>Messaggistica istantanea/presenza in Outlook Web App</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-lync-server-in-a-cross-premises-environment.md">Configurazione di Microsoft Lync Server 2013 in un ambiente cross-premise</a></p></li>
<li><p>Pianificazione e partecipazione a riunioni online tramite Outlook Web App</p></li>
<li><p>Messaggistica istantanea/presenza nei client mobili</p></li>
<li><p>Partecipazione a riunioni online da client mobili</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-deploying-mobility.md">Distribuzione delle funzionalità per dispositivi mobili in Lync Server 2013</a></p></li>
<li><p>Pubblicazione dello stato in base alle informazioni sulla disponibilità nel calendario di Outlook</p></li>
<li><p>Elenco di contatti (tramite archivio contatti unificato)</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-lync-server-to-use-the-unified-contact-store.md">Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archivio contatti unificato</a></p>
<div class="alert">

> [!NOTE]
> Richiede Exchange 2013.<BR>È necessario un client desktop Lync 2013.


</div></li>
<li><p>Foto ad alta risoluzione del contatto nel client Lync 2013 e in Lync Web App</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-the-use-of-high-resolution-photos.md">Configurazione dell'utilizzo delle foto ad alta risoluzione in Microsoft Lync Server 2013</a></p>
<div class="alert">

> [!NOTE]
> Richiede Exchange 2013.


</div></li>
<li><p>Delega delle riunioni</p>
<p>Supportata solo quando entrambi gli utenti sono ospitati online nella stessa foresta oppure quando sono entrambi ospitati in locale.</p></li>
<li><p>La cronologia delle conversazioni non effettuate e i registri delle chiamate vengono scritti nella cassetta postale di Exchange dell'utente</p></li>
<li><p>Archiviazione di contenuto (messaggistica istantanea e riunioni) in Exchange</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-deployment-checklist-for-archiving.md">Elenco di controllo di distribuzione per l'archiviazione in Lync Server 2013</a></p>
<div class="alert">

> [!NOTE]
> Richiede Exchange 2013.


</div></li>
<li><p>Ricerca nel contenuto archiviato</p>
<div class="alert">

> [!NOTE]
> Richiede Exchange 2013.


</div></li>
<li><p>Segreteria telefonica</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md">Distribuzione della messaggistica unificata di Exchange in locale per fornire la funzionalità di segreteria telefonica di Lync Server 2013</a></p></li>
</ul></td>
<td><ul>
<li><p>Messaggistica istantanea/presenza in Outlook</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md">Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online</a></p></li>
<li><p>Pianificazione e partecipazione a riunioni online tramite Outlook</p></li>
<li><p>Messaggistica istantanea/presenza in Outlook Web App</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md">Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online</a></p></li>
<li><p>Pianificazione e partecipazione a riunioni online da Outlook Web App</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md">Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online</a></p></li>
<li><p>Messaggistica istantanea/presenza nei client mobili</p></li>
<li><p>Partecipazione a riunioni online da client mobili</p></li>
<li><p>Pubblicazione dello stato in base alle informazioni sulla disponibilità nel calendario di Outlook</p></li>
<li><p>Elenco di contatti (tramite archivio contatti unificato). Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-lync-server-to-use-the-unified-contact-store.md">Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archivio contatti unificato</a></p>
<div class="alert">

> [!NOTE]
> Solo Lync Server 2013. È necessario un client desktop Lync 2013.


</div></li>
<li><p>Foto ad alta risoluzione del contatto nel client Lync 2013 e in Lync Web App</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-configuring-the-use-of-high-resolution-photos.md">Configurazione dell'utilizzo delle foto ad alta risoluzione in Microsoft Lync Server 2013</a>.</p></li>
<li><p>Delega delle riunioni</p>
<p>Supportata solo quando entrambi gli utenti sono ospitati online nella stessa foresta oppure quando sono entrambi ospitati in locale.</p></li>
<li><p>La cronologia delle conversazioni non effettuate e i registri delle chiamate vengono scritti nella cassetta postale di Exchange dell'utente</p></li>
<li><p>Archiviazione di contenuto (messaggistica istantanea e riunioni) in Exchange.</p>
<p>Per ulteriori informazioni, vedere <a href="lync-server-2013-deployment-checklist-for-archiving.md">Elenco di controllo di distribuzione per l'archiviazione in Lync Server 2013</a></p></li>
<li><p>Ricerca di contenuto archiviato. Per ulteriori informazioni, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=285448">Configurare Exchange per SharePoint eDiscovery Center</a>.</p></li>
<li><p>Segreteria telefonica. Per ulteriori informazioni, vedere <a href="lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md">Fornire agli utenti di Lync Server 2013 la segreteria telefonica nella messaggistica unificata di Exchange ospitata</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Lync Online</strong></p></td>
<td><ul>
<li><p>Messaggistica istantanea e presenza in Outlook</p></li>
<li><p>Pianificazione e partecipazione a riunioni online tramite Outlook</p></li>
<li><p>Messaggistica istantanea/presenza nei client mobili</p></li>
<li><p>La cronologia delle conversazioni non effettuate e i registri delle chiamate vengono scritti nella cassetta postale di Exchange dell'utente</p></li>
<li><p>Foto ad alta risoluzione del contatto nel client Lync 2013.</p>
<div class="alert">

> [!NOTE]
> Richiede Microsoft Exchange Server 2013. Non supportata in Lync Web App quando gli utenti sono ospitati in Skype for Business online.


</div></li>
<li><p>Partecipazione a riunioni online da client mobili</p></li>
<li><p>Pubblicazione dello stato in base alle informazioni sulla disponibilità nel calendario di Outlook</p></li>
<li><p>Delega delle riunioni</p>
<p>Supportata solo quando entrambi gli utenti sono ospitati online nella stessa foresta oppure quando sono entrambi ospitati in locale.</p></li>
</ul></td>
<td><ul>
<li><p>Messaggistica istantanea/presenza in Outlook</p></li>
<li><p>Pianificazione e partecipazione a riunioni online tramite Outlook</p></li>
<li><p>Messaggistica istantanea/presenza in Outlook Web App</p></li>
<li><p>Pianificazione e partecipazione a riunioni online da Outlook Web App</p></li>
<li><p>Messaggistica istantanea/presenza nei client mobili</p></li>
<li><p>Partecipazione a riunioni online da client mobili</p></li>
<li><p>Pubblicazione dello stato in base alle informazioni sulla disponibilità nel calendario di Outlook</p></li>
<li><p>La cronologia delle conversazioni non effettuate e i registri delle chiamate vengono scritti nella cassetta postale di Exchange dell'utente</p></li>
<li><p>Elenco di contatti (tramite archivio contatti unificato)</p>
<div class="alert">

> [!NOTE]
> Richiesto client Lync Server 2013


</div></li>
<li><p>Foto ad alta risoluzione del contatto nel client Lync 2013 e in Lync Web App</p></li>
<li><p>Delega delle riunioni</p>
<p>Supportata solo quando entrambi gli utenti sono ospitati online nella stessa foresta oppure quando sono entrambi ospitati in locale.</p></li>
<li><p>Archiviazione di contenuto (messaggistica istantanea e riunioni) in Exchange</p></li>
<li><p>Ricerca nel contenuto archiviato</p></li>
<li><p>Segreteria telefonica</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Integrazione con SharePoint

Nella tabella seguente sono elencate le funzionalità supportate in una distribuzione ibrida di Lync Server 2013 in caso di integrazione con SharePoint.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>SharePoint in locale</th>
<th>SharePoint Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Lync Server 2013 in locale</strong></p></td>
<td><ul>
<li><p>Ricerca nelle competenze</p></li>
<li><p>Presenza in SharePoint</p></li>
</ul></td>
<td><ul>
<li><p>Presenza in SharePoint</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Lync Online</strong></p></td>
<td><ul>
<li><p>Presenza in SharePoint</p></li>
</ul></td>
<td><ul>
<li><p>Presenza in SharePoint</p></li>
</ul></td>
</tr>
</tbody>
</table>

