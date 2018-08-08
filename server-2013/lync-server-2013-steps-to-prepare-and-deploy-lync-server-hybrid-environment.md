---
title: "Lync Server 2013: Passaggi per preparare e distribuire un ambiente ibrido LS"
TOCTitle: Passaggi per la preparazione e la distribuzione di un ambiente ibrido di Lync Server 2013
ms:assetid: a50d4f7b-63f4-4663-af63-56ca87e4e3e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205157(v=OCS.15)
ms:contentKeyID: 49301561
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Passaggi per la preparazione e la distribuzione di un ambiente ibrido di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella seguente vengono elencati i passaggi necessari per preparare l'ambiente a una distribuzione ibrida con Microsoft Lync Online e Microsoft Office 365.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Completato</th>
<th>Passaggio</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Creare un account tenant per Office 365 e abilitare Lync Online</p></td>
<td><p>Le informazioni su Office 365 e Lync Online sono disponibili all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=254980">Office 365</a>.</p>
<p>Per assicurarsi che l'ambiente sia pronto per Office 365, vedere i <a href="http://go.microsoft.com/fwlink/p/?linkid=401408">requisiti di sistema</a>.</p>
<p>Per informazioni dettagliate sulla configurazione di Office 365, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=254982">Introduzione a Office 365</a> e <a href="http://go.microsoft.com/fwlink/p/?linkid=254979">Configurazione di Office 365</a>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Aggiungere il dominio e verificare la proprietà</p></td>
<td><p>Il dominio viene talvolta detto anche <em>dominio personale</em> . Per confermare di essere il proprietario del dominio è necessario aggiungere il dominio al tenant di Office 365 e quindi seguire i passaggi per convalidare il dominio con Office 365.</p>
<p>Per aggiungere il dominio al tenant di Office 365, seguire i passaggi descritti in <a href="http://go.microsoft.com/fwlink/p/?linkid=254983">Aggiunta del dominio a Office 365</a>.</p>
<p>Completare tutti i passaggi di ogni sezione dell'argomento, incluso il passaggio &quot;Modifica dei record DNS per i servizi di Office 365&quot;.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verificare la conformità dell'ambiente</p></td>
<td><p>Per distribuire Office 365, è possibile utilizzare l'assistente installazione Office 365. Per ulteriori informazioni, vedere l'articolo sull'<a href="http://go.microsoft.com/fwlink/p/?linkid=254985">utilizzo dell'assistente installazione per verificare la conformità di Office 365</a></p>
<p>Per informazioni dettagliate sull'utilizzo dello strumento e la distribuzione di Office 365, vedere la <a href="http://go.microsoft.com/fwlink/p/?linkid=257337">guida alla distribuzione di Office 365</a>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Preparare la sincronizzazione di Active Directory</p></td>
<td><p>La sincronizzazione di Active Directory mantiene Active Directory in locale sempre sincronizzato con Office 365. In questo modo è possibile creare versioni sincronizzate di ogni account utente e gruppo di utenti e viene abilitata la sincronizzazione dell'elenco indirizzi globale dall'ambiente Microsoft Exchange Server locale a Microsoft Exchange Online.</p>

> [!IMPORTANT]
> È necessario sincronizzare gli account AD per tutti gli utenti Lync nell'organizzazione tra le distribuzioni di Lync in locale e online, anche se gli utenti non vengono spostati in Lync Online. Se gli utenti non vengono sincronizzati, la comunicazione tra utenti locali e online nell'organizzazione potrebbe non funzionare nella maniera desiderata.

<p>Per preparare l'ambiente alla sincronizzazione Active Directory, seguire i passaggi descritti in <a href="http://go.microsoft.com/fwlink/p/?linkid=254988">Roadmap sulla sincronizzazione della directory</a>, inclusa la configurazione di Single Sign-On.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Creare certificati per Active Directory Federation Services (ADFS)</p></td>
<td><p>Sarà necessario creare i certificati utilizzati per la federazione delle identità con Office 365. Per ulteriori informazioni, vedere la sezione &quot;Certificati server federativi&quot; dell'argomento Revisione dei requisiti per la distribuzione di AD FS all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=285376">Elenco di controllo: Utilizzo di ADFS per implementare e gestire l'accesso Single Sign-On</a>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Assegnare i certificati per ADFS</p></td>
<td><p>Dopo aver creato i certificati utilizzati per la federazione delle identità con Office 365, è necessario installarli e assegnarli.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Spostare gli utenti pilota in Skype for Business online</p></td>
<td><p>Dopo aver completato i passaggi per preparare e configurare l'ambiente per Skype for Business online, è possibile iniziare lo spostamento degli utenti pilota in Lync Online.</p>
<p>Vedere <a href="lync-server-2013-move-users-to-lync-online.md">Spostare utenti in Lync Online in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Amministrazione degli utenti in una distribuzione ibrida</p></td>
<td><p>Per informazioni dettagliate sull'amministrazione degli utenti in una distribuzione ibrida, vedere <a href="lync-server-2013-administering-users-in-a-hybrid-deployment.md">Amministrazione degli utenti in una distribuzione ibrida di Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

