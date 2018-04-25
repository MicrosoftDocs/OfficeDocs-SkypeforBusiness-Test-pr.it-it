---
title: Impostazioni nuove e modificate per Lync 2013
TOCTitle: Impostazioni nuove e modificate per Lync 2013
ms:assetid: bb13789c-7eda-461c-a387-02ea8ca4dabe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205204(v=OCS.15)
ms:contentKeyID: 49301793
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostazioni nuove e modificate per Lync 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento vengono illustrate le modifiche dei cmdlet di Lync Server Management Shell direttamente correlate alla gestione client. In Lync Server 2013 sono stati introdotti diversi nuovi parametri, mentre i parametri per le funzionalità configurabili in altri modi sono deprecati.

## Nuovi parametri di gestione client


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nuovo</th>
<th>Cmdlet di Lync Server Management Shell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TracingLevel</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Se impostato su True, verrà abilitata la funzionalità di traccia del software in Lync. Se impostato su False, la funzionalità di traccia del software verrà disabilitata. La funzionalità di traccia del software comporta una registrazione dettagliata di tutte le attività di un programma, inclusa la traccia della chiamate API. Questo tipo di traccia è utile soprattutto per gli sviluppatori e il personale di supporto per le applicazioni. Questa impostazione equivale all'impostazione di Criteri di gruppo di Communications Server 2007 R2 &quot;Attiva traccia per Communicator&quot;. Le impostazioni sono le seguenti:</p>
<ul>
<li><p>Off = la traccia è disabilita e l'utente non può modificare questa impostazione.</p></li>
<li><p>Light = viene eseguita la traccia con livello minimo e l'utente non può modificare questa impostazione.</p></li>
<li><p>On = viene eseguita la traccia con livello dettagliato e l'utente non può modificare questa impostazione.</p></li>
</ul>
<p>Per impostazione predefinita, TracingLevel è impostato su un valore Null. Questo significa che verrà eseguita la traccia con livello minimo, ma che l'utente potrà abilitare o disabilitare questa traccia minima.</p></td>
</tr>
<tr class="even">
<td><p>EnableMediaRedirection</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Se impostato su True ($True), consente la separazione dei flussi audio e video dal resto del traffico di rete. I dispositivi client possono quindi eseguire la codifica e decodifica dei dati audio e video localmente. Il reindirizzamento dei dati multimediali in genere comporta un minore utilizzo della larghezza di banda, una maggiore scalabilità dei server e un'esperienza utente più ottimizzata rispetto a tecniche simili, come la gestione remota dei dispositivi o la compressione dei codec.</p></td>
</tr>
<tr class="odd">
<td><p>AllowLargeMeetings</p></td>
<td><p>CsConferencing</p></td>
<td><p>Se impostato su True, tutte le riunioni di Lync vengono considerate come &quot;riunioni di grandi dimensioni&quot;. Per queste riunioni, vengono applicate restrizioni relativamente al numero di notifiche inviate ai partecipanti, oltre alle dimensioni dell'elenco dei partecipanti alla riunione che viene trasmesso per impostazione predefinita.</p></td>
</tr>
<tr class="even">
<td><p>DisablePowerPointAnnotations</p></td>
<td><p>CsConferencing</p></td>
<td><p>Se impostato su True ($True), gli utenti non potranno aggiungere annotazioni alle diapositive di PowerPoint utilizzate in una conferenza. Tuttavia, a seconda del valore della proprietà AllowAnnotations, gli utenti potranno comunque accedere ad altre funzionalità della lavagna. Il valore predefinito è False, pertanto le annotazioni di PowerPoint sono consentite.</p></td>
</tr>
<tr class="odd">
<td><p>AllowSharedNotes</p></td>
<td><p>CsConferencing</p></td>
<td><p>Se impostato su True (valore predefinito), tutti gli eventuali blocchi appunti di OneNote aperti e collegati alla conferenza verranno aggiornati automaticamente con informazioni come i partecipanti alla conferenza e i dettagli sul contenuto condiviso durante la conferenza.</p></td>
</tr>
<tr class="even">
<td><p>EnableInviteCustomization</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>Utilizzato con gli altri nuovi parametri CsMeetingConfiguration per personalizzare gli inviti alle riunioni generati dal componente aggiuntivo per riunioni online per Lync 2013.</p></td>
</tr>
<tr class="odd">
<td><p>LogoURL</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>Aggiunge il logo dell'organizzazione a tutti gli inviti generati dal componente aggiuntivo per riunioni online per Lync 2013. È possibile specificare l'URL di un'immagine GIF o JPG.</p></td>
</tr>
<tr class="even">
<td><p>HelpURL</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>Aggiunge l'URL del servizio clienti o dell'assistenza tecnica dell'organizzazione a tutti gli inviti generati dal componente aggiuntivo per riunioni online per Lync 2013.</p></td>
</tr>
<tr class="odd">
<td><p>LegalURL</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>Aggiunge un testo di carattere legale o una dichiarazione di non responsabilità a tutti gli inviti generati dal componente aggiuntivo per riunioni online per Lync 2013. È possibile specificare l'URL del percorso del testo.</p></td>
</tr>
<tr class="even">
<td><p>CustomFooterText</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>Aggiunge un piè di pagina personalizzato a tutti gli inviti generati dal componente aggiuntivo per riunioni online per Lync 2013. È possibile specificare l'URL del percorso del testo di piè di pagina personalizzato.</p></td>
</tr>
<tr class="odd">
<td><p>IsPublicDisclosureAllowed</p></td>
<td><p>CsWebServiceConfiguration</p></td>
<td><p>Abilita la nuova versione 2013 di Lync Web App. La nuova versione di Lync Web App è disabilitata per impostazione predefinita e deve essere abilitata dall'amministratore.</p></td>
</tr>
</tbody>
</table>


## Parametri di gestione client deprecati


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Cmdlet di Lync Server Management Shell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EnableSQMData</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Il parametro EnableSQMData del cmdlet Set-CSClientPolicy è stato rimosso in Lync Server 2013. È invece possibile utilizzare l'impostazione condivisa di Criteri di gruppo per i dati SQM (Software Quality Management) per determinare l'interfaccia utente per l'opzione per l'Analisi utilizzo software nella pagina delle opzioni generali del client Lync:</p>
<p>HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\Common\QMEnable</p>
<p>Valori:</p>
<p>1 = la casella di controllo viene visualizzata e selezionata (l'utente può deselezionare la casella di controllo).</p>
<p>0 = la casella di controllo viene disattivata e disabilitata (l'utente non può modificare l'impostazione).</p>
<p>Null = il valore è determinato dal programma di installazione di Office e la casella di controllo viene visualizzata in modo che gli utenti possano impostarla come desiderato.</p></td>
</tr>
<tr class="even">
<td><p>AllowExchangeContactStore</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Questo parametro è stato rimosso. Quando si distribuisce Lync Server 2013 e si pubblica la topologia, l'archivio contatti unificato è però abilitato per tutti gli utenti per impostazione predefinita. Questo significa che tutti i contatti di un utente vengono mantenuti in Exchange e sono disponibili in Lync, Outlook e Outlook Web Access. È possibile utilizzare il cmdlet Set-CsUserServicesPolicy per personalizzare gli utenti per i quali è disponibile l'archivio contatti unificato. È possibile abilitare gli utenti globalmente, in base al sito, al tenant oppure a persone singole o gruppi di persone. Per informazioni dettagliate, vedere <a href="lync-server-2013-enable-users-for-unified-contact-store.md">Abilitare gli utenti per l'archivio contatti unificato in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MAPIPollInterval</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Questo parametro non viene utilizzato da Lync 2013. Nelle versioni precedenti questo parametro specifica la frequenza con cui il client recupera i dati MAPI dalle cartelle pubbliche di Exchange.</p></td>
</tr>
</tbody>
</table>

