---
title: Amministrazione del servizio Rubrica in Lync Server 2013
TOCTitle: Amministrazione del servizio Rubrica in Lync Server 2013
ms:assetid: 801e4243-9670-4477-aa2f-88b61ecf5351
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429711(v=OCS.15)
ms:contentKeyID: 49301131
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Amministrazione del servizio Rubrica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il servizio Rubrica viene installato per impostazione predefinita come parte di una distribuzione del Lync Server, Enterprise Edition o server Standard Edition. Il database utilizzato dal servizio Rubrica, RTCab, è creato in SQL Server (per Enterprise Edition, si tratta dell'istanza di SQL Server back end; per server Standard Edition, si tratta dell'istanza di SQL Server collocata).


> [!NOTE]
> Per informazioni sull'utilizzo di <STRONG>ADSI Edit</STRONG> per modificare gli attributi degli oggetti di Servizi di dominio Active Directory, vedere <A href="http://go.microsoft.com/fwlink/?linkid=330427">ADSI Edit</A>. Per informazioni sugli strumenti specifici del Resource Kit per il servizio Rubrica, vedere <A href="http://go.microsoft.com/fwlink/?linkid=330429">Strumenti del Resource Kit di Microsoft Lync Server 2013</A>.



## Normalizzazione dei numeri di telefono del server della Rubrica

Lync Server richiede i numeri di telefono nel formato standard RFC 3966/E.164. Per utilizzare numeri di telefono non strutturati o formattati in modo incoerente, in Lync Server viene utilizzato il server della Rubrica per pre-elaborare i numeri di telefono prima che vengano passati alle regole di normalizzazione. Quando viene utilizzato un numero di telefono dalla Rubrica e viene applicata la regola di normalizzazione, i client, ad esempio Lync Phone Edition e Lync Mobile possono utilizzare questi numeri normalizzati.

Le regole di normalizzazione utilizzate nelle versioni precedenti potrebbero non funzionare correttamente senza alcune modifiche. Poiché gli spazi vuoti e i caratteri non obbligatori vengono rimossi prima delle regole di normalizzazione, se l'espressione regex cerca in modo specifico un trattino o un altro carattere che è stato rimosso, la regola di normalizzazione potrebbe non riuscire. È opportuno esaminare le regole di normalizzazione per garantire che non cerchino questi caratteri non obbligatori o che un errore della regola non impedisca la continuazione nel caso in cui il carattere non sia presente dove previsto dalla regola stessa.

## User Replicator e server della Rubrica

Il server della Rubrica utilizza i dati forniti da User Replicator per aggiornare le informazioni ottenute inizialmente dall'elenco indirizzi globale. User Replicator scrive gli attributi di Servizi di dominio Active Directory per ogni utente, contatto e gruppo nella tabella AbUserEntry nel database e il server della Rubrica sincronizza i dati utente del database in file nell'archivio file del server della Rubrica e nel database della Rubrica, RTCab o RTCab1. Lo schema per la tabella AbUserEntry prevede l'utilizzo di due colonne, **UserGuid** e **UserData**. **UserGuid** è la colonna di indice e contiene il GUID a 16 byte dell'oggetto Active Directory. **UserData** è una colonna immagini che contiene tutti gli attributi di Servizi di dominio Active Directory menzionati in precedenza per il contatto.

User Replicator determina gli attributi di Active Directory da scrivere leggendo una tabella di configurazione che si trova nella stessa istanza basata su SQL Server della tabella AbUserEntry. La tabella AbAttribute contiene tre colonne, **ID**, **Name**, **Flags** e **Enable**. La tabella viene creata durante l'impostazione del database. Se la tabella AbAttribute è vuota,User Replicator ignora la logica di elaborazione della tabella AbUserEntry. Gli attributi del server della Rubrica sono dinamici e vengono recuperati dalla tabella AbAttribute, che viene inizialmente scritta dal server della Rubrica quando questo viene attivato.

In seguito all'attivazione del server della Rubrica la tabella AbAttribute viene popolata con i valori indicati nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ID</th>
<th>Nome</th>
<th>Flag</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>givenName</p></td>
<td><p>0x01400000</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Sn</p></td>
<td><p>0x02400000</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>displayName</p></td>
<td><p>0x03420000</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>Title</p></td>
<td><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p>mailNickname</p></td>
<td><p>0x05400000</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p>Company</p></td>
<td><p>0x06000000</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p>physicalDeliveryOfficeName</p></td>
<td><p>0x07000000</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>msRTCSIP-PrimaryUserAddress</p></td>
<td><p>0x08520C00</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>telephoneNumber</p></td>
<td><p>0x09022800</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>homePhone</p></td>
<td><p>0x0A302800</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p>Mobile</p></td>
<td><p>0x0B622800</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>otherTelephone</p></td>
<td><p>0x0C302000</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p>ipPhone</p></td>
<td><p>0x0D302000</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p>Mail</p></td>
<td><p>0x0E500000</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p>groupType</p></td>
<td><p>0x0F010800</p></td>
</tr>
<tr class="even">
<td><p>16</p></td>
<td><p>Department</p></td>
<td><p>0x10000000</p></td>
</tr>
<tr class="odd">
<td><p>17</p></td>
<td><p>Description</p></td>
<td><p>0x11000100</p></td>
</tr>
<tr class="even">
<td><p>18</p></td>
<td><p>Manager</p></td>
<td><p>0x12040001</p></td>
</tr>
<tr class="odd">
<td><p>19</p></td>
<td><p>proxyAddress</p></td>
<td><p>0x00500105</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>msExchHideFromAddressLists</p></td>
<td><p>0xFF000003</p></td>
</tr>
<tr class="odd">
<td><p>99</p></td>
<td><p>entryID</p></td>
<td><p>0x99000000</p></td>
</tr>
</tbody>
</table>


I numeri nella colonna **ID** devono essere univoci e non devono mai essere riutilizzati. Inoltre, mantenendo i valori ID inferiori a 256, si risparmia spazio nei file di output scritti dal server della Rubrica. Tuttavia, il valore ID massimo è 65535. La colonna **Name** corrisponde al nome di attributo di Active Directory che deve essere inserito da User Replicator nella tabella AbUserEntry per ogni contatto. Il valore nella colonna **Flags** è utilizzato per definire il tipo di attributo. I tipi seguenti di attributi del server della Rubrica sono riconosciuti da User Replicator, indicati dal bit basso del valore nella colonna **Flags**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x0</p></td>
<td><p>Attributo stringa. Questo tipo viene convertito da User Replicator in formato UTF-8 prima dell'archiviazione nella tabella AbUserEntry.</p></td>
</tr>
<tr class="even">
<td><p>0x1</p></td>
<td><p>Attributo binario. Viene archiviato da User Replicator nell'oggetto blob senza alcuna conversione.</p></td>
</tr>
<tr class="odd">
<td><p>0x2</p></td>
<td><p>Attributo stringa, incluso solo se il valore dell'attributo inizia con &quot;tel:&quot;. È utilizzato principalmente per attributi stringa multivalore, in particolare <strong>proxyAddresses</strong>. In questo caso, il server della Rubrica considera solo le voci <strong>proxyAddresses</strong> che iniziano con &quot;tel:&quot;. Per risparmiare spazio, pertanto, tramite User Replicator vengono archiviate solo le voci che iniziano con &quot;tel:&quot;.</p></td>
</tr>
<tr class="even">
<td><p>0x3</p></td>
<td><p>Attributo stringa booleano. Se l'impostazione è TRUE, il contatto non viene incluso da User Replicator nella tabella AbUserEntry. Se l'impostazione è FALSE, gli attributi per il contatto vengono inclusi da User Replicator nella tabella AbUserEntry, ad eccezione dell'attributo specifico con questo flag. Si tratta di un altro tipo di caso speciale utilizzato principalmente per l'attributo <strong>msExchHideFromAddressLists</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>0x4</p></td>
<td><p>Attributo stringa, incluso solo se il valore dell'attributo inizia con &quot;smtp:&quot; e include il simbolo &quot;@&quot;.</p></td>
</tr>
<tr class="even">
<td><p>0x5</p></td>
<td><p>Attributo stringa, incluso solo se il valore dell'attributo inizia con &quot;tel:&quot; o &quot;smtp:&quot; e include il simbolo &quot;@&quot;.</p></td>
</tr>
<tr class="odd">
<td><p>0x100</p></td>
<td><p>Se impostato, si tratta di un attributo multivalore che può essere presente più volte per ogni contatto.</p></td>
</tr>
<tr class="even">
<td><p>0x400</p></td>
<td><p>Se impostato, identifica l'attributo del nome account utente di posta elettronica per un contatto. Questo flag viene utilizzato dal server della Rubrica per identificare il valore di attributo da visualizzare nella voce del registro eventi di normalizzazione del telefono.</p></td>
</tr>
<tr class="odd">
<td><p>0x800</p></td>
<td><p>Se impostato, identifica un attributo obbligatorio per un contatto. Il server della Rubrica include un utente nella tabella AbUserEntry solo se è presente un valore per questo attributo in Active Directory. Se sono presenti più attributi obbligatori, è necessario che solo uno di essi disponga di un valore per includere l'utente nella tabella AbUserEntry.</p></td>
</tr>
<tr class="even">
<td><p>0x1000</p></td>
<td><p>Se impostato, il valore di questo attributo viene sempre normalizzato dal server della Rubrica.</p></td>
</tr>
<tr class="odd">
<td><p>0x2000</p></td>
<td><p>Se impostato, il server della Rubrica utilizza il numero normalizzato di <strong>proxyAddresses</strong>, se l'impostazione CMS di <strong>UseNormalizationRules</strong> è FALSE; in caso contrario, il comportamento corrisponde a quello che si verifica quando il bit di flag è 0x1000.</p></td>
</tr>
<tr class="even">
<td><p>0x4000</p></td>
<td><p>Se impostato, il server della Rubrica non include nella tabella AbUserEntry oggetti con questo valore per l'attributo specificato. Se, ad esempio, per l'attributo <strong>msRTCSIP-PrimaryUserAddress</strong> è impostato questo bit di flag, i contatti con questo attributo non vengono scritti nel database.</p></td>
</tr>
<tr class="odd">
<td><p>0x8000</p></td>
<td><p>Se impostato, il server della Rubrica non include nella tabella AbUserEntry oggetti che non hanno questo valore per l'attributo specificato. Se entrambi i bit di flag 0x4000 e 0x8000 sono impostati in un oggetto, l'attributo con il valore del bit di flag impostato su 0x4000 ha la precedenza e l'oggetto viene escluso dalla tabella AbUserEntry.</p></td>
</tr>
<tr class="even">
<td><p>0x10000</p></td>
<td><p>Se impostato, rappresenta un oggetto gruppo. Questo bit di flag viene utilizzato da User Replicator per includere i contatti con l'attributo <strong>groupType</strong>, la cui presenza indica un gruppo (ad esempio, una lista di distribuzione o un gruppo di sicurezza).</p></td>
</tr>
<tr class="odd">
<td><p>0x20000</p></td>
<td><p>Se impostato, questo bit di flag viene utilizzato da User Replicator per includere questo attributo nei file del server della Rubrica specifici del dispositivo, ovvero file con estensione dabs.</p></td>
</tr>
</tbody>
</table>


Nelle versioni precedenti di Lync Server, quando si applica una modifica a Active Directory, l'amministratore deve eseguire i cmdlet **Update -CSUserDatabase** e **Update –CSAddressBook**Windows PowerShell affinché le modifiche rimarranno permanenti nel database utenti e RTCab di Lync Server immediatamente. In Lync Server 2013, User Replicator di Lync Server raccoglie le modifiche da Active Directory e aggiorna il database utenti di Lync Server sulla base di un intervallo configurato. User Replicator di Lync Server propaga inoltre le modifiche al database RTCab in maniera rapida, e senza che l'amministratore debba eseguire Update-CSAddressBook. Se il servizio query Web della Rubrica è abilitato, le modifiche saranno riflesse nei risultati di ricerca dai client di Lync. Gli amministratori devono eseguire Update -CSAddressBook se il download dei file della Rubrica è abilitato.


> [!NOTE]
> Per impostazione predefinita, User Replicator di Lync Server è eseguito automaticamente ogni 5 minuti. È possibile configurare questo intervallo utilizzando Set -CSUserReplicatorConfiguration -ReplicationCycleInterval &lt;&gt;.



## Filtro della Rubrica

Gli utenti inseriti nei file del server della Rubrica possono essere controllati in base a determinati attributi di Servizi di dominio Active Directory elencati nella tabella AbAttribute. Uno di questi attributi utilizzato per il filtro è **msExchangeHideFromAddressBook** . Si tratta di un attributo utente aggiunto dallo schema di Exchange. Se il valore di questo attributo è TRUE, questo attributo viene utilizzato da Exchange Server per nascondere il contatto dall'elenco indirizzi globale di Outlook. Analogamente, se il valore di questo attributo è TRUE, tale utente non viene incluso da User Replicator nella tabella AbUserEntry e l'utente non sarà presente nei file del server della Rubrica.

È possibile utilizzare alcuni bit di flag per definire un filtro da utilizzare per gli attributi del server della Rubrica. La presenza di alcuni bit di flag consente, ad esempio, di identificare un attributo come attributo di inclusione o di esclusione. User Replicator consente di escludere tramite filtro i contatti che contengono un attributo di esclusione e quelli che non contengono un attributo di inclusione.


> [!WARNING]
> Per ulteriori informazioni sul meccanismo di filtro della Rubrica, vedere <A href="https://technet.microsoft.com/en-us/library/gg415643(v=ocs.15)">Cmdlet per i server della Rubrica</A> e <A href="http://go.microsoft.com/fwlink/?linkid=330430">Filtrare la Rubrica di Lync 2013</A>



Attualmente, sono disponibili tre diversi filtri, elencati nella tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x800</p></td>
<td><p>Se impostato, identifica un attributo obbligatorio per un contatto. Questo bit di flag viene utilizzato da User Replicator per escludere tramite filtro i contatti che non includono almeno un attributo obbligatorio. OuPathId è un attributo obbligatorio, che è sempre impostato. È pertanto necessario che sia impostato almeno un altro degli attributi obbligatori. In caso contrario, il contatto (ovvero con il valore dell'attributo obbligatorio OuPathId) non sarà scritto nel database. Se, ad esempio, <strong>telephoneNumber</strong> e <strong>homePhone</strong> sono definiti come attributi obbligatori, solo i contatti che dispongono di almeno uno di questi attributi vengono scritti nel database.</p></td>
</tr>
<tr class="even">
<td><p>0x4000</p></td>
<td><p>Se impostato, identifica un attributo di esclusione. Questo bit di flag viene utilizzato da User Replicator per escludere tramite filtro i contatti che contengono questo attributo. Se, ad esempio, <strong>msRTCSIP-PrimaryUserAddress</strong> è definito come attributo di esclusione, i contatti che dispongono di questo attributo non vengono scritti nel database.</p></td>
</tr>
<tr class="odd">
<td><p>0x8000</p></td>
<td><p>Se impostato, identifica un attributo di inclusione. Questo bit di flag viene utilizzato da User Replicator per escludere tramite filtro i contatti che non contengono questo attributo. Se, ad esempio, <strong>msRTCSIP-PrimaryUserAddress</strong> è definito come attributo di inclusione, solo i contatti che dispongono di questo attributo vengono scritti nel database.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se vengono impostati entrambi i bit di flag, 0x4000 (attributo di esclusione) e 0x8000 (attributo di inclusione), il bit 0x4000 ha la precedenza su 0x8000 e il contatto viene escluso.



Sebbene sia possibile filtrare la Rubrica per includere solo determinati utenti, la limitazione delle voci non implica una limitazione della possibilità da parte di altri utenti di contattare gli utenti esclusi tramite filtro o di visualizzare il loro stato presenza. Gli utenti possono sempre trovare gli utenti non inclusi nella Rubrica, inviare loro manualmente messaggi istantanei o avviare manualmente chiamate verso tali utenti, immettendo il nome di accesso completo dell'utente. Le informazioni sul contatto per un utente sono inoltre disponibili anche in Outlook.

Sebbene la presenza di record dei contatti completi nei file della Rubrica consenta di utilizzare Lync Server per avviare scambi di posta elettronica, conversazioni telefoniche o chiamate VoIP aziendale (se VoIP aziendale è abilitato nel server) con utenti non configurati per SIP (Session Initiation Protocol), alcune organizzazioni preferiscono includere solo gli utenti abilitati per SIP nelle voci del server della Rubrica. È possibile filtrare la Rubrica per includere solo gli utenti abilitati per SIP cancellando il bit 0x800 nella colonna **Flags** per gli attributi obbligatori seguenti: **mailNickname**, **telephoneNumber**, **homePhone** e **mobile**. È inoltre possibile filtrare la Rubrica per includere solo utenti abilitati per SIP impostando 0x8000 (attributo di inclusione) nella colonna **Flags** dell'attributo **msRTCSIP-PrimaryUserAddress**. In questo modo vengono inoltre esclusi gli account del servizio dai file della Rubrica.

Dopo aver modificato la tabella AbAttribute, è possibile aggiornare i dati nella tabella AbUserEntry eseguendo il cmdlet **Update-CsUserDatabase**. Al termine della replica di User Replicator, è possibile aggiornare il file dell'archivio file del server della Rubrica eseguendo manualmente il cmdlet **UpdateCsAddressBook**.


> [!NOTE]
> Il Front End Server in cui si trova il server della Rubrica non può essere configurato a livello amministrativo. Viene scelto un server durante la distribuzione, in genere il primo Front End Server distribuito. In caso di guasto, il servizio Rubrica viene spostato in un altro server Front End Server, senza che sia necessario un intervento amministrativo.



> [!IMPORTANT]  
> Se l'infrastruttura è stata consolidata o modificata in altro modo da una distribuzione a più foreste o padre/figlio (ad esempio in caso di consolidamento dell'infrastruttura prima di passare a Lync Server), il download del servizio Rubrica e le query Web sulla Rubrica potrebbero non riuscire per alcuni utenti. In una distribuzione con più domini o foreste, l'attributo <strong>MsRTCSIP-OriginatorSid</strong> viene popolato negli oggetti utente in cui si presenta il problema. Per risolvere il problema, l'attributo <strong>MsRTCSIP-OriginatorSid</strong> deve essere impostato su NULL in questi oggetti.
