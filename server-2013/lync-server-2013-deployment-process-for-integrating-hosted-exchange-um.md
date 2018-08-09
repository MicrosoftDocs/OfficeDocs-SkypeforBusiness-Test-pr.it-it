---
title: "Lync Server 2013: Distribuz. per integrare messaggi di Exchange ospitata"
TOCTitle: Processo di distribuzione per l'integrazione della messaggistica unificata di Exchange ospitata con Lync Server
ms:assetid: dbec9c38-7f66-419d-b8c3-c61380052cac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398968(v=OCS.15)
ms:contentKeyID: 49302179
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per l'integrazione della messaggistica unificata di Exchange ospitata con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per una pianificazione efficace dell'integrazione di Lync Server 2013 con la messaggistica unificata di Exchange ospitata è necessario tenere conto di quanto segue:

  - Prerequisiti per l'integrazione di Lync Server 2013 con la messaggistica unificata di Exchange ospitata

  - Passaggi necessari durante il processo di integrazione

## Prerequisiti della distribuzione per l'integrazione con la messaggistica unificata di Exchange ospitata

Prima di iniziare il processo di integrazione, è necessario che sia già stato distribuito Lync Server 2013 (almeno un pool Front End o un server Standard Edition), un server perimetrale e client Lync 2013 o Lync 2010.

## Processo di integrazione

Nella tabella seguente è riportata una panoramica del processo di integrazione della messaggistica unificata di Exchange ospitata. Per informazioni dettagliate sui passaggi di distribuzione, vedere [Fornire agli utenti di Lync Server 2013 la segreteria telefonica nella messaggistica unificata di Exchange ospitata](lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md) nella documentazione relativa alla distribuzione.


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
<th>Diritti e autorizzazioni</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configurare il server perimetrale.</p></td>
<td><ol>
<li><p>Configurare il server perimetrale per la federazione.</p></li>
<li><p>Replicare manualmente i dati nel server perimetrale.</p></li>
<li><p>Configurare il provider di hosting nel server perimetrale.</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-configure-the-edge-server-for-integration-with-hosted-exchange-um.md">Configurare il server perimetrale per l'integrazione con la messaggistica unificata di Exchange ospitata</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare i criteri della segreteria telefonica ospitata.</p></td>
<td><ol>
<li><p>Modificare i criteri globali della segreteria telefonica ospitata o crearne di nuovi con ambito a livello di sito o per utente.</p></li>
<li><p>Per i criteri con ambito per utente, assegnarli a utenti o gruppi.</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-manage-hosted-voice-mail-policies.md">Gestire i criteri di segreteria telefonica ospitata in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Abilitare gli utenti per la segreteria telefonica ospitata.</p></td>
<td><ul>
<li><p>Configurare gli account utente per gli utenti di cassette postali che si trovano in un servizio di Exchange ospitato.</p></li>
</ul></td>
<td><p>RTCUniversalUserAdmins</p></td>
<td><p><a href="lync-server-2013-enable-users-for-hosted-voice-mail.md">Abilitare gli utenti per la segreteria telefonica ospitata in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare gli oggetti contatto ospitati.</p></td>
<td><ol>
<li><p>Creare oggetti contatto Operatore automatico per la messaggistica unificata di Exchange ospitata.</p></li>
<li><p>Creare oggetti contatti Accesso sottoscrittore per la messaggistica unificata di Exchange ospitata.</p></li>
</ol></td>
<td><p>RTCUniversalUserAdmins</p>

> [!NOTE]
> Per creare, modificare o rimuovere oggetti contatto, l'utente che esegue il cmdlet New-CsExUmContact, Set-CsExUmContact o Remove-CsExUmContact deve disporre della corretta autorizzazione per l'unità organizzativa di Active Directory in cui sono archiviati i nuovi oggetti contatto. Questa autorizzazione può essere concessa eseguendo il cmdlet Grant-CsOUPermission. Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell.


</td>
<td><p><a href="lync-server-2013-create-contact-objects-for-hosted-exchange-um.md">Creare oggetti contatto per la messaggistica unificata di Exchange ospitata in Lync Server 2013</a></p></td>
</tr>
</tbody>
</table>

