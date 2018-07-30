---
title: 'Lync Server 2013: porte e protocolli per i server interni'
TOCTitle: Porte e protocolli per i server interni
ms:assetid: c94063f1-e802-4a61-be90-022fc185335e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398833(v=OCS.15)
ms:contentKeyID: 49301937
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Porte e protocolli per i server interni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono riepilogati i protocolli e le porte utilizzati dai server, dai servizi di bilanciamento del carico e dai client in una distribuzione di Lync Server.

> [!IMPORTANT]  
> Una comunicazione uno-a-uno tra un client di Lync e un client di Communicator viene spesso denominata peer-to-peer. Tecnicamente i due client comunicano mediante una conversazione uno-a-uno con l'unità IMMCU (Instant Messaging Multipoint Control Unit) nel mezzo. IMMCU è un componente di Front End Server. Se si posiziona IMMCU nel flusso di lavoro necessario per la comunicazione, è possibile utilizzare la registrazione dettagli chiamata e altre caratteristiche abilitate da Front End Server. La comunicazione avviene da una porta di origine dinamica sul client alla porta TLS/TCP/5061 di Front End Server, purché venga utilizzata la crittografia TLS (Transport Layer Security) consigliata. Per impostazione predefinita, la comunicazione peer-to-peer, così come la messaggistica istantanea con più partecipanti, è possibile solo se Lync Server e IMMCU sono attivi e disponibili.

## Informazioni dettagliate relative a porta e protocollo


> [!NOTE]
> Prima di avviare i servizi di Lync Server in un server, è necessario che sia in esecuzione Windows Firewall, perché è in questa fase che Lync Server apre le porte necessarie nel firewall.



Per informazioni dettagliate sulla configurazione del firewall per i componenti perimetrali, vedere [Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md).

Nella tabella seguente sono elencate le porte che è necessario aprire per ogni ruolo server interno.

### Porte server richieste (per ruolo server)

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo del server</th>
<th>Nome servizio</th>
<th>Porta</th>
<th>Protocollo</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tutti i server</p></td>
<td><p>SQL Browser</p></td>
<td><p>1434</p></td>
<td><p>UDP</p></td>
<td><p>SQL Browser per la copia locale replicata del database dell'archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>5060</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata facoltativamente dai server Standard Edition e dai Front End Server per le route statiche ai servizi trusted, ad esempio i server di controllo delle chiamate remote.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>5061</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata dai server Standard Edition e dai pool Front End per tutte le comunicazioni SIP interne tra i server (MTLS), per le comunicazioni SIP tra Server e Client (TLS), per le comunicazioni SIP tra Front End Server e Mediation Server (MTLS), nonché per le comunicazioni con Monitoring Server.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p>
<p>TCP</p></td>
<td><p>Utilizzata per le comunicazioni HTTPS tra il componente Focus, ovvero il componente di Lync Server che gestisce lo stato delle conferenze, e i singoli server.</p>
<p>Questa porta viene utilizzata anche per le comunicazioni TCP tra Survivable Branch Appliance e Front End Server.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>135</p></td>
<td><p>DCOM e RPC (Remote Procedure Call)</p></td>
<td><p>Utilizzata per le operazioni basate su DCOM quali spostamento utenti, sincronizzazione User Replicator e sincronizzazione rubrica.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio IM Conferencing di Lync Server</p></td>
<td><p>5062</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per le conferenze di messaggistica istantanea (IM).</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Web Conferencing di Lync Server</p></td>
<td><p>8057</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata per attendere le connessioni PSOM (Persistent Shared Object Model) dal client.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Web Conferencing Compatibility di Lync Server</p></td>
<td><p>8058</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata per attendere le connessioni PSOM (Persistent Shared Object Model) dal client Live Meeting e dalle versioni precedenti di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Audio/Video Conferencing di Lync Server</p></td>
<td><p>5063</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per Audio/Video (A/V) Conferencing.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Audio/Video Conferencing di Lync Server</p></td>
<td><p>57501-65535</p></td>
<td><p>TCP/UDP</p></td>
<td><p>Intervallo di porte di attesa multimediali utilizzato per le conferenze video.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Compatibilità Web di Lync Server</p></td>
<td><p>80</p></td>
<td><p>HTTP</p></td>
<td><p>Utilizzata per le comunicazioni dai Front End Server ai nomi di dominio completi della Web farm (gli URL utilizzati dai componenti Web IIS) quando non si utilizzano protocolli HTTPS.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Compatibilità Web di Lync Server</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
<td><p>Utilizzata per le comunicazioni dai Front End Server ai nomi di dominio completi della Web farm (gli URL utilizzati dai componenti Web IIS).</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Compatibilità Web di Lync Server</p></td>
<td><p>8080</p></td>
<td><p>TCP e HTTP</p></td>
<td><p>Utilizzata dai componenti Web per l'accesso esterno.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Componente server Web</p></td>
<td><p>4443</p></td>
<td><p>HTTPS</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Componente server Web</p></td>
<td><p>8060</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Componente server Web</p></td>
<td><p>8061</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Componente dei servizi per dispositivi mobili</p></td>
<td><p>5086</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Porta SIP utilizzata dai processi interni dei servizi per dispositivi mobili.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Componente dei servizi per dispositivi mobili</p></td>
<td><p>5087</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Porta SIP utilizzata dai processi interni dei servizi per dispositivi mobili.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Componente dei servizi per dispositivi mobili</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Operatore Conferenza di Lync Server (conferenze telefoniche con accesso esterno)</p></td>
<td><p>5064</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per le conferenze telefoniche con accesso esterno.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Operatore Conferenza di Lync Server (conferenze telefoniche con accesso esterno)</p></td>
<td><p>5072</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per Attendant (conferenze telefoniche con accesso esterno).</p></td>
</tr>
<tr class="even">
<td><p>Front End Server che eseguono anche un Mediation Server collocato</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata dal Mediation Server per le richieste in arrivo dal Front End Server al Mediation Server.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server che eseguono anche un Mediation Server collocato</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5067</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo dal gateway PSTN al Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server che eseguono anche un Mediation Server collocato</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5068</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo dal gateway PSTN al Mediation Server.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server che eseguono anche un Mediation Server collocato</p>
<p></p></td>
<td><p>Servizio Mediation di Lync Server</p>
<p></p></td>
<td><p>5081</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in uscita dal Mediation Server al gateway PSTN.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server che eseguono anche un Mediation Server collocato</p>
<p></p></td>
<td><p>Servizio Mediation di Lync Server</p>
<p></p></td>
<td><p>5082</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata per le richieste SIP in uscita dal Mediation Server al gateway PSTN.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio condivisione applicazioni di Lync Server</p></td>
<td><p>5065</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste di attesa SIP in arrivo per la condivisione delle applicazioni.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio condivisione applicazioni di Lync Server</p></td>
<td><p>49152-65535</p></td>
<td><p>TCP</p></td>
<td><p>Intervallo di porte di attesa multimediali per la condivisione delle applicazioni.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Annuncio conferenza di Lync Server</p></td>
<td><p>5073</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per il servizio Annuncio conferenza di Lync Server, ovvero per le conferenze telefoniche con accesso esterno.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio Parcheggio di chiamata di Lync Server</p></td>
<td><p>5075</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per l'applicazione Parcheggio di chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio Test audio di Lync Server</p></td>
<td><p>5076</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per il servizio Test audio.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Non applicabile</p></td>
<td><p>5066</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per il gateway Enhanced 9-1-1 (E9-1-1) in uscita.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Response Group Service di Lync Server</p></td>
<td><p>5071</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per l'applicazione Response Group.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Response Group Service di Lync Server</p></td>
<td><p>8404</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo per l'applicazione Response Group.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server</p></td>
<td><p>Servizio criteri larghezza di banda di Lync Server</p></td>
<td><p>5080</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per il controllo di ammissione di chiamata eseguito dal servizio criteri larghezza di banda per il traffico A/V Edge TURN.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server</p></td>
<td><p>Servizio criteri larghezza di banda di Lync Server</p></td>
<td><p>448</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per il servizio Controllo di ammissione di chiamata da parte del servizio criteri larghezza di banda di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p>Front End Server in cui risiede l'archivio di gestione centrale</p></td>
<td><p>Servizio Agente di replica master di Lync Server</p></td>
<td><p>445</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per estrarre i dati di configurazione dall'archivio di gestione centrale nei server che eseguono Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>Tutti i server</p></td>
<td><p>SQL Browser</p></td>
<td><p>1434</p></td>
<td><p>UDP</p></td>
<td><p>SQL Browser per la copia di replica locale dei dati di archivio di gestione centrale nell'istanza locale di SQL Server.</p></td>
</tr>
<tr class="odd">
<td><p>Tutti i server interni</p></td>
<td><p>Vari</p></td>
<td><p>49152-57500</p></td>
<td><p>TCP/UDP</p></td>
<td><p>Intervallo di porte multimediali utilizzato per le conferenze audio in tutti i server interni. Utilizzato da tutti i server che terminano l'audio: Front End Server (per il servizio Operatore Conferenza di Lync Server, il servizio Annuncio conferenza di Lync Server e il servizio Audio/Video Conferencing di Lync Server) e Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p>Server Office Web Apps</p></td>
<td><p></p></td>
<td><p>443</p></td>
<td><p></p></td>
<td><p>Utilizzata da Lync Server 2013 per la connessione al server Office Web Apps.</p></td>
</tr>
<tr class="odd">
<td><p>Director</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>5060</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata facoltativamente per le route statiche ai servizi trusted, come i server di controllo delle chiamate remote.</p></td>
</tr>
<tr class="even">
<td><p>Director</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p>
<p>TCP</p></td>
<td><p>Comunicazioni interne ai server tra Front End e Director. Inoltre, pubblicazione del certificato client (nei Front End Server) o convalida se il certificato client è stato già pubblicato.</p></td>
</tr>
<tr class="odd">
<td><p>Director</p></td>
<td><p>Servizio Compatibilità Web di Lync Server</p></td>
<td><p>80</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le comunicazioni iniziali dai Director ai nomi di dominio completo (FQDN) della Web farm (gli URL utilizzati dai componenti Web IIS). Durante il normale funzionamento, viene effettuato il passaggio al traffico HTTPS mediante la porta 443 e il tipo di protocollo TCP.</p></td>
</tr>
<tr class="even">
<td><p>Director</p></td>
<td><p>Servizio Compatibilità Web di Lync Server</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
<td><p>Utilizzata per le comunicazioni dai Director ai nomi di dominio completi (FQDN) della Web farm (gli URL utilizzati dai componenti Web IIS).</p></td>
</tr>
<tr class="odd">
<td><p>Director</p></td>
<td><p>Servizio Front End di Lync Server</p></td>
<td><p>5061</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le comunicazioni interne tra i server e per le connessioni client.</p></td>
</tr>
<tr class="even">
<td><p>Mediation Server</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata dal Mediation Server per le richieste in arrivo dal Front End Server.</p></td>
</tr>
<tr class="odd">
<td><p>Mediation Server</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5067</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo dal gateway PSTN.</p></td>
</tr>
<tr class="even">
<td><p>Mediation Server</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5068</p></td>
<td><p>TCP</p></td>
<td><p>Utilizzata per le richieste SIP in arrivo dal gateway PSTN.</p></td>
</tr>
<tr class="odd">
<td><p>Mediation Server</p></td>
<td><p>Servizio Mediation di Lync Server</p></td>
<td><p>5070</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Utilizzata per le richieste SIP dai Front End Server.</p></td>
</tr>
<tr class="even">
<td><p>Front End Server Chat persistente</p></td>
<td><p>SIP di Chat persistente</p></td>
<td><p>5041</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Front End Server Chat persistente</p></td>
<td><p>Windows Communication Foundation (WCF) di Chat persistente</p></td>
<td><p>881</p></td>
<td><p>TCP (TLS) e TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Front End Server Chat persistente</p></td>
<td><p>Servizio di trasferimento file di Chat persistente</p></td>
<td><p>443</p></td>
<td><p>TCP (TLS)</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Alcuni scenari di controllo delle chiamate remote richiedono una connessione TCP tra il Front End Server o Director e il sistema PBX. Sebbene Lync Server non utilizzi più la porta TCP 5060, durante la distribuzione del controllo delle chiamate remote viene creata una configurazione di server trusted che associa il nome di dominio completo del server linea RCC alla porta TCP che verrà utilizzata dal Front End Server o dal Director per la connessione al sistema PBX. Per informazioni dettagliate, vedere il cmdlet <STRONG>CsTrustedApplicationComputer</STRONG> nella documentazione relativa alla Lync Server Management Shell.



Per i pool che utilizzano solo il servizio di bilanciamento del carico hardware (non il servizio di bilanciamento del carico DNS), la tabella che segue mostra le porte che devono aprire i servizi di bilanciamento del carico hardware.

### Porte del servizio di bilanciamento del carico hardware se si utilizza solo questo servizio di bilanciamento

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servizio di bilanciamento del carico</th>
<th>Porta</th>
<th>Protocollo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>5061</p></td>
<td><p>TCP (TLS)</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>135</p></td>
<td><p>DCOM e RPC (Remote Procedure Call)</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>80</p></td>
<td><p>HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>8080</p></td>
<td><p>TCP - Recupero tramite client e dispositivi del certificato radice da Front End Server; client e dispositivi autenticati mediante NTLM</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (da proxy inverso)</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>5072</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p>
<p></p></td>
<td><p>5073</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p>
<p></p></td>
<td><p>5075</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p>
<p></p></td>
<td><p>5076</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p>
<p></p></td>
<td><p>5071</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p>
<p></p></td>
<td><p>5080</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p>
<p></p></td>
<td><p>448</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Mediation Server</p>
<p></p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server (se il pool esegue anche Mediation Server)</p>
<p></p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Director</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Director</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Director</p>
<p></p></td>
<td><p>5061</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Director</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (da proxy inverso)</p></td>
</tr>
</tbody>
</table>


È necessario che anche nei pool Front End e server Director che utilizzano il servizio di bilanciamento del carico DNS sia distribuito un servizio di bilanciamento del carico hardware. Nella tabella che segue sono indicate le porte che è necessario aprire in questi servizi di bilanciamento del carico hardware.

### Porte del servizio di bilanciamento del carico hardware se si utilizza il servizio di bilanciamento del carico DNS

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servizio di bilanciamento del carico</th>
<th>Porta</th>
<th>Protocollo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>80</p></td>
<td><p>HTTP</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>8080</p></td>
<td><p>TCP - Recupero tramite client e dispositivi del certificato radice da Front End Server; client e dispositivi autenticati mediante NTLM</p></td>
</tr>
<tr class="even">
<td><p>Servizio di bilanciamento del carico Front End Server</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (da proxy inverso)</p></td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Director</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="even">
<td> </td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Servizio di bilanciamento del carico Director</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (da proxy inverso)</p></td>
</tr>
</tbody>
</table>


### Porte client richieste

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Porta</th>
<th>Protocollo</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client</p></td>
<td><p>67/68</p></td>
<td><p>DHCP</p></td>
<td><p>Intervallo utilizzato da Lync Server per individuare il nome di dominio completo della funzione di registrazione, ovvero se si verifica un errore DNS SRV e non sono configurate impostazioni manuali.</p></td>
</tr>
<tr class="even">
<td><p>Client</p>
<p></p></td>
<td><p>443</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>Utilizzata per il traffico SIP da client a server per l'accesso utente esterno.</p></td>
</tr>
<tr class="odd">
<td><p>Client</p></td>
<td><p>443</p></td>
<td><p>TCP (PSOM/TLS)</p></td>
<td><p>Utilizzata per l'accesso utente esterno alle sessioni di Web Conferencing.</p></td>
</tr>
<tr class="even">
<td><p>Client</p></td>
<td><p>443</p></td>
<td><p>TCP (STUN/MSTURN)</p></td>
<td><p>Utilizzata per l'accesso utente esterno alle sessioni A/V e ai supporti multimediali (TCP).</p></td>
</tr>
<tr class="odd">
<td><p>Client</p></td>
<td><p>3478</p></td>
<td><p>UDP (STUN/MSTURN)</p></td>
<td><p>Utilizzata per l'accesso utente esterno alle sessioni A/V e ai supporti multimediali (UDP).</p></td>
</tr>
<tr class="even">
<td><p>Client</p></td>
<td><p>5061</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Utilizzata per il traffico SIP da client a server per l'accesso utente esterno.</p></td>
</tr>
<tr class="odd">
<td><p>Client</p></td>
<td><p>6891-6901</p></td>
<td><p>TCP</p></td>
<td><p>Intervallo utilizzato per il trasferimento file tra i client Lync e i client precedenti, ovvero i client di Microsoft Office Communications Server 2007 R2, Microsoft Office Communications Server 2007 e Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>Client</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP/UDP</p></td>
<td><p>Intervallo di porte audio (almeno 20 porte richieste).</p></td>
</tr>
<tr class="odd">
<td><p>Client</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP/UDP</p>
<p></p></td>
<td><p>Intervallo di porte video (almeno 20 porte richieste).</p></td>
</tr>
<tr class="even">
<td><p>Client</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP</p></td>
<td><p>Trasferimento file peer-to-peer (per il trasferimento dei file del servizio di conferenza, i client utilizzano PSOM).</p></td>
</tr>
<tr class="odd">
<td><p>Client</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP</p></td>
<td><p>Condivisione applicazioni.</p></td>
</tr>
<tr class="even">
<td><p>Telefono di area comune Aastra 6721ip</p>
<p>Telefono da tavolo Aastra 6725ip</p>
<p>Telefono IP HP 4110 (telefono di area comune)</p>
<p>Telefono IP HP 4120 (telefono da tavolo)</p>
<p>Telefono di area comune IP Polycom CX500</p>
<p>Telefono da tavolo IP Polycom CX600</p>
<p>Telefono da tavolo IP Polycom CX700</p>
<p>Telefono IP per conferenze Polycom CX3000</p></td>
<td><p>67/68</p></td>
<td><p>DHCP</p></td>
<td><p>Utilizzate dai dispositivi elencati per trovare il certificato di Lync Server, il nome di dominio completo (FQDN) del provisioning e l'FQDN della funzione di registrazione.</p></td>
</tr>
</tbody>
</table>


**\*** Per configurare porte specifiche per questi tipi di contenuto multimediale, utilizzare il cmdlet CsConferencingConfiguration (parametri ClientMediaPortRangeEnabled, ClientMediaPort e ClientMediaPortRange).


> [!NOTE]
> I programmi impostati per i client Lync creano automaticamente le eccezioni del firewall del sistema operativo necessarie nel computer client.




> [!NOTE]
> Le porte utilizzate per l'accesso utente esterno sono richieste per tutti gli scenari in cui il client deve attraversare il firewall dell'organizzazione, ad esempio per qualsiasi comunicazione o riunione esterna ospitata da altre organizzazioni.


