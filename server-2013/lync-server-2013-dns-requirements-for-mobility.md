---
title: Requisiti di DNS per dispositivi mobili
TOCTitle: Requisiti di DNS per dispositivi mobili
ms:assetid: df6962bc-2a16-440e-a333-022ebd14f957
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690040(v=OCS.15)
ms:contentKeyID: 49302203
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di DNS per dispositivi mobili

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Se si distribuisce il servizio per dispositivi mobili Lync Server 2013, è possibile utilizzare i nuovi URL disponibili con il servizio di individuazione automatica di Microsoft Lync Server 2013 oppure gli URL dei servizi Web esistenti. Se si utilizzano gli URL esistenti, gli utenti devono immetterli manualmente nelle impostazioni dei loro dispositivi mobili. Questa opzione viene solitamente utilizzata per la risoluzione dei problemi. Se si utilizzano i nuovi URL i client mobili sono in grado di individuare automaticamente le risorse di Lync Server 2013. Se si supporta l'individuazione automatica, è necessario aggiungere nuovi record DNS (Domain Name System). In questa sezione vengono descritti i record DNS necessari per l'individuazione automatica.

Per supportare l'individuazione automatica, è necessario creare i record DNS seguenti per ogni dominio SIP:

  - Un record DNS interno per supportare gli utenti di dispositivi mobili che si connettono dall'interno della rete dell'organizzazione

  - Un record esterno, o pubblico, per supportare gli utenti di dispositivi mobili che si connettono da Internet

L'URL interno di individuazione automatica interna non deve essere indirizzabile dall'esterno della rete. L'URL esterno di individuazione automatica non deve essere indirizzabile dall'interno della rete. Se tuttavia non è possibile soddisfare questo requisito per l'URL esterno, la funzionalità dei client mobili non verrà influenzata.

I record DNS possono essere di tipo CNAME o A (host).

**Record DNS interni**

È necessario creare uno dei record DNS interni seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di record</th>
<th>Nome host o definizione SRV</th>
<th>Viene risolto in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>lyncdiscoverinternal.<em>&lt;dominiosip&gt;</em></p></td>
<td><p>Nome di dominio completo (FQDN) dei servizi Web interni per il pool di server Director, se disponibile, oppure per il pool Front End se non si dispone di un Server Director</p></td>
</tr>
<tr class="even">
<td><p>A (host)</p></td>
<td><p>lyncdiscoverinternal.<em>&lt;dominiosip&gt;</em></p></td>
<td><p>Indirizzo IP dei servizi Web interni (IP virtuale, o VIP, se si utilizza il bilanciamento del carico) del pool di server Director, se disponibile oppure del pool Front End se non si dispone di un Server Director</p></td>
</tr>
</tbody>
</table>


**Record DNS esterni**

È necessario creare uno dei record DNS esterni seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di record</th>
<th>Nome host</th>
<th>Viene risolto in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>lyncdiscover. <em>&lt;dominiosip&gt;</em></p></td>
<td><p>FQDN dei servizi Web esterni per il pool di server Director, se disponibile, oppure del pool Front End se non si dispone di un Server Director</p></td>
</tr>
<tr class="even">
<td><p>A (host)</p></td>
<td><p>lyncdiscover. <em>&lt;dominiosip&gt;</em></p></td>
<td><p>Indirizzo IP esterno o pubblico (indirizzo VIP se si utilizza il bilanciamento del carico) del proxy inverso</p></td>
</tr>
<tr class="odd">
<td><p>SRV</p></td>
<td><p>_sipfederationtls._tcp. <em>&lt;dominiosip&gt;</em></p>
<p>Viene risolto in un record host (A o AAAA) per il servizio Access Edge</p></td>
<td><p>Per supportare servizio notifica Push e servizio notifica Push Apple, è necessario creare un record SRV per ogni dominio SIP con client Microsoft Lync Mobile.</p>
<div class="alert">

> [!IMPORTANT]
> Questo requisito è valido solo per i client Microsoft Lync Mobile in dispositivi mobili Apple o Microsoft. I dispositivi Android e Nokia Symbian non utilizzano le notifiche push.

</div></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Il traffico di Lyncdiscover, denominato anche individuazione automatica, passa attraverso il proxy inverso. Il record SRV fa riferimento a un record che viene risolto tramite il servizio Access Edge.


