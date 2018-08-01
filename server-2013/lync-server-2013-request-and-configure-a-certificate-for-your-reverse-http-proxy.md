---
title: 'Lync Server 2013: Richiedere e configurare un certificato per il proxy inverso HTTP'
TOCTitle: Richiedere e configurare un certificato per il proxy inverso HTTP
ms:assetid: 4b70991e-5f10-40a3-b069-0b227c3a3a0a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429704(v=OCS.15)
ms:contentKeyID: 49300467
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Richiedere e configurare un certificato per il proxy inverso HTTP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È necessario installare il certificato dell'autorità di certificazione (CA) radice nel server che esegue Microsoft Forefront Threat Management Gateway 2010 o ARR di IIS per l'infrastruttura di CA che ha rilasciato i certificati server ai server interni che eseguono Microsoft Lync Server 2013.

È inoltre necessario installare un certificato server Web pubblico nel server proxy inverso. I nomi alternativi soggetto del certificato dovrebbero contenere i nomi di dominio completi (FQDN) esterni pubblicati di ogni pool che ospita gli utenti abilitati per l'accesso remoto e gli FQDN esterni di tutti i Director o pool di server Director che verranno utilizzati in tale infrastruttura Edge. Il nome alternativo soggetto deve contenere anche l'URL semplice della riunione, l'URL semplice di accesso esterno e, se si distribuiscono applicazioni mobili e si prevede di utilizzare l'individuazione automatica, l'URL del servizio di individuazione automatica esterno come illustrato nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Valore</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome soggetto</p></td>
<td><p>FQDN del pool</p></td>
<td><p>webext.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Nome alternativo soggetto</p></td>
<td><p>FQDN del pool</p></td>
<td><p>webext.contoso.com</p>

> [!IMPORTANT]  
> Il nome soggetto deve essere presente anche nel nome alternativo soggetto.

</td>
</tr>
<tr class="odd">
<td><p>Nome alternativo soggetto</p></td>
<td><p>Servizi Web del Server Director facoltativi (se è distribuito il Server Director)</p></td>
<td><p>webdirext.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Nome alternativo soggetto</p></td>
<td><p>URL semplice riunione</p>

> [!NOTE]
> Tutti gli URL semplici di riunione devono essere inclusi nel nome alternativo soggetto. Ogni dominio SIP deve avere almeno un URL semplice di riunione attiva.


</td>
<td><p>meet.contoso.com</p></td>
</tr>
<tr class="odd">
<td><p>Nome alternativo soggetto</p></td>
<td><p>URL semplice accesso esterno</p></td>
<td><p>dialin.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Nome alternativo soggetto</p></td>
<td><p>Server Office Web Apps</p></td>
<td><p>officewebapps01.contoso.com</p></td>
</tr>
<tr class="odd">
<td><p>Nome alternativo soggetto</p></td>
<td><p>URL servizio di individuazione automatica esterno</p></td>
<td><p>lyncdiscover.contoso.com</p>

> [!NOTE]
> Se si utilizza anche Microsoft Exchange Server, è inoltre necessario configurare le regole del proxy inverso per gli URL dei servizi di individuazione automatica e Web di Exchange.


</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se la distribuzione interna include più server Standard Edition o pool Front End, è necessario configurare le regole di pubblicazione Web per ogni FQDN di Web FARM esterna e sarà necessario un certificato e un listener Web per ognuno oppure ottenere un certificato con nome alternativo soggetto che contiene i nomi utilizzati da tutti i pool, assegnarlo a un listener Web e condividerlo tra più regole di pubblicazione Web.



## Creazione di una richiesta di certificato

Le richieste di certificato vengono create nel proxy inverso. La richiesta viene creata in un altro computer, ma è necessario esportare il certificato firmato con la chiave primaria e importarlo nel proxy inverso dopo averlo ricevuto dall'autorità di certificazione pubblica.


> [!NOTE]
> Una richiesta di certificato o una richiesta di firma del certificato è una richiesta a un'autorità di certificazione pubblica attendibile di convalida e firma della chiave pubblica del computer richiedente. Quando viene generato un certificato, vengono create una chiave pubblica e una chiave privata. Solo la chiave pubblica è condivisa e firmata. Come indica il nome, la chiave pubblica è resa disponibile per tutte le richieste pubbliche. La chiave pubblica può essere usata da client, server e altri richiedenti che devono scambiare informazioni in modo sicuro e convalidare l'identità di un computer. La chiave privata è invece protetta e viene usata solo dal computer che ha creato la coppia di chiavi per decrittografare i messaggi crittografati con la relativa chiave pubblica. È possibile utilizzare la chiave privata per altri scopi. Con un proxy inverso, l'uso principale è la crittografia. Un altro uso è l'autenticazione dei certificati a livello di chiave del certificato ed è limitato solo alla verifica che il richiedente disponga della chiave pubblica del computer o che il computer per cui si dispone della chiave pubblica sia effettivamente il computer che dichiara di essere.



> [!tip]  
> Se si pianificano i certificati del server perimetrale e del proxy inverso contemporaneamente, è importante tenere presente che i requisiti dei due certificati sono molto simili. Quando si configura e si richiede il certificato del server perimetrale, è consigliabile combinare i nomi soggetto alternativi del server perimetrale e del proxy inverso. È possibile usare lo stesso certificato per il proxy inverso se si esporta il certificato e la chiave privata e si copia il file esportato nel proxy inverso, quindi si importa la coppia certificato/chiave e la si assegna in base alle procedure disponibili. Fare riferimento ai requisiti dei certificati per il server perimetrale  <a href="lync-server-2013-plan-for-edge-server-certificates.md">Pianificare i certificati dei server perimetrali in Lync Server 2013</a> e del proxy inverso <a href="lync-server-2013-certificate-summary-reverse-proxy.md">Riepilogo dei certificati - proxy inverso in Lync Server 2013</a>. Assicurarsi di creare il certificato con una chiave privata esportabile. La creazione del certificato e della richiesta di certificato con una chiave privata esportabile è necessaria per i server perimetrali in pool, pertanto si tratta di una procedura normale. La Configurazione guidata certificati dello Distribuzione guidata di Lync Server per il server perimetrale consente di impostare il flag <strong>Consenti esportazione chiave privata</strong> . Una volta che la richiesta di certificato viene restituita dall'autorità di certificazione pubblica, esportare il certificato e la chiave privata. Per informazioni dettagliate su come creare ed esportare il certificato con una chiave privata, vedere la sezione relativa all'esportazione del certificato con la chiave privata per i server perimetrali di un pool nell'articolo <a href="lync-server-2013-set-up-certificates-for-the-external-edge-interface.md">Impostare i certificati per l'interfaccia perimetrale esterna per Lync Server 2013</a>. L'estensione del certificato deve essere di tipo <strong>pfx</strong>.

Per generare una richiesta di firma del certificato nel computer a cui verranno assegnati il certificato e la chiave privata, eseguire le operazioni seguenti:

**Creazione di una richiesta di firma del certificato**

1.  Aprire Microsoft Management Console (MMC), aggiungere lo snap-in Certificati e selezionare **Computer** , quindi espandere **Personale** . Per informazioni dettagliate su come creare una console dei certificati in Microsoft Management Console (MMC), vedere la pagina all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=282616](http://go.microsoft.com/fwlink/?linkid=282616).

2.  Fare clic con il pulsante destro del mouse su **Certificati** , **Tutte le attività** , **Operazioni avanzate** e infine su **Crea richiesta personalizzata** .

3.  Nella pagina **Registrazione certificato** fare clic su **Avanti** .

4.  Nella pagina **Seleziona criteri di registrazione certificato** selezionare **Continua senza criteri di registrazione** in **Richiesta personalizzata** . Fare clic su **Avanti** .

5.  Nella pagina **Richiesta personalizzata** per **Modello** selezionare **(Nessun modello) Chiave legacy** . Se non specificato diversamente dal provider del certificato, lasciare deselezionata l'opzione **Elimina estensioni predefinite** e impostare **Formato richiesta** su **PKCS \#10** . Fare clic su **Avanti** .

6.  Nella pagina **Informazioni sul certificato** fare clic su **Dettagli** e quindi su **Proprietà** .

7.  Nel campo **Nome descrittivo** della pagina **Proprietà certificato** nella scheda **Generale** digitare un nome per il certificato. Se lo si desidera, digitare una descrizione nel campo **Descrizione** . Il nome descrittivo e la descrizione vengono in genere usati dall'amministratore per identificare lo scopo del certificato, ad esempio **Listener del proxy inverso per Lync Server**.

8.  Selezionare la scheda **Soggetto** . In **Nome soggetto** per **Tipo** selezionare **Nome comune** come tipo del nome soggetto. In **Valore** digitare il nome soggetto che verrà usato per il proxy inverso, quindi fare clic su **Aggiungi** . Nell'esempio disponibile nella tabella in questo argomento, il nome soggetto è webext.contoso.com e deve essere digitato nel campo Valore in Nome soggetto.

9.  Nella scheda **Soggetto** in **Nome alternativo** selezionare **DNS** nell'elenco a discesa **Tipo** . Per ciascun nome alternativo di soggetto definito richiesto per il certificato digitare il nome di dominio completo, quindi fare clic su **Aggiungi** . Nella tabella, ad esempio, sono presenti tre nomi di soggetto alternativi: meet.contoso.com, dialin.contoso.com e lyncdiscover.contoso.com. Nel campo **Valore** digitare meet.contoso.com, quindi fare clic su **Aggiungi** . Ripetere la procedura per tutti i nomi di soggetto alternativi da definire.

10. Nella pagina **Proprietà certificato** fare clic sulla scheda **Estensioni** . In questa pagina verrà definito lo scopo della chiave crittografica in **Utilizzo chiave** e l'uso esteso della chiave in **Utilizzo chiave esteso (criteri di applicazione)** .

11. Fare clic sulla freccia **Utilizzo chiave** per visualizzare **Opzioni disponibili** . In Opzioni disponibili fare clic su **Firma digitale** , quindi su **Aggiungi** . Fare clic su **Crittografia chiave** , quindi su **Aggiungi** . Se la casella di controllo **Rendi gli utilizzi delle chiavi critici** non è selezionata, selezionarla.

12. Fare clic sulla freccia **Utilizzo chiave esteso (criteri di applicazione)** per visualizzare **Opzioni disponibili** . In Opzioni disponibili fare clic su **Autenticazione server** e quindi su **Aggiungi** . Fare clic su **Autenticazione client** e quindi su **Aggiungi** . Se la casella di controllo **Rendi gli utilizzi delle chiavi critici** è selezionata, deselezionarla. A differenza di quando si usa la casella di controllo Utilizzo chiave, che deve essere selezionata, è necessario verificare che la casella di controllo Utilizzo chiave esteso non lo sia.

13. Nella pagina **Proprietà certificato** fare clic sulla scheda **Chiave privata** . Fare clic sulla freccia **Opzioni chiave** . Per **Dimensioni chiave** selezionare **2048** nell'elenco a discesa. Se si genera questa coppia di chiavi con richiesta di firma del certificato in un computer diverso dal proxy inverso per cui è stato creato il certificato, selezionare **Consenti esportazione chiave privata** .

    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />SicurezzaNota:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>La selezione dell'opzione <strong>Consenti esportazione chiave privata</strong> è in genere consigliabile quando si dispone di più proxy inversi in una farm, in quanto il certificato e la chiave privata verranno copiati in ogni computer della farm. Se si consente l'esportazione della chiave privata, è necessario dedicare particolare attenzione al certificato e al computer in cui è stato generato. La chiave privata, se danneggiata, renderà inutile il certificato e potrà esporre il computer o i computer all'accesso esterno e ad altre vulnerabilità della sicurezza.</td>
    </tr>
    </tbody>
    </table>

14. Nella scheda **Chiave privata** fare clic sulla freccia **Tipo chiave** . Selezionare l'opzione **Exchange** .

15. Fare clic su **OK** per salvare le impostazioni della finestra **Proprietà certificato** .

16. Nella pagina **Registrazione certificato** fare clic su **Avanti** .

17. Nella pagina **Specificare il percorso in cui salvare la richiesta offline** specificare **Nome file** e **Formato file** per salvare la richiesta di firma del certificato.

18. Nel campo **Nome file** digitare un percorso e nome file per la richiesta oppure fare clic su **Sfoglia** per selezionare una posizione per il file e digitare il nome file per la richiesta.

19. In **Formato file** fare clic su **Base 64** o **Binario** . Selezionare **Base 64** , a meno che il fornitore dei certificati non abbia dato istruzioni diverse.

20. Individuare il file della richiesta salvato al passaggio precedente. Inviarlo all'autorità di certificazione pubblica.
    
    > [!IMPORTANT]  
    > Microsoft ha identificato le autorità di certificazione pubbliche che soddisfano i requisiti per le comunicazioni unificate. Un elenco è disponibile nell'articolo della Knowledge Base disponibile all'indirizzo <a href="http://go.microsoft.com/fwlink/?linkid=282625">http://go.microsoft.com/fwlink/?LinkId=282625</a>
