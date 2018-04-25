---
title: 'Lync Server 2013: Pianificare i certificati dei server perimetrali'
TOCTitle: Pianificare i certificati dei server perimetrali
ms:assetid: f1dfe220-2398-4ac8-ba4c-206c8c0cbc50
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413010(v=OCS.15)
ms:contentKeyID: 49302432
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificare i certificati dei server perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-05_

La creazione di certificati per i server perimetrali è semplificata in Lync Server 2013.

**Diagramma di flusso Certificati per Edge Server**

![Diagramma di flusso per i certificati](images/Gg413010.a5fc20db-7ced-4364-b577-6a709a8367cd(OCS.15).jpg "Diagramma di flusso per i certificati")

Creare un singolo certificato pubblico, verificare di disporre di una chiave privata esportabile definita per il certificato e assegnarlo alle interfacce esterne dei server perimetrali seguenti utilizzando la Configurazione guidata certificati:

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>I certificati con caratteri jolly non sono supportati in Lync Server, ad eccezione di quando sono utilizzati per riepilogare gli URL semplici tramite il proxy inverso. È necessario definire nomi soggetto alternativi (SAN, Subject Alternate Name) distinti per ogni nome di dominio SIP, servizio Web Conferencing Edge, servizio A/V Edge e dominio XMPP offerto dalla distribuzione.</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Introdotta in Lync Server 2013, la gestione temporanea dei certificati di autenticazione audio/video prima della data di scadenza del certificato corrente richiede una pianificazione aggiuntiva. Anziché un certificato con più scopi per l'interfaccia esterna perimetrale, saranno necessari due certificati, uno assegnato al servizio Access Edge e al servizio Web Conferencing Edge e uno per il servizio A/V Edge. Per ulteriori informazioni, vedere <A href="lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-set-cscertificate.md">Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013</A>



<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nel caso di un pool di server perimetrali, esportare il certificato con la chiave privata in ciascun server perimetrale e assegnare il certificato a ciascun servizio del server perimetrale. Eseguire la stessa operazione per il certificato interno del server perimetrale, esportando il certificato con la chiave privata e assegnandolo a ciascuna interfaccia interna perimetrale.</td>
</tr>
</tbody>
</table>


  - Verificare di disporre di una chiave privata esportabile assegnata per il certificato

  - servizio Access Edge (denominato **Access Edge Server SIP esterno** nella Configurazione guidata certificati)

  - servizio Web Conferencing Edge (denominato **Web Conferencing Edge Server esterno** nella Configurazione guidata certificati)

  - Servizio di autenticazione A/V (denominato **A/V Edge Server esterno** nella Configurazione guidata certificati)

Creare un singolo certificato interno con chiave privata esportabile, copiarlo e assegnarlo a ciascuna delle interfacce interne del server perimetrale:

  - Server perimetrale (denominato **Edge Server interno** nella Configurazione guidata certificati)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È possibile utilizzare certificati separati e distinti per ciascun servizio del server perimetrale. Scegliere di separare i certificati se si desidera utilizzare la nuova funzionalità di certificati in sequenza per il certificato servizio A/V Edge. In tal caso, è consigliabile separare il certificato servizio A/V Edge dal servizio Access Edge e dal servizio Web Conferencing Edge. Se si sceglie di richiedere, acquisire e assegnare certificati separati per ciascun servizio, è necessario che la chiave privata sia esportabile per il servizio A/V Edge (anche in questo caso, si tratta del servizio di autenticazione A/V) e assegnare lo stesso certificato all'interfaccia esterna perimetrale A/V in ciascun server perimetrale.</td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013](lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-set-cscertificate.md)  

#### Concetti

[Modifiche introdotte in Lync Server 2013 che incidono sulla pianificazione dei server perimetrali](lync-server-2013-changes-in-lync-server-that-affect-edge-server-planning.md)

