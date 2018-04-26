---
title: Utilizzo di Config.xml per l'esecuzione delle attività di installazione
TOCTitle: Utilizzo di Config.xml per l'esecuzione delle attività di installazione
ms:assetid: 0813184a-ab40-417c-b3a3-c2090766b831
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204651(v=OCS.15)
ms:contentKeyID: 49299593
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di Config.xml per l'esecuzione delle attività di installazione

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Anche se lo Strumento di personalizzazione di Office è lo strumento principale per la personalizzazione dell'installazione, gli amministratori possono utilizzare il file Config.xml per specificare ulteriori istruzioni di installazione non disponibili nello strumento. Le personalizzazioni seguenti possono essere eseguite solo utilizzando il file Config.xml:

  - Specifica della posizione di installazione dalla rete.

  - Scelta dei prodotti da installare.

  - Configurazione della registrazione e del percorso del file di configurazione dell'installazione e degli aggiornamenti software.

  - Specifica delle opzioni di installazione, ad esempio il nome utente.

  - Copia dell'origine di installazione locale nel computer dell'utente senza installare Office.

  - Aggiunta o rimozione di lingue dall'installazione.

Per configurare l'installazione invisibile all'utente di Lync 2013 è consigliabile utilizzare il file Config.xml.

Per impostazione predefinita, il file Config.xml archiviato nella cartella principale di un prodotto, ad esempio \\*prodotto*.WW, consente l'installazione del prodotto stesso. Il file Config.xml nella cartella seguente, ad esempio, consente l'installazione di Lync 2013:

  - \\\\server\\condivisione\\Lync15\\Lync.WW \\Config.xml

Nella tabella seguente sono elencati gli elementi di Config.xml più comunemente utilizzati per l'installazione di Lync 2013.

### Elementi di Config.xml

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configuration</p></td>
<td><p>Elemento di primo livello (obbligatorio). Contiene l'attributo relativo al prodotto, ad esempio Product=Lync</p></td>
</tr>
<tr class="even">
<td><p>OptionState</p></td>
<td><p>Specifica le modalità di gestione di specifiche funzionalità del prodotto durante l'installazione. Utilizzare gli attributi seguenti per impedire l'installazione di Servizi di integrazione applicativa, che include componenti condivisi che interferiscono con Outlook 2010:</p>
<ul>
<li><p>Id=&quot;LOBiMain&quot;</p></li>
<li><p>State=&quot;Absent&quot;</p></li>
<li><p>Children=&quot;Force&quot;</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Display</p>
<p></p></td>
<td><p>Livello di interfaccia utente che il programma di installazione mostra all'utente. Gli attributi tipici includono i seguenti:</p>
<ul>
<li><p>CompletionNotice=&quot;Yes&quot; | &quot;No&quot;(impostazione predefinita)</p></li>
<li><p>AcceptEula=&quot;Yes&quot; | &quot;No&quot;(impostazione predefinita)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Logging</p></td>
<td><p>Opzioni relative al tipo di registrazione eseguita dal programma di installazione. Gli attributi tipici includono i seguenti:</p>
<ul>
<li><p>Type =&quot;Off&quot; | &quot;Standard&quot;(impostazione predefinita) | &quot;Verbose&quot;</p></li>
<li><p>Template=”<em>nomefile</em>.txt” (nome del file di log)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Setting</p></td>
<td><p>Specifica i valori delle proprietà di Windows Installer. Gli attributi tipici includono i seguenti:</p>
<ul>
<li><p>Setting Id=&quot;<em>nome</em>&quot; (nome della proprietà di Windows Installer)</p></li>
<li><p>Value=&quot;<em>valore</em>&quot; (valore da assegnare alla proprietà)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DistributionPoint</p></td>
<td><p>Percorso completo della posizione di installazione dalla rete da cui viene eseguita l'installazione. Include l'attributo di posizione:</p>
<ul>
<li><p>Location=”<em>percorso</em>”</p></li>
</ul></td>
</tr>
</tbody>
</table>


L'esempio seguente mostra il file Config.xml di una tipica installazione invisibile all'utente di Lync 2013.

    <Configuration Product="Lync">
      <OptionState Id="LOBiMain" State="Absent" Children="Force" />
      <Display Level="None" CompletionNotice="No" AcceptEula="Yes" />
      <Logging Type="verbose" Path="%temp%" Template="LyncSetupVerbose(*).log" />
      <Setting Id="SETUP_REBOOT" Value="Never" />
      <DistributionPoint Location="\\server\share\Lync15" />
    </Configuration>

Informazioni dettagliate sull'utilizzo del file Config.xml per eseguire le attività di installazione e manutenzione di Office sono disponibili all'indirizzo [http://go.microsoft.com/fwlink/?linkid=267514\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=267514%26clcid=0x410).

## Per personalizzare il file Config.xml

1.  Aprire il file Config.xml con un editor di testo, ad esempio Blocco note.

2.  Individuare le righe che contengono gli elementi da modificare.

3.  Modificare la voce di elemento con le opzioni di installazione invisibile all'utente da utilizzare. Assicurarsi di rimuovere i delimitatori di commenti, "\<\!--" e "--\>". Ad esempio, utilizzare la sintassi seguente:
    
        < DistributionPoint Location="\\server\share\Lync15" />

4.  Salvare il file Config.xml.

