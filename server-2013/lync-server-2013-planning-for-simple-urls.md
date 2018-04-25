---
title: 'Lync Server 2013: Pianificazione degli URL semplici'
TOCTitle: Pianificazione degli URL semplici
ms:assetid: 20e4f4b6-b7ff-4297-b00d-d1211ee800ac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398287(v=OCS.15)
ms:contentKeyID: 49299908
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione degli URL semplici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Gli URL semplici consentono agli utenti di partecipare più facilmente alle riunioni e agli amministratori di accedere più agevolmente agli strumenti di amministrazione di Lync Server.

Lync Server supporta tre URL semplici:

  - L'URL **riunione** viene utilizzato come URL di base per tutte le conferenze nel sito o nell'organizzazione. Un URL di una riunione potrebbe essere https://meet.contoso.com, mentre un URL riunione particolare può essere https://meet.contoso.com/ *nome utente* /7322994.
    
    Con l'URL semplice riunione, i collegamenti per partecipare alle riunioni sono semplici da capire, da comunicare e da distribuire.

  - L'URL per **accesso esterno** consente di accedere alla pagina Web Impostazioni conferenza telefonica con accesso esterno. In questa pagina vengono visualizzati i numeri di accesso alle conferenze con le lingue disponibili, le informazioni sulla conferenza assegnate (ovvero per riunioni che non devono essere pianificate) e i controlli DTMF in conferenza. Questa pagina supporta la gestione del PIN e delle informazioni sulla conferenza assegnate. L'URL semplice per accesso esterno è incluso in tutti gli inviti a conferenze, in modo che gli utenti che desiderano eseguire l'accesso esterno alla conferenza dispongano delle informazioni sul numero di telefono e il PIN. Un esempio di URL semplice per accesso esterno è https://dialin.contoso.com.

  - L'URL di **amministrazione** consente di accedere rapidamente al Pannello di controllo di Lync Server. Da qualsiasi computer all'interno dei firewall dell'organizzazione un amministratore può aprire il Pannello di controllo di Lync Server digitando l'URL semplice di amministrazione in un browser. Tale URL è interno all'organizzazione. Un esempio dell'URL semplice di amministrazione è https://admin.contoso.com

## Ambito degli URL semplici

È possibile configurare gli URL semplici per un ambito globale oppure specificare URL semplici diversi per ogni sito centrale dell'organizzazione. Se vengono specificati sia un URL semplice globale che un URL semplice di sito, quest'ultimo avrà la priorità.

Nella maggior parte dei casi, è consigliabile impostare gli URL semplici solo a livello globale, in modo che l'URL semplice riunione di un utente non cambi con lo spostamento da un sito a un altro. L'eccezione è rappresentata da organizzazioni che devono utilizzare numeri di telefono diversi per gli utenti connessi tramite chiamata in ingresso in siti diversi. Si noti che se si imposta in un sito un URL semplice a livello di sito, ad esempio per l'accesso esterno, sarà necessario impostare a livello di sito anche gli altri URL semplici del sito.

È possibile impostare URL semplici globali in Generatore di topologie. Per impostare un URL semplice a livello di sito, è necessario utilizzare il cmdlet Set-CsSimpleURLConfiguration.

## Denominazione degli URL semplici

Sono disponibili tre opzioni consigliate per denominare gli URL semplici. L'opzione scelta determina il modo in cui vengono configurati i certificati e i record A DNS che supportano gli URL semplici. In ogni opzione è necessario configurare un URL semplice riunione per ogni dominio SIP dell'organizzazione.

Sono sufficienti sempre nell'intera organizzazione un solo URL semplice per accesso esterno e uno di amministrazione, indipendentemente dal numero di domini SIP presenti.

Per informazioni dettagliate sui certificati e i record A DNS necessari, vedere [Requisiti DNS per gli URL semplici in Lync Server 2013](lync-server-2013-dns-requirements-for-simple-urls.md) e [Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md) nella documentazione relativa alla pianificazione.

Nell'opzione 1 viene creato un nuovo nome di dominio SIP per ogni URL semplice.

Se si utilizza questa opzione, è necessario un record A DNS separato per ogni URL semplice e ogni URL semplice riunione deve essere denominato nei certificati.

### Opzione 1 di denominazione degli URL semplici

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>URL semplice</strong></p></td>
<td><p><strong>Esempio</strong></p></td>
</tr>
<tr class="even">
<td><p>URL riunione</p></td>
<td><p>https://meet.contoso.com, https://meet.fabrikam.com e così via (uno per ogni dominio SIP dell'organizzazione)</p></td>
</tr>
<tr class="odd">
<td><p>Accesso esterno</p></td>
<td><p>https://dialin.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>URL di amministrazione</p></td>
<td><p>https://admin.contoso.com</p></td>
</tr>
</tbody>
</table>


Con l'opzione 2, gli URL semplici sono basati sul nome di dominio lync.contoso.com. È necessario pertanto un solo record A DNS che consenta tutti e tre i tipi di URL semplici. Questo record A DNS fa riferimento a lync.contoso.com. Sono sempre necessari però record A DNS separati per altri domini SIP dell'organizzazione.

### Opzione 2 di denominazione degli URL semplici

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>URL semplice</strong></p></td>
<td><p><strong>Esempio</strong></p></td>
</tr>
<tr class="even">
<td><p>URL riunione</p></td>
<td><p>https://lync.contoso.com/Meet, https://lync.fabrikam.com/Meet e così via (uno per ogni dominio SIP dell'organizzazione)</p></td>
</tr>
<tr class="odd">
<td><p>Accesso esterno</p></td>
<td><p>https://lync.contoso.com/Dialin</p></td>
</tr>
<tr class="even">
<td><p>URL di amministrazione</p></td>
<td><p>https://lync.contoso.com/Admin</p></td>
</tr>
</tbody>
</table>


L'opzione 3 è più utile se si dispone di numerosi domini SIP e si desidera che dispongano di URL semplici riunione separati, riducendo però al minimo i requisiti dei certificati e dei record DNS per questi URL semplici.

### Opzione 3 di denominazione degli URL semplici

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>URL semplice</strong></p></td>
<td><p><strong>Esempio</strong></p></td>
</tr>
<tr class="even">
<td><p>URL riunione</p></td>
<td><p>https://lync.contoso.com/contosoSIPdomain/Meet</p>
<p>https://lync.contoso.com/fabrikamSIPdomain/Meet</p></td>
</tr>
<tr class="odd">
<td><p>Accesso esterno</p></td>
<td><p>https://lync.contoso.com/Dialin</p></td>
</tr>
<tr class="even">
<td><p>URL di amministrazione</p></td>
<td><p>https://lync.contoso.com/Admin</p></td>
</tr>
</tbody>
</table>


## Regole di denominazione e convalida degli URL semplici

Generatore di topologie e i cmdlet di Lync Server Management Shell applicano diverse regole di convalida per gli URL semplici. È obbligatorio impostare URL semplici riunione e per accesso esterno, mentre l'impostazione dell'URL semplice di amministrazione è facoltativa. Ogni dominio SIP deve disporre di un URL semplice riunione separato, ma sono sufficienti un URL semplice per accesso esterno e un URL semplice di amministrazione per l'intera organizzazione.

Ogni URL semplice dell'organizzazione deve avere un nome univoco e non può essere un prefisso di un altro URL semplice. Non è possibile ad esempio impostare lync.contoso.com/Meet come URL semplice riunione e lync.contoso.com/Meet/Dialin com URL semplice per accesso esterno. I nomi degli URL semplici non possono includere l'FQDN dei pool o altre informazioni sulle porte, ad esempio https://FQDN:88/meet non è consentito. Tutti gli URL semplici devono iniziare con il prefisso https://.

Gli URL semplici possono includere solo caratteri alfanumerici, ovvero a-z, A-Z, 0-9 e il punto (.). Se si utilizzano altri caratteri, gli URL semplici potrebbero non funzionare come previsto.

## Modifica degli URL semplici dopo la distribuzione

Se si modifica un URL semplice dopo la distribuzione iniziale, è necessario tenere conto dell'impatto delle modifiche sui record DNS e i certificati per gli URL semplici. Se la modifica la base di un URL semplice, sarà necessario modificare anche i certificati e i record DNS. Se ad esempio si cambia https://lync.contoso.com/Meet in https://meet.contoso.com, l'URL di base cambia da lync.contoso.com in meet.contoso.com. In tal caso, sarà necessario modificare i certificati e i record DNS in modo che facciano riferimento a meet.contoso.com. Se invece si cambia l'URL semplice da https://lync.contoso.com/Meet in https://lync.contoso.com/Meetings, l'URL di base lync.contoso.com resta invariato e pertanto non è necessario apportare modifiche ai certificati o ai record DNS.

Ogni volta che si modifica il nome di un URL semplice, tuttavia, è necessario eseguire **Enable-CsComputer** in ogni Director e Front End Server per registrare la modifica.

## Vedere anche

#### Concetti

[Requisiti DNS per gli URL semplici in Lync Server 2013](lync-server-2013-dns-requirements-for-simple-urls.md)

