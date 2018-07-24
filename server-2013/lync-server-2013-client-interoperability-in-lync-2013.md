---
title: 'Lync Server 2013: Interoperabilità dei client in Lync 2013'
TOCTitle: Interoperabilità dei client in Lync 2013
ms:assetid: 0f126571-91a2-45d5-855c-1e4ddb45fc04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204672(v=OCS.15)
ms:contentKeyID: 49299689
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Interoperabilità dei client in Lync 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento viene illustrata la capacità dei client Microsoft Lync Server 2013 di coesistere e interagire con client di versioni precedenti di Lync Server e Office Communications Server.

## Compatibilità di server e client

Nella tabella seguente sono mostrate le combinazioni supportate di versioni client e server. Viene indicato se è supportato l'accesso quando il client tenta di connettersi al server indicato. Lync Server 2013 supporta le versioni client precedenti. Inoltre, a differenza delle versioni precedenti, Lync Server 2010 supporta i nuovi client Lync 2013. Questo consente alle organizzazioni che eseguono l'aggiornamento da Lync Server 2010 di implementare nuovi client indipendentemente dagli aggiornamenti di Lync Server.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Lync Server 2013</th>
<th>Lync Server 2010</th>
<th>Office Communications Server 2007 R2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato5</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 di base</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Lync Web App 2013</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 Attendant</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010, Group Chat</p></td>
<td><p>Supportato1</p></td>
<td><p>Supportato2</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Lync Web App 2010</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 Attendee</p></td>
<td><p>Non supportato3</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>Interoperativo4</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Office Communications Server 2007 R2 Attendant</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="even">
<td><p>Office Live Meeting 2007</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="odd">
<td><p>app Windows Store Lync</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
</tbody>
</table>


1Per informazioni dettagliate, vedere [Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md).

2In Microsoft Lync Server 2010 la funzionalità Group Chat è disponibile con Group Chat Server, un'applicazione attendibile di terze parti per Lync Server 2010. I client di Lync 2013 non sono compatibili con Lync Server 2010, Group Chat.

3Lync Web App 2013 offre ora funzionalità complete di partecipazione alle riunioni, inclusi audio e video e video del computer e può sostituire Lync 2010 Attendee. Lync 2010 Attendee si connetterà a Lync Server 2013 solo quando si usa un browser non supportato (Internet Explorer 6 o Internet Explorer 7) e Windows XP.

4Le funzionalità di presenza e messaggistica istantanea di Office Communicator 2007 R2 sono compatibili con Lync Server 2013, mentre le funzionalità di conferenza non lo sono. Durante la migrazione da Office Communications Server 2007 R2, Office Communicator 2007 R2 è utile per l'interoperabilità di presenza e messaggistica istantanea, ma gli utenti devono utilizzare Lync Web App 2013 per partecipare alle riunioni Lync Server 2013.

5 Per le limitazioni vedere "Supporto della funzionalità di conferenza per client Lync 2013 in riunioni di Lync Server 2010" più avanti in questo argomento.

## Interoperabilità tra client

Con la versione Lync Server 2013, le varie versioni client possono interagire facilmente in scenari peer-to-peer e di conferenza. In questa sezione vengono illustrate le funzionalità disponibili quando gli utenti interagiscono con altri utenti che utilizzano versioni diverse dei client e server.

## Supporto della funzionalità peer-to-peer

Le funzionalità peer-to-peer sono supportate per gli utenti ospitati su diverse versioni del server e che utilizzano diverse versioni client. L'esperienza dell'utente finale e le caratteristiche disponibili sono in linea con le funzionalità del client dell'utente e con la versione del server a cui l'utente ha eseguito l'accesso. In altri termini:

  - Se un utente ha eseguito l'accesso a Lync Server 2013 con un client precedente, l'esperienza sarà uguale a quella consueta. Nessuna delle nuove caratteristiche introdotte in Lync Server 2013 sarà disponibile fino a quando il client dell'utente non verrà aggiornato. Alcuni esempi includono la visualizzazione Raccolta video, i video HD, la condivisione PowerPoint e l'opzione per disattivare l'audio e il video di tutti i partecipanti al momento dell'accesso alla riunione. Le nuove funzionalità sono illustrate in [Nuove funzionalità di conferenza in Lync Server 2013](lync-server-2013-new-conferencing-features.md) e [Novità per i client in Lync Server 2013](lync-server-2013-what-s-new-for-clients.md).

  - Se un utente ha eseguito l'accesso a Lync Server 2010 con un client Lync 2013, le nuove caratteristiche non supportate da Lync Server 2010 non saranno disponibili fino a quando l'utente non verrà spostato in Lync Server 2013.

Nella tabella seguente vengono confrontate le caratteristiche disponibili nelle sessioni peer-to-peer in cui il client ha eseguito l'accesso a Lync Server 2013 o Lync Server 2010.


> [!NOTE]
> Lync Web App e Lync 2010 Attendee sono client specifici per riunioni e non sono inclusi in questa tabella.




<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Messaggistica istantanea</th>
<th>Presenza</th>
<th>Voce</th>
<th>Video</th>
<th>Condivisione applicazioni</th>
<th>Trasferimento di file</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 di base</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 Attendant</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 Mobile</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Lync Phone Edition</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì1</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Messaggistica istantanea pubblica (AOL, Yahoo!)</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Messaggistica istantanea pubblica (MSN, Windows Live Messenger)</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


> [!important]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (PIC USL) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La possibilità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante non verrà rinnovato.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti in tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Lync Standard. La federazione con Skype verrà aggiunta a questo elenco per consentire agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


1 In Office Communicator 2007 R2 è disponibile solo la condivisione desktop, ma non dei programmi.

## Supporto della funzionalità di conferenza per client Lync 2013 in riunioni di Lync Server 2010

Quando gli utenti partecipano a riunioni di Lync Server 2010 con un client Lync 2013, hanno accesso alle funzionalità client di Lync 2013 con le seguenti eccezioni:

  - Nelle opzioni di gestione **Participanti**, accessibili tramite l'icona Persone nella finestra della riunione, l'opzione **Messaggistica istantanea della riunione non disponibile** non funziona.

  - La Visualizzazione Raccolta non funziona nelle conferenze video. L'utente vede solo l'interlocutore attivo, anziché tutti gli interlocutori. Nell'elenco delle opzioni **Scegliere un Layout** l'opzione **Visualizzazione Raccolta** non è disponibile.

  - Per impostazione predefinita, nelle conferenze video viene visualizzato l'elenco dei participanti.

  - Quando si fa clic con il pulsante destro del mouse su un utente nell'elenco dei partecipanti, le opzioni di gestione dei partecipanti **Blocca l'evidenza video** e **Aggiungi alla raccolta** non sono disponibili.

## Supporto delle funzionalità di conferenza in riunioni di Lync Server 2013

Lync Server 2013 include nuove funzionalità di conferenza che diventano disponibili quando gli utenti spostano i propri account in Lync Server 2013 ed eseguono l'accesso con il client di Lync 2013. Alcuni esempi includono la visualizzazione Raccolta video, i video HD, la condivisione PowerPoint e l'opzione per disattivare l'audio e il video di tutti i partecipanti al momento dell'accesso alla riunione. Le nuove funzionalità sono illustrate in [Nuove funzionalità di conferenza in Lync Server 2013](lync-server-2013-new-conferencing-features.md) e [Novità per i client in Lync Server 2013](lync-server-2013-what-s-new-for-clients.md).

Nelle riunioni di Lync Server 2013 alcune funzionalità di conferenza sono supportate per gli utenti ospitati su diverse versioni del server e che utilizzano client e versioni client diverse. Quando i client partecipano a una riunione di Lync Server 2013, gli utenti hanno accesso alle caratteristiche e funzionalità mostrate in questa tabella.


<table style="width:100%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Messaggistica istantanea peer-to-peer</th>
<th>Voce</th>
<th>Video</th>
<th>Condivisione applicazioni</th>
<th>PowerPoint</th>
<th>Trasferimento di file</th>
<th>Lavagna</th>
<th>Polling</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 di base</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Lync Web App</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì2</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì3</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R24</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 In Office Communicator 2007 R2 è disponibile solo la condivisione desktop, ma non dei programmi.

2Lync Server 2013 utilizza un meccanismo aggiornato per il caricamento dei file di PowerPoint. Gli utenti di Lync Web App che partecipano a una riunione originariamente pianificata su Lync Server 2010 possono visualizzare e scorrere le presentazioni di PowerPoint, ma non caricare file di PowerPoint.

3 Se la riunione è stata pianificata in Lync Server 2013 e le diapositive di PowerPoint sono state caricate da un client Lync 2013, gli utenti di Lync 2010 possono accedere alla diapositive in sola visualizzazione. Al contrario, se le diapositive di PowerPoint sono state caricate da un utente di Lync 2010, gli utenti di Lync Server 2013 saranno in grado di visualizzare le diapositive e, se il server Office Web Apps è configurato, di accedere alle nuove funzionalità, ad esempio schermo, animazioni, transizioni di diapositive e video incorporati con risoluzione superiore. Per ulteriori informazioni, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

4Le funzionalità di presenza e messaggistica istantanea di Office Communicator 2007 R2 sono compatibili con Lync Server 2013, mentre le funzionalità di conferenza non lo sono. Durante la migrazione da Office Communications Server 2007 R2, Office Communicator 2007 R2 è utile per l'interoperabilità di presenza e messaggistica istantanea, ma gli utenti devono utilizzare Lync Web App 2013 per partecipare alle riunioni Lync Server 2013.

## Supporto dei componenti aggiuntivi di pianificazione

Il supporto server per i vari componenti aggiuntivi di pianificazione è coerente con la compatibilità tra le versioni server e client. In generale, in Lync Server 2013 sono supportati i seguenti componenti aggiuntivi di pianificazione. Le versioni precedenti dei componenti aggiuntivi, tuttavia, non forniscono le nuove funzionalità dei componenti aggiuntivi di Lync 2013, ad esempio la possibilità di disattivare l'audio e il video di tutti i partecipanti al momento dell'accesso alla riunione.

  - **componente aggiuntivo per riunioni online per Lync 2013**   Fornisce le stesse funzionalità del Componente aggiuntivo per riunioni online per Lync 2010, con l'aggiunta di controlli per la disattivazione dell'audio dei partecipanti. Questo consente agli organizzatori delle riunioni di pianificare conferenze in cui l'audio e il video dei partecipanti sono disattivati per impostazione predefinita. Gli amministratori possono anche personalizzare le convocazioni di riunioni dell'organizzazione aggiungendo un logo personalizzato, un URL di supporto, l'URL di una dichiarazione di non responsabilità legale o un testo a piè di pagina personalizzato.

  - **Componente aggiuntivo per riunioni online per Lync 2010**   Fornisce la pianificazione per le riunioni di Lync e rimuove la possibilità di pianificare conferenze di Office Live Meeting.

  - **Componente aggiuntivo per conferenze per Communicator 2007 R2**   Fornisce la pianificazione per le conferenze di Office Live Meeting e di Office Communicator 2007 R2. 


> [!NOTE]
> Le conferenze di Live Meeting non possono essere pianificate in Lync Server 2013.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client di pianificazione</th>
<th>Lync Server 2013</th>
<th>Lync Server 2010</th>
<th>Office Communications Server 2007 R2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>componente aggiuntivo per riunioni online per Lync 2013 (può essere utilizzato con Office 2013, Outlook 2010 e Outlook 2007)</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato (nuove caratteristiche dei componenti aggiuntivi non disponibili)</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Utilità di pianificazione Web di Lync 2013</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Componente aggiuntivo per riunioni online per Lync 2010</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Componente aggiuntivo per conferenze per Office Communicator 2007 R2</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
</tbody>
</table>


## Supporto della partecipazione a riunioni

Tutti i client supportati da Lync Server 2013 possono partecipare alle riunioni di Lync 2013. Dato che Lync Web App è un componente Web del server, nei casi in cui viene utilizzato Lync Web App per partecipare a una riunione di Lync Server 2013, viene sempre utilizzata la versione più recente di Lync Web App.

I client Lync 2013 possono partecipare alle riunioni ospitate su Lync 2010 e Office Communications Server 2007 R2 con funzionalità ridotte. Le funzionalità per le riunioni sono limitate dalla versione del server in cui è ospitata la riunione.

## Vedere anche

#### Concetti

[Requisiti dell'app Lync di Windows Store](lync-server-2013-lync-windows-store-app-requirements.md)  
[Nuove funzionalità di conferenza in Lync Server 2013](lync-server-2013-new-conferencing-features.md)  
[Novità per i client in Lync Server 2013](lync-server-2013-what-s-new-for-clients.md)

