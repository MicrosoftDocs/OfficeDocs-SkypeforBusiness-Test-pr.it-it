---
title: 'Lync Server 2013: test del ripristino di emergenza'
TOCTitle: Test del ripristino di emergenza
ms:assetid: 04f5e747-d837-4350-9fc0-8605dbf025a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn747887(v=OCS.15)
ms:contentKeyID: 62293493
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test del ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-01-26_

Sottoporre a test la procedura documentata del ripristino di emergenza effettuando un ripristino di sistema per un server pool Lync Server 2013. Il test consente di simulare un errore hardware completo per un server e ha lo scopo di garantire la disponibilità dei dati, dei piani e delle risorse per il ripristino. Provare ad avvicendare ogni mese un campo d'azione diverso, così da sottoporre un server diverso o di un'altra attrezzatura al test.

La pianificazione in base alla quale le organizzazioni svolgono il test del ripristino di emergenza è soggetta a variazioni. È molto importante non ignorare o trascurare l'esecuzione del test del ripristino di emergenza.


Esportare in un file le impostazioni di configurazione, i criteri e la topologia di Lync Server 2013. Questo file, tra le altre cose, può essere utilizzato per ripristinare le informazioni incluse nell'archivio di gestione centrale dopo una perdita di dati conseguente a un aggiornamento, un errore hardware o altri problemi.

Importare le impostazioni di configurazione, i criteri e la topologia di Lync Server 2013 nell'archivio di gestione centrale o nel computer locale, come mostrato nel seguenti comandi:

`Import-CsConfiguration -ByteInput <Byte[]> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]`

`Import-CsConfiguration -FileName <String> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]`

Per eseguire il backup dei dati di Lync Server 2013 di produzione, procedere nel modo seguente:

  - Eseguire il backup dei database RTC e LCSLog utilizzando la procedura di backup SQL Server standard che consente di creare un dump del database in un file o in un apposito dispositivo a nastro.

  - Utilizzare applicazioni di terze parti per eseguire il backup dei dati in file o su nastro.

  - Creare un file di esportazione XML dell'intero database RTC utilizzando il cmdlet Export-CsUserData.

  - Utilizzare il backup del file system o ricorrere a terze parti per eseguire il backup del contenuto delle riunioni e dei registri di conformità.

  - Utilizzare lo strumento da riga di comando Export-CsConfiguration per effettuare il backup delle impostazioni di Lync Server 2013.

Il primo passaggio della procedura di failover prevede lo spostamento forzato di utenti dal pool di produzione al pool del ripristino di emergenza.

Lo spostamento è forzato poiché il pool di produzione non ammette il riposizionamento degli utenti.

Il processo di spostamento degli utenti di Lync Server 2013 consiste nella modifica di un attributo a un oggetto account utente e nell'aggiornamento di un record nel database SQL RTC.

Per il ripristino dei dati è possibile attenersi a due procedure.

  - Il database RTC può essere ripristinato dal dispositivo originale del dump di backup SQL Server di produzione mediante la procedura standard di ripristino di SQL Server oppure con un'utility di backup o di ripristino di terze parti.

  - I dati di contatto degli utenti possono essere ripristinati con l'utility DBIMPEXP.exe, utilizzando il file XML generato dall'esportazione di SQL Server di produzione.

Dopo il ripristino dei dati, gli utenti possono connettersi correttamente al pool Lync Server 2013 per il ripristino di emergenza e svolgere le attività consuete.

Per consentire agli utenti di stabilire una connessione con il pool Lync Server 2013 per il ripristino di emergenza, è necessario modificare i record DNS.

I client faranno riferimento al pool Lync Server 2013 di produzione mediante l'autoconfigurazione e i record DNS SRV di:

  - SRV: \_sip.\_tls.\<domain\> /CNAME: SIP.\<domain\>

  - CNAME: SIP.\<domain\> /cvc-pool-1.\<domain\>

Per agevolare il failover, il record CNAME deve essere aggiornato in modo che faccia riferimento all'FQDN DROCSPool:

  - CNAME: SIP.\<domain\> /DROCSPool.\<domain\>

  - Sip.\<domain\>

  - AV.\<domain\>

  - webconf.\<domain\>

  - OCSServices.\<domain\>

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per informazioni dettagliate sulle procedure di gestione e amministrazione, vedere <a href="lync-server-2013-backing-up-and-restoring-lync-server.md">Backup e ripristino di Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)  
[Cmdlet di backup e disponibilità elevata](https://docs.microsoft.com/en-us/powershell/module/skype/?view=skype-ps)  

#### Ulteriori risorse

[Import-CsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsConfiguration)  
[Backup e ripristino di Lync Server 2013](lync-server-2013-backing-up-and-restoring-lync-server.md)  
[Gestione di ripristino di emergenza, disponibilità elevata e servizio di backup di Lync Server 2013](lync-server-2013-managing-lync-server-disaster-recovery-high-availability-and-backup-service.md)

