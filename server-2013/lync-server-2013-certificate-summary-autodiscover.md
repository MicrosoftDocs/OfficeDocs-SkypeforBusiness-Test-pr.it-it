---
title: Riepilogo certificato - Individuazione automatica
TOCTitle: Riepilogo certificato - Individuazione automatica
ms:assetid: 16ac96bb-882a-4141-b75c-9530637548d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945616(v=OCS.15)
ms:contentKeyID: 52062098
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo certificato - Individuazione automatica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il servizio di individuazione automatica di Lync Server 2013 viene eseguito nei server dei pool di server Director e Front End e, se pubblicato in DNS, può essere utilizzato dai client Lync per individuare i servizi utente e server. Se si sta eseguendo l'aggiornamento da Lync Server 2010 e non è stato distribuito il servizio Mobility, prima che i client possano utilizzare l'individuazione automatica, è necessario modificare gli elenchi dei nomi alternativi del soggetto dei certificati in tutti i Server Director e Front End Server che eseguono tale servizio. Potrebbe inoltre essere necessario modificare gli elenchi dei nomi alternativi soggetto dei certificati utilizzati per le regole di pubblicazione dei servizi Web esterni nei proxy inversi.

La decisione relativa all'utilizzo degli elenchi dei nomi alternativi soggetto nei proxy inversi dipende dalla pubblicazione del servizio di individuazione automatica sulla porta 80 o sulla porta 443:

  - **Pubblicato sulla porta 80**   Non sono necessarie modifiche relative ai certificati se la query iniziale inviata al servizio di individuazione automatica avviene sulla porta 80. Questo è dovuto al fatto che i dispositivi mobili che eseguono Lync accederanno al proxy inverso sulla porta 80 esternamente e quindi verranno reindirizzati a un Server Director o Front End Server sulla porta 8080 internamente. Per informazioni dettagliate, vedere la sezione "Processo di individuazione automatica iniziale tramite la porta 80" [Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md).

  - **Pubblicato sulla porta 443**   L'elenco dei nomi alternativi soggetto nei certificati utilizzati dalla regola di pubblicazione dei servizi Web esterni deve contenere una voce *lyncdiscover.\<dominiosip\>* per ogni dominio SIP all'interno dell'organizzazione.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>È consigliabile utilizzare HTTPS anziché HTTP. HTTPS utilizza i certificati per crittografare il traffico. HTTP non fornisce la crittografia e i dati verranno inviati in formato di testo normale.</td>
    </tr>
    </tbody>
    </table>


La riemissione dei certificati tramite un'autorità di certificazione interna in genere è un processo semplice, ma per i certificati pubblici utilizzati nella regola di pubblicazione dei servizi Web l'aggiunta di più voci dei nomi alternativi soggetto può diventare un'attività dispendiosa. Per ovviare al problema, viene fornito il supporto per la connessione di individuazione automatica iniziale sulla porta 80, con conseguente reindirizzamento alla porta 8080 del pool di server Server Director o Front End Server.


> [!NOTE]
> Se nell'infrastruttura di Lync Server 2013 vengono utilizzati certificati interni rilasciati da un'autorità di certificazione interna e si prevede di supportare la connessione wireless per i dispositivi mobili, la catena di certificati radice dall'autorità di certificazione interna deve essere installata nei dispositivi mobili oppure è necessario passare a un certificato pubblico nell'infrastruttura di Lync Server 2013.



In questo argomento vengono descritti i nomi alternativi soggetto necessari per il pool di server Server Director, il Front End Server e il proxy inverso. Viene fatto riferimento solo ai nomi alternativi soggetto (SAN) aggiunti. Fare riferimento alle sezioni sulla pianificazione per informazioni sulle altre voci nei certificati. Per informazioni dettagliate, vedere [Scenari per il server Director in Lync Server 2013](lync-server-2013-scenarios-for-the-director.md), [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md) e [Scenari per i proxy inversi in Lync Server 2013](lync-server-2013-scenarios-for-reverse-proxy.md).

Nelle tabelle seguenti vengono definite le voci SAN di individuazione automatica per il pool di server Director, il pool Front End e il proxy inverso:

### Requisiti relativi ai certificati per il pool di server Director

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Voce nome alternativo soggetto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>URL servizio di individuazione automatica interno</p></td>
<td><p>SAN=lyncdiscoverinternal.<em>&lt;nome dominio interno&gt;</em></p></td>
</tr>
<tr class="even">
<td><p>URL servizio di individuazione automatica esterno</p></td>
<td><p>SAN=lyncdiscover.<em>&lt;dominiosip&gt;</em></p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Questo certificato aggiornato con la nuova voce SAN viene assegnato al certificato predefinito. In alternativa, è possibile utilizzare SAN=*.<EM>&lt;dominiosip&gt;</EM>.



### Requisiti relativi ai certificati per il pool Front End

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Voce nome alternativo soggetto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>URL servizio di individuazione automatica interno</p></td>
<td><p>SAN=lyncdiscoverinternal.<em>&lt;nome dominio interno&gt;</em></p></td>
</tr>
<tr class="even">
<td><p>URL servizio di individuazione automatica esterno</p></td>
<td><p>SAN=lyncdiscover.<em>&lt;dominiosip&gt;</em></p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Questo certificato aggiornato con la nuova voce SAN viene assegnato al certificato predefinito. In alternativa, è possibile utilizzare SAN=*.<EM>&lt;dominiosip&gt;</EM>



### Requisiti relativi ai certificati del proxy inverso (CA pubblica)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Voce nome alternativo soggetto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>URL servizio di individuazione automatica esterno</p></td>
<td><p>SAN=lyncdiscover.<em>&lt;dominiosip&gt;</em></p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Questo certificato aggiornato con la nuova voce SAN viene assegnato al listener SSL nel proxy inverso.


