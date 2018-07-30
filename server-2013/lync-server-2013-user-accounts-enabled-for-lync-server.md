---
title: Account utente abilitati per Lync Server 2013
TOCTitle: Account utente abilitati per Lync Server 2013
ms:assetid: 8021087e-5084-4a39-9fef-ab9376c6d371
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182543(v=OCS.15)
ms:contentKeyID: 49301132
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Account utente abilitati per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Negli argomenti di questa sezione vengono descritte le procedure dettagliate relative alla configurazione delle impostazioni utente che è possibile eseguire utilizzando il Pannello di controllo di Lync Server 2013.

> [!IMPORTANT]  
> Non è possibile utilizzare il Pannello di controllo di Lync Server per gestire gli utenti membri del gruppo Domain Admins di Active Directory. Per tali utenti, è possibile utilizzare il Pannello di controllo di Lync Server solo per eseguire operazioni di ricerca di sola lettura. Per eseguire operazioni di scrittura per gli utenti del gruppo Domain Admins (ad esempio abilitarli o disabilitarli per Pannello di controllo di Lync Server o modificare le assegnazioni di criteri o pool, le impostazioni di telefonia o l'indirizzo SIP), è necessario utilizzare i cmdlet di Windows PowerShell dopo avere eseguito l'accesso come utente incluso nel gruppo Domain Admins. Per informazioni dettagliate sull'utilizzo dei cmdlet di Windows PowerShell per gestire gli utenti, vedere <a href="lync-server-2013-lync-server-management-shell.md">Lync Server Management Shell</a>.

Quando si esegue qualsiasi attività amministrativa di Lync Server 2013 che implica la ricerca di un utente o il filtro dei risultati della ricerca di utenti, vi sono alcune proprietà utente presenti come attributi in Servizi di dominio Active Directory che non vengono replicate nel catalogo globale fino a quando non viene completata la distribuzione di Microsoft Exchange Server. Microsoft Exchange, e non Lync Server, contrassegna gli attributi seguenti per la replica nel catalogo globale quando viene installato:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Informazioni utente</th>
<th>Indirizzo e telefono</th>
<th>Organizzazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Iniziali</p></td>
<td><p>Indirizzo</p>
<p>Paese</p>
<p>Cercapersone</p>
<p>Fax</p>
<p>Cellulare</p></td>
<td><p>Titolo</p>
<p>Società</p>
<p>Reparto</p>
<p>Office</p></td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Visualizzazione delle informazioni sugli account utente abilitati per Lync Server 2013](lync-server-2013-viewing-information-about-user-accounts-enabled-for-lync-server.md)

  - [Abilitazione e disabilitazione degli utenti per Lync Server 2013](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

  - [Gestione di VoIP aziendale per gli utenti](lync-server-2013-managing-enterprise-voice-for-users.md)

  - [Modifica delle proprietà degli account utente](lync-server-2013-modifying-user-account-properties.md)

  - [Gestire i criteri di accesso esterno per l'organizzazione in Lync Server 2013](lync-server-2013-manage-external-access-policy-for-your-organization.md)

  - [Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md)

## Vedere anche

#### Concetti

[Cmdlet per la gestione degli utenti](lync-server-2013-user-management-cmdlets.md)  

#### Ulteriori risorse

[Gestione degli utenti in Lync Server 2013](lync-server-2013-managing-users-in-lync-server.md)

