---
title: Come vengono visualizzate le foto degli utenti in Lync
TOCTitle: Come vengono visualizzate le foto degli utenti in Lync
ms:assetid: b44a364d-a1d2-4d45-b27a-b5f77775e233
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn783119(v=OCS.15)
ms:contentKeyID: 62833685
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Come vengono visualizzate le foto degli utenti in Lync

 

_**Ultima modifica dell'argomento:** 2015-03-09_

**Riepilogo:** le foto degli utenti visualizzate nel client Lync possono essere diverse a seconda della funzionalità di Lync in uso, ad esempio durante una conferenza o una chat di messaggistica istantanea.

In Lync 2010 è stata introdotta la possibilità di includere una foto nel profilo Lync visualizzato agli altri utenti di Lync. È anche possibile scegliere se visualizzare o meno le foto dei contatti nel client Lync. In Lync 2013 è stato introdotto il supporto per le foto degli utenti ad alta risoluzione. In questo argomento vengono descritti in che modo il client Lync recupera e visualizza le foto degli utenti, la posizione di archiviazione delle immagini, le limitazioni per ogni origine di immagini e come vengono usate le foto degli utenti dai diversi servizi di Lync.

## Considerazioni di pianificazione

È necessario tenere presente quanto segue se si prevede di implementare il supporto per le foto degli utenti.

  - Il supporto per le foto degli utenti ad alta definizione richiede che la cassetta postale dell'utente sia basata su Exchange 2013 e che l'account utente di Lync sia nel pool di Lync 2013.

  - Le foto degli utenti ad alta definizione sono supportate solo in un ambiente in cui vengono usati sia Lync Server 2013 che Exchange 2013.

  - Per gli utenti con cassette postali in Exchange 2010 verrà sempre usato l'attributo **thumbnailPhoto** di Servizi di dominio Active Directory come origine per le relative foto.

  - Una foto dell'utente archiviata come attributo **thumbnailPhoto** di Servizi di dominio Active Directory non verrà visualizzata ai contatti esterni o federati.

  - Se le foto per i contatti degli utenti sono archiviate in Servizi di dominio Active Directory, il limite per il file di immagine è di 96 per 96 pixel e la dimensione massima è di 100 KB.

  - Se la connettività tra Lync Server ed Exchange Server viene persa, verrà visualizzata la foto dell'utente **thumbnailPhoto** a bassa definizione da Servizi di dominio Active Directory e solo per gli utenti interni.

  - Le foto degli utenti ad alta risoluzione sono visualizzate nelle riunioni di Lync 2013 quando non è abilitato il video per un interlocutore attivo. Inoltre, spostando il puntatore del mouse sulla foto di anteprima nella raccolta, verrà visualizzata la foto ad alta risoluzione.

## Foto degli utenti in Lync 2010

Nel client Lync 2010 è possibile scegliere tra due opzioni per la visualizzazione di una foto per il proprio profilo, **Immagine aziendale predefinita** e **Mostra l'immagine da un indirizzo Web**.

## Immagine aziendale predefinita

Quando si sceglie l'opzione **Immagine aziendale predefinita**, Lync recupera la foto visualizzata da Servizi di dominio Active Directory. L'immagine usata è l'immagine definita come valore per l'attributo **thumbnailPhoto** in Servizi di dominio Active Directory. Si tratta dello stesso file usato da Exchange per visualizzare le immagini in Outlook.

Le considerazioni per l'uso di immagini da Servizi di dominio Active Directory includono quanto segue:

  - Sono supportate solo immagini con dimensioni fino a 96 per 96 pixel. Il limite per la dimensione del file di immagine è di 100 KB.

  - Per impostazione predefinita, gli utenti possono modificare l'immagine usata per l'attributo **thumbnailPhoto**, anche se non direttamente tramite il client Lync. È possibile disabilitare questa impostazione mediante Servizi di dominio Active Directory.

  - Le immagini archiviate in Servizi di dominio Active Directory non vengono visualizzate ai contatti esterni all'organizzazione, anche se sono contatti federati.

  - Nelle organizzazioni di grandi dimensioni, l'archiviazione e il recupero delle immagini per numerosi utenti può influire sulla dimensione e sulle prestazioni del database di Servizi di dominio Active Directory.

  - Le dimensioni limitate dell'immagine e del file implicano che è possibile usare solo immagini a bassa risoluzione.

## Modalità di gestione delle foto da parte degli utenti in Servizi di dominio Active Directory

Un utente non può modificare l'immagine usata nel proprio profilo di Servizi di dominio Active Directory direttamente tramite il client Lync 2010. A tale scopo, è possibile usare una delle seguenti opzioni, se disponibili:

  - **SharePoint Server**   Gli utenti possono caricare una foto in "Sito personale" in un sistema SharePoint Server e quindi [configurare la sincronizzazione del profilo in SharePoint](http://go.microsoft.com/fwlink/p/?linkid=507466) per sincronizzare la foto nell'attributo **thumbnailPhoto** in Servizi di dominio Active Directory.

  - **Foto archiviata in un URL accessibile pubblicamente**   Gli utenti possono configurare la propria foto specificando un URL accessibile pubblicamente per l'immagine che vogliono usare. L'immagine deve essere accessibile pubblicamente senza una password. L'immagine archiviata all'indirizzo Web specificato viene trasferita agli altri utenti tramite la categoria della scheda contatto nelle informazioni sulla presenza. Quando il client Lync deve visualizzare una foto dell'utente, recupera l'immagine dall'indirizzo Web specificato.

  - **Cmdlet di Exchange 2010 per Windows PowerShell**   Gli amministratori possono eseguire il cmdlet [Import-RecipientDataProperty](http://go.microsoft.com/fwlink/p/?linkid=507468) in Exchange 2010 Management Shell per gestire l'attributo **thumbnailPhoto**. Quando le immagini vengono importate con i cmdlet di Exchange 2010, il limite per la dimensione del file è di 10 KB.

  - **Strumenti di terze parti**   Gli utenti possono caricare solo la propria foto per l'attributo **thumbnailPhoto**.

## Mostra l'immagine da un indirizzo Web

Quando si sceglie l'opzione **Mostra l'immagine da un indirizzo Web**, Lync recupera l'immagine all'indirizzo specificato e la visualizza come foto dell'utente in Lync.

Le considerazioni per l'uso di immagini da un indirizzo Web includono quanto segue:

  - I limiti per la dimensione del file sono determinati dall'attributo **MaxPhotoSizeKB** nei criteri client, definiti con il cmdlet [New-CsClientPolicy](http://go.microsoft.com/fwlink/p/?linkid=507463). Il limite predefinito per la dimensione è di 30 KB. Il valore massimo è di 100 KB. Non sono previste limitazioni per la risoluzione dell'immagine, ma se si tenta di usare un file di immagine superiore al limite di dimensione, il file non verrà scaricato nei client Lync. È possibile impostare il valore su 0 per disabilitare l'uso di tutte le foto degli utenti in Lync.

  - Le foto degli utenti da un indirizzo Web possono essere visualizzate dai contatti federati esterni.

## Gestione delle foto degli utenti con i cmdlet dei criteri client

In Lync Server 2010 le impostazioni dei criteri client sono configurate con i cmdlet CsClientPolicy. Le impostazioni dei criteri configurate vengono inviate ai client tramite il provisioning di tipo in-band. I due parametri dei cmdlet CsClientPolicy che determinano l'esperienza relativa alle foto degli utenti sono **DisplayPhoto** e **MaxPhotoSizeKB**. Il parametro corrispondente del provisioning in-band per **DisplayPhoto** e **MaxPhotoSizeKB** è denominato **PhotoUsage**. I valori per il parametro **PhotoUsage** vengono inviati ai client tramite il **provisionGroupendpointConfiguration**. Per ulteriori informazioni, vedere [Panoramica di criteri e impostazioni client](http://go.microsoft.com/fwlink/?linkid=507470).

Il valore del parametro **DisplayPhoto** determina l'origine dell'immagine per la foto dell'utente. I valori supportati sono inclusi nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore del parametro DisplayPhoto</th>
<th>Immagine di origine</th>
<th>Impostazioni del client Lync 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NoPhoto</p></td>
<td><p>nessuna</p></td>
<td><p><strong>Non mostrare l'immagine personale</strong></p></td>
</tr>
<tr class="even">
<td><p>PhotoFromADOnly</p></td>
<td><p>Active Directory</p></td>
<td><p><strong>Immagine aziendale predefinita</strong></p></td>
</tr>
<tr class="odd">
<td><p>AllPhotos</p></td>
<td><p>Indirizzo Web</p></td>
<td><p><strong>Mostra l'immagine da un indirizzo Web</strong></p></td>
</tr>
</tbody>
</table>


## Modalità di recupero delle foto da parte del client Lync 2010

In Lync 2010 le foto degli utenti sono gestite sul server tramite il servizio Rubrica. Il client Lync recupera le foto degli utenti innanzitutto interrogando il servizio query Web della Rubrica (ABWQ) sul server, esposto tramite il servizio Web di espansione liste distribuzione. Il client riceve il file di immagine e quindi lo copia nella cache dell'utente per evitare di scaricare l'immagine ogni volta che deve essere visualizzata. Anche i valori dell'attributo restituiti dalla query vengono archiviati nella voce del servizio Rubrica memorizzata nella cache per l'utente. Il servizio Rubrica elimina tutte le immagini memorizzate nella cache ogni 24 ore, pertanto possono occorrere fino a 24 ore perché le nuove immagini degli utenti vengano aggiornate nella cache sul server. È possibile forzare un aggiornamento della cache usando il cmdlet [Update-CsAddressBook](https://docs.microsoft.com/en-us/powershell/module/skype/Update-CsAddressBook).

Alle foto degli utenti incluse nello stato presenza è associato anche un valore hash usato dal client Lync per determinare se è disponibile un'immagine più recente. Al client vengono automaticamente notificate le modifiche apportate al file di immagine usato nello stato presenza.


> [!NOTE]
> Poiché le foto non sono archiviate nel database GalContacts.db, il download delle foto degli utenti non dipende dall'impostazione <STRONG>AddressBookAvailability</STRONG> nei criteri client (<A href="http://go.microsoft.com/fwlink/p/?linkid=507508">Set-CsClientPolicy</A>).



La query al servizio ABWQ include gli attributi seguenti:

  - **PhotoHash**   Il valore hash dei dati binari della foto, usato per determinare se la foto corrente è stata modificata.

  - **PhotoRelPath**   Il percorso relativo del file di immagine archiviato nel server.

  - **PhotoSize**   La dimensione del file di immagine, in byte.

  - **TimeStamp**   La data e l'ora in cui il file di immagine è stato scaricato dal server e copiato nella cache del client l'ultima volta.

Successivamente, dopo avere recuperato il file di immagine, il client Lync 2010 confronta i valori degli attributi restituiti dalla query con i valori degli attributi ricevuti dal client dal provisioning in-band per stabilire se sono diversi. Se i valori sono differenti, il client recupera il file di immagine dell'utente che ha eseguito l'accesso con una richiesta HTTP GET.

Inoltre, il client esegue una verifica con il server ogni 24 ore dal momento in cui è stata creata la versione memorizzata nella cache del file di immagine per confrontare il valore dell'attributo **PhotoHash** sul server con il valore nel client. Se i valori sono differenti, il client determina che il file di immagine è stato modificato. Per ottenere il file di immagine aggiornato, il client interroga nuovamente il servizio ABWQ per aggiornare il file di immagine nella cache del client con il file di immagine sul server. Tale operazione, inoltre, reimposta l'attributo **TimeStamp** del file nella cache del client.

Di seguito è riportata una risposta di esempio a una query al servizio ABWQ:

    <Attribute>
              <Name>PhotoRelPath</Name>
              <Value>efa6096aed2746cb9ab2037f7dbdde9d.f2eeeb5946db54a7aa607ecd3ae09d
              95.photo</Value>
              <Values xmlns:d6p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays" i:nil="true" />
    </Attribute>
    <Attribute>
              <Name>PhotoHash</Name>
              <Value>f2eeeb5946db54a7aa607ecd3ae09d95</Value>
              <Values xmlns:d6p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays" i:nil="true" />
    </Attribute>
    <Attribute>
         <Name>PhotoSize</Name>
         <Value>4620</Value>
         <Valuesxmlns:d6p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
    i:nil="true" />
    </Attribute>

## Foto degli utenti in Lync 2013

In Lync 2013 è stato introdotto il supporto per le immagini ad alta risoluzione per le foto degli utenti. Lync 2013 include anche il supporto per l'archiviazione delle foto degli utenti nella cassetta postale dell'utente in Exchange 2013, che rimuove le limitazioni per la risoluzione e la dimensione delle immagini presenti in Lync 2010. Le foto degli utenti in Lync 2013 possono essere fino a 648 per 648 pixel con una dimensione massima del file di 20 MB. Le foto ad alta risoluzione in Lync 2013 devono essere contenute nella cassetta postale dell'utente in Exchange 2013 e sono supportate solo con il client Lync 2013. Questa integrazione con Exchange trae vantaggio dal nuovo framework di autorizzazione incluso nelle versioni 2013 di Lync, Exchange e SharePoint denominato Oauth.

Se Exchange 2013 non è in uso nella distribuzione, il supporto per le foto degli utenti è lo stesso di quello disponibile con Lync 2010. Tuttavia, le opzioni degli utenti per la scelta della foto da usare sono diverse nel client Lync 2013. Nel client Lync 2013 gli utenti possono selezionare **Nascondi immagine** o **Mostra immagine**. L'opzione **Mostra un'immagine da un sito Web** non è disponibile per impostazione predefinita, ma può essere abilitata assegnando un criterio client.

## Nascondi immagine

Le impostazioni per le foto degli utenti sono disponibili nella finestra di dialogo **Opzioni** in Lync 2013. Quando si sceglie **Nascondi immagine**, non viene visualizzata alcuna foto dell'utente nel client Lync, ma la foto viene comunque visualizzata nella scheda contatto e all'esterno di Lync.

## Mostra immagine

Quando si sceglie l'opzione **Mostra immagine**, la foto dell'utente viene visualizzata nel client Lync e agli altri utenti nelle conversazioni Lync. L'immagine usata è quella archiviata in Servizi di dominio Active Directory.

## Mostra un'immagine da un sito Web

L'opzione **Mostra un'immagine da un sito Web** diventa disponibile in Lync 2013 dopo avere impostato un criterio client per abilitarla. La versione del client deve essere successiva alla 15.0.4535.1002, che viene installata con gli [aggiornamenti cumulativi di Lync di novembre 2013](http://go.microsoft.com/fwlink/p/?linkid=509908). Per gli utenti può essere necessario disconnettersi e quindi eseguire nuovamente l'accesso per visualizzare le modifiche nel client.

È possibile impostare il criterio client in modo da abilitare l'impostazione **Mostra un'immagine da un sito Web** eseguendo il criterio [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy) in Lync Server Management Shell. I cmdlet di esempio seguenti illustrano come impostare il criterio in modo globale per tutti gli utenti nella distribuzione:

```
$pe=New-CsClientPolicyEntry -Name EnablePresencePhotoOptions -Value True
```
```
$po=Get-CsClientPolicy -Identity Global
```
```
$po.PolicyEntry.Add($pe)
```
```
Set-CsClientPolicy -Instance $po
```

Quando un'immagine viene caricata nella cassetta postale dell'utente, Exchange crea automaticamente una versione a risoluzione inferiore dell'immagine, che può essere usata nelle applicazioni client. La foto dell'utente viene aggiornata anche in Servizi di dominio Active Directory.


> [!NOTE]
> Quando un file di immagine viene aggiornato in Servizi di dominio Active Directory, un'immagine da 48 per 48 pixel viene creata e usata per thumbnailPhoto in Servizi di dominio Active Directory. Qualsiasi immagine esistente viene sostituita. Se quindi è stata aggiunta a Servizi di dominio Active Directory un'immagine da 96 per 96 pixel, questa verrà sovrascritta dalla nuova immagine da 48 per 48 pixel. Ciò è importante solo se nell'ambiente sono presenti utenti che usano client Lync 2010, dal momento che tali client otterranno le foto degli utenti da Servizi di dominio Active Directory. È possibile importare immagini da 96 per 96 pixel per sostituire quelle create da Servizi di dominio Active Directory se nell'organizzazione sono presenti client Lync 2010.



## Supporto per le foto degli utenti in Lync 2013

In Lync 2013 sono supportate tre risoluzioni delle immagini per le foto degli utenti, come descritto nella tabella seguente. L'immagine usata viene determinata dall'impostazione del criterio client assegnata agli utenti di Lync. Per ulteriori informazioni, vedere “Gestione delle foto degli utenti con i cmdlet dei criteri client” in questo argomento.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Risoluzione dell'immagine (pixel)</th>
<th>Applicazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>48 x 48</p></td>
<td><p>Usata se non viene selezionata un'immagine con risoluzione superiore</p></td>
</tr>
<tr class="even">
<td><p>96 x 96</p></td>
<td><p>Usata in Outlook Web App e Outlook 2013</p></td>
</tr>
<tr class="odd">
<td><p>648 x 648</p></td>
<td><p>Usata nel client desktop Lync 2013 e Lync 2013 Web App</p></td>
</tr>
</tbody>
</table>


Qualsiasi utente con una cassetta postale abilitata in Exchange 2013 può caricare un'immagine differente, incluse foto ad alta risoluzione, tramite le opzioni di Outlook Web Access o del client Lync 2013. Le impostazioni consigliate per le immagini usate includono:

  - **Risoluzione dell'immagine**   648 per 648 pixel

  - **Intensità colore**   24 bit

  - **Dimensione del file di immagine**   fino a 20 MB

  - **Formato del file**   JPEG

Una tipica immagine JPEG a 24 bit da 648 per 648 pixel ha una dimensione del file di circa 240 KB, quindi è necessario 1 MB di spazio di archiviazione ogni 4 foto degli utenti.

