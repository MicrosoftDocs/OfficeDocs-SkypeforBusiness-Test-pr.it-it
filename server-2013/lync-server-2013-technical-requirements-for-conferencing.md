---
title: 'Lync Server 2013: Requisiti tecnici per le conferenze'
TOCTitle: Requisiti tecnici per le conferenze
ms:assetid: 3c0d89e1-53e6-46d7-bf8c-491260b292ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425889(v=OCS.15)
ms:contentKeyID: 49300269
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per le conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per Lync Server 2013 le funzionalità di conferenza telefonica con accesso esterno, A/V Conferencing, conferenza di messaggistica istantanea e Web Conferencing vengono eseguite sempre nei Front End Server.

In questa sezione vengono fornite informazioni dettagliate sui requisiti hardware e software per questi server, insieme alla collocazione supportata.

La funzionalità di conferenza telefonica con accesso esterno include una vasta gamma di componenti, alcuni dei quali sono specifici delle conferenze telefoniche con accesso esterno, mentre altri sono componenti di VoIP aziendale. In questa sezione vengono descritti i requisiti per i componenti specifici delle conferenze telefoniche con accesso esterno. Per informazioni dettagliate sui requisiti di Mediation Server e dei gateway PSTN (Public Switched Telephone Network), vedere [Componente Mediation Server in Lync Server 2013](lync-server-2013-mediation-server-component.md) e [Componenti e topologie per Mediation Server in Lync Server 2013](lync-server-2013-components-and-topologies-for-mediation-server.md) nella documentazione relativa alla pianificazione.

## Requisiti hardware

Poiché le funzionalità Web Conferencing e A/V Conferencing sono incluse nel Front End Server, i requisiti hardware per il server sono gli stessi dei Front End Server. Per informazioni dettagliate sui requisiti hardware, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa alla supportabilità. Anche i requisiti dei componenti seguenti, richiesti per la funzionalità di conferenza telefonica con accesso esterno, sono gli stessi del Front End Server:

  - Servizio applicazione

  - applicazione Operatore Conferenza

  - applicazione Annuncio conferenza

I requisiti hardware per i Front End Server sono gli stessi di molti altri ruoli del server in Lync Server 2013, come descritto nella tabella seguente.

## Requisiti software

Poiché le funzionalità Web Conferencing e A/V Conferencing sono incluse nel Front End Server, i requisiti software per il server sono gli stessi dei Front End Server. Per informazioni dettagliate sui requisiti software, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa alla supportabilità.

Per la funzionalità Web Conferencing, Lync Server 2013 richiede inoltre Office Web Apps e Server Office Web Apps (precedentemente noto come WAC Server) per gestire le presentazioni PowerPoint. Per informazioni dettagliate, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

Per le funzionalità di conferenza telefonica con accesso esterno, i requisiti del sistema operativo Servizio applicazione, dell' applicazione Operatore Conferenza e dell' applicazione Annuncio conferenza sono gli stessi dei Front End Server. Per informazioni dettagliate sui requisiti software, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa alla supportabilità.

L' applicazione Operatore Conferenza e l' applicazione Annuncio conferenza richiedono l'installazione di Runtime formato Windows Media nei Front End Server. Runtime formato Windows Media è richiesto per la riproduzione dei file audio WMA (Windows Media Audio) usati per la musica in attesa, i nomi registrati e i messaggi. Ad eccezione di Windows Server 2012 e Windows Server 2012 R2, Runtime formato Windows Media viene installato automaticamente come parte dell'esperienza desktop di Windows quando si esegue il programma di installazione, tuttavia potrebbe essere necessario riavviare il computer. È consigliabile pertanto installare il componente come parte dell'esperienza desktop di Windows prima di eseguire il programma di installazione. Windows Server 2012 e Windows Server 2012 R2 richiedono Microsoft Media Foundation.

## Requisiti delle porte per le conferenze telefoniche con accesso esterno

Nella tabella seguente vengono descritte le porte usate per le conferenze telefoniche con accesso esterno. Se si usa un servizio di bilanciamento del carico, assicurarsi che sia configurato per le porte usate dalle applicazioni che verranno eseguite nel pool.

Queste porte sono impostazioni predefinite ed è possibile modificarle utilizzando il cmdlet **Set-CsApplicationServer**. Per informazioni dettagliate sul cmdlet, vedere la documentazione di Lync Server Management Shell.


> [!NOTE]
> Tutte le istanze della stessa applicazione in un pool usano la stessa porta di attesa SIP.



### Porte usate dalle conferenze telefoniche con accesso esterno

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero di porta</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5072</p></td>
<td><p>Usata per le richieste di attesa SIP dell' applicazione Operatore Conferenza</p></td>
</tr>
<tr class="even">
<td><p>5073</p></td>
<td><p>Usata per le richieste di attesa SIP dell'applicazione Annuncio conferenza</p></td>
</tr>
</tbody>
</table>


## Client supportati per le conferenze telefoniche con accesso esterno

È possibile usare il client seguente per pianificare conferenze locali che supportino la conferenza telefonica con accesso esterno:

  - componente aggiuntivo per riunioni online per Lync 2013 (installato automaticamente con l'installazione di Lync 2013 o Attendee)

## Requisiti della pagina Impostazioni conferenza telefonica con accesso esterno

Lo pagina Impostazioni conferenza telefonica con accesso esterno supporta le combinazioni di sistemi operativi e Web browser descritte nella tabella seguente.


> [!NOTE]
> Sono supportate le versioni a 32 bit e a 64 bit dei sistemi operativi.



### Sistemi operativi e Web browser supportati

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema operativo</th>
<th>Web browser</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows 7</p></td>
<td><p>Internet Explorer 9</p>
<p>Internet Explorer 8</p>
<p>Firefox</p></td>
</tr>
<tr class="even">
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p></td>
<td><p>Internet Explorer 9</p>
<p>Internet Explorer 8</p>
<p>Internet Explorer 7</p></td>
</tr>
<tr class="odd">
<td><p>Sistema operativo Mac</p></td>
<td><p>Firefox</p>
<p>Safari</p></td>
</tr>
</tbody>
</table>


## Requisiti dei file audio per le conferenze telefoniche con accesso esterno

Lync Server 2013 non supporta la personalizzazione di messaggi vocali e musica per la conferenza telefonica con accesso esterno. Tuttavia, se vi è l'esigenza aziendale di modificare i file audio predefiniti, vedere l'articolo 961177 della Microsoft Knowledge Base, [Come personalizzare le istruzioni vocali o file di musica per conferenze audio con accesso esterno in Microsoft Office Communications Server 2007 R2](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=961177).

È anche possibile usare l'utilità per la gestione dei [messaggi vocali personalizzati di Operatore Conferenza Microsoft Lync Server](http://go.microsoft.com/fwlink/p/?linkid=396880), che consente agli amministratori di sostituire i messaggi vocali predefiniti usati quando un chiamante partecipa a una riunione Lync con messaggi personalizzati, per offrire un'esperienza diversa di ingresso alle riunioni. I messaggi vocali personalizzati possono essere installati in un server che esegue Lync Server 2010 o Lync Server 2013, sia Enterprise Edition che Standard Edition.

I requisiti dell' applicazione Operatore Conferenza e dell' applicazione Annuncio conferenza per la musica in attesa, il nome registrato e i file dei messaggi audio sono i seguenti:

  - Formato file WMA (Windows Media Audio)

  - Mono a 16 bit

  - CBR (Constant Bit Rate) a due passaggi 48 kbps

  - Livello parlato a -24 DB

## Requisiti utente per le conferenze telefoniche con accesso esterno

Gli utenti delle conferenze telefoniche con accesso esterno devono avere un numero di telefono univoco o un interno assegnato al loro account. Questo requisito supporta l'autenticazione durante l'accesso esterno. Gli utenti aziendali (ossia gli utenti che dispongono di credenziali Servizi di dominio Active Directory e di account Lync Server all'interno dell'organizzazione) immettono il numero di telefono (o interno) e un PIN (Personal Identification Number) per effettuare l'accesso esterno alle conferenze come utenti autenticati.

