---
title: Configurare la messaggistica unificata in Microsoft Exchange per Lync Server 2013
TOCTitle: Configurare la messaggistica unificata in Microsoft Exchange per Lync Server 2013
ms:assetid: 07547968-c59b-4dde-ace4-9fd286933759
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398129(v=OCS.15)
ms:contentKeyID: 49299576
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la messaggistica unificata in Microsoft Exchange per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

In questo argomento viene descritto come configurare la Messaggistica unificata di Exchange in un server Microsoft Exchange Server per l'utilizzo con VoIP aziendale.


> [!NOTE]
> Negli esempi di cmdlet riportati in questo argomento viene utilizzata la sintassi per la versione Exchange 2007 di Exchange Management Shell. Se si sta eseguendo Exchange 2010 o Exchange 2013, vedere la documentazione appropriata come indicato di seguito.



## Per configurare un server in cui è in esecuzione la messaggistica unificata di Exchange Server

1.  Creare un dial plan di messaggistica unificata URI (Uniform Resource Identifier) SIP (Session Initiation Protocol) per ogni profilo località di VoIP aziendale Se si sceglie di utilizzare Exchange Management Console, creare un nuovo dial plan con l'impostazione di sicurezza **Secured (consigliata)**.
    

    > [!WARNING]
    > Se si imposta il valore dell'impostazione di sicurezza su <STRONG>SIPSecured</STRONG> per richiedere la crittografia solo per il traffico SIP, come consigliato in precedenza, tale impostazione di sicurezza in un dial plan è insufficiente se il pool Front End è configurato per richiedere la crittografia, in quanto in questo caso il pool richiede la crittografia sia per il traffico SIP che per il traffico RTP. Quando le impostazioni di sicurezza del dial plan e del pool non sono compatibili, tutte le chiamate alla Messaggistica unificata di Exchange dal pool Front End avranno esito negativo e verrà generato un errore "Impostazione di sicurezza non compatibile".

    
    Se si utilizza Exchange Management Shell, digitare quanto segue:
    
        New-UMDialPlan -Name <dial plan name> -UriType "SipName" -VoipSecurity <SIPSecured|Unsecured|Secured> -NumberOfDigitsInExtension <number of digits> -AccessTelephoneNumbers <access number in E.164 format>
    
    Per informazioni dettagliate, vedere quanto segue:
    
      - Per Office Communications Server 2007, vedere "Creazione di un dial plan di messaggistica unificata URI SIP" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268632\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268632%26clcid=0x410) e "New-UMDialplan" nella documentazione di Exchange 2007 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268666\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268666%26clcid=0x410).
    
      - Per Exchange 2010, vedere "Creazione di un dial plan di messaggistica unificata" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268674\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268674%26clcid=0x410) e "New-UMDialplan" nella documentazione di Exchange 2010 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268680\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268680%26clcid=0x410).
    
      - Per Exchange 2013, vedere l'articolo sulla messaggistica unificata all'indirizzo [http://go.microsoft.com/fwlink/?linkid=266579\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x410).
    

    > [!NOTE]
    > La scelta di <STRONG>SIPSecured</STRONG> o <STRONG>Secured</STRONG> come livello di sicurezza dipende dal fatto che il protocollo SRTP (Secure Real-Time Transport Protocol) sia attivato o disattivato per la crittografia multimediale. Per l'integrazione di Lync Server 2010 con la messaggistica unificata di Exchange, dovrebbe corrispondere al livello di crittografia impostato nella configurazione multimediale di Lync Server. La configurazione multimediale di Lync Server può essere visualizzata eseguendo il cmdlet <STRONG>Get-CsMediaConfiguration</STRONG>. Per informazioni dettagliate, vedere Get-CsMediaConfiguration nella documentazione di Lync Server Management Shell.<BR>Per informazioni dettagliate sulla scelta dell'impostazione appropriata per la protezione VoIP, vedere <A href="lync-server-2013-deployment-process-for-integrating-on-premises-unified-messaging.md">Processo di distribuzione per l'integrazione della messaggistica unificata locale con Lync Server 2013</A>.



2.  Eseguire il cmdlet seguente per ottenere il nome di dominio completo (FQDN) per ogni dial plan di messaggistica unificata:
    
    ``` 
    (Get-UMDialPlan <dialplanname>).PhoneContext  
    ```
    
    Per informazioni dettagliate, vedere quanto segue:
    
      - Per Exchange 2007, vedere "Get-UMDialplan" nella documentazione di Exchange 2007 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268678\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268678%26clcid=0x410).
    
      - Per Exchange 2010, vedere "Get-UMDialplan" nella documentazione di Exchange 2010 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268679\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268679%26clcid=0x410).
    
      - Per Exchange 2013, vedere l'articolo sulla messaggistica unificata all'indirizzo [http://go.microsoft.com/fwlink/?linkid=266579\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x410).

3.  Registrare il nome di ogni dial plan di messaggistica unificata. A seconda della versione di Exchange Server, potrebbe essere necessario utilizzare successivamente l'FQDN di ogni nome di dial plan come nome del dial plan di Lync Server corrispondente di ogni dial plan di messaggistica unificata, in modo che i nomi dei dial plan coincidano.
    

    > [!NOTE]
    > I nomi dei dial plan di Lync Server devono corrispondere ai nomi dei dial plan di messaggistica unificata solo se questi ultimi vengono eseguiti in una versione di Exchange <EM>precedente</EM> a Exchange 2010 SP1.



4.  Aggiungere il dial plan al server in cui è in esecuzione la Messaggistica unificata di Exchange come segue:
    
      - Se si sceglie di utilizzare Exchange Management Console, è possibile aggiungere il dial plan dalla scheda delle proprietà del server. Per istruzioni specifiche, vedere la documentazione del prodotto Exchange Server.
        
        Per Exchange 2007, vedere "Come aggiungere un server di messaggistica unificata a un dial plan" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268681\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268681%26clcid=0x410).
        
        Per Exchange 2010, vedere "Visualizzazione o configurazione delle proprietà di un server di messaggistica unificata" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268682\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268682%26clcid=0x410).
        
        Per Exchange 2013, vedere l'articolo sulla messaggistica unificata all'indirizzo [http://go.microsoft.com/fwlink/?linkid=266579\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x410).
    
      - Se si utilizza Exchange Management Shell, eseguire quanto segue per ogni server di messaggistica unificata di Exchange:
        
            $ums=get-umserver; 
            $dp=get-umdialplan -id <name of dial-plan created in step 1>; 
            $ums[0].DialPlans +=$dp.Identity; 
            set-umserver -instance $ums[0]
    

    > [!NOTE]
    > Prima di eseguire il passaggio seguente, verificare che per tutti gli utenti di VoIP aziendale sia stata configurata una cassetta postale di Exchange Server.<BR>Per Exchange 2007, vedere la documentazione tecnica di Exchange Server 2007 su TechNet all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268685%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=268685&amp;clcid=0x410</A>.<BR>Per Exchange 2010, vedere la documentazione tecnica di Exchange Server 2010 su TechNet all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268686%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=268686&amp;clcid=0x410</A>.<BR>Quando si specifica un criterio di cassetta postale per ogni dial plan creato nel passaggio 1, selezionare il criterio predefinito o uno dei criteri creati.



5.  Passare a \<*directory di installazione di Exchange*\>\\Scripts e quindi, se Exchange è distribuito in una singola foresta, digitare quanto segue:
    
        exchucutil.ps1
    
    In alternativa, se Exchange è distribuito in più foreste, digitare quanto segue:
    
        exchucutil.ps1 -Forest:"<forest FQDN>"
    
    dove *forest FQDN* specifica la foresta in cui è distribuito Lync Server.
    
    Se si dispone di uno o più dial plan di messaggistica unificata associati a più gateway IP, continuare con il passaggio 6. Se i dial plan sono associati ciascuno a un solo gateway IP, saltare il passaggio 6.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ricordarsi di riavviare il servizio <strong>Lync Server Front End</strong> (rtcsrv.exe) <em>dopo</em> aver eseguito exchucutil.ps1, altrimenti Lync Server non rileverà la messaggistica unificata nella topologia.</td>
    </tr>
    </tbody>
    </table>


6.  Tramite Exchange Management Shell o Exchange Management Console disabilitare le chiamate in uscita per tutti i gateway IP, tranne uno, associati a ciascuno dei dial plan.
    

    > [!NOTE]
    > Questo passaggio è necessario per garantire che le chiamate in uscita effettuate tramite il server che esegue la messaggistica unificata di Exchange Server e destinate a utenti esterni (ad esempio, come nel caso di scenari di riproduzione al telefono) attraversino correttamente il firewall aziendale.

    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Quando si seleziona il gateway IP di messaggistica unificata tramite cui consentire le chiamate in uscita, scegliere quello ritenuto più probabilmente in grado di gestire la maggior parte del traffico. Non consentire il traffico in uscita tramite un gateway IP che si connette a un pool di server Director di Lync Server. Evitare inoltre i pool in un altro sito centrale o un sito di succursale. Per impedire il passaggio delle chiamate in uscita attraverso un gateway IP, è possibile utilizzare uno dei metodi seguenti:</td>
    </tr>
    </tbody>
    </table>
    
      - Se si utilizza Exchange Management Shell, disattivare ogni gateway IP eseguendo il comando seguente:
        
            Set-UMIPGateway <gatewayname> -OutcallsAllowed $false
        
        Per Exchange 2007, vedere "Set-UMIPGateway" nella documentazione di Exchange 2007 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268687\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268687%26clcid=0x410).
        
        Per Exchange 2010, vedere "Set-UMIPGateway" nella documentazione di Exchange 2010 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268688\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268688%26clcid=0x410).
    
      - Se si utilizza Exchange Management Console, deselezionare la casella di controllo **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se il dial plan di messaggistica unificata URI SIP è associato a un solo gateway IP, non impedire le chiamate in uscita attraverso questo gateway.</td>
    </tr>
    </tbody>
    </table>


7.  Creare un operatore automatico di messaggistica unificata per ogni dial plan di Lync Server.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Non includere spazi nel nome dell'operatore automatico.</td>
    </tr>
    </tbody>
    </table>
    
        New-umautoattendant -name <auto attendant name> -umdialplan < name of dial plan created in step 1> -PilotIdentifierList <auto attendant phone number in E.164 format> -SpeechEnabled $true -Status Enabled
    
    Per informazioni dettagliate, vedere quanto segue:
    
      - Per Exchange 2007, vedere "New-UMAutoAttendan" nella documentazione di Exchange 2007 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268689\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268689%26clcid=0x410).
    
      - Per Exchange 2010, vedere "New-UMAutoAttendant" nella documentazione di Exchange 2010 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268690\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268690%26clcid=0x410).
    
    Il passaggio seguente deve essere eseguito per ogni utente dopo aver abilitato gli utenti di Lync Server per VoIP aziendale quando se ne conoscono gli URI SIP.

8.  Associare gli utenti di messaggistica unificata di Exchange (per i quali è stata configurata una cassetta postale di Exchange) al dial plan di messaggistica unificata e creare un URI SIP per ogni utente.
    

    > [!NOTE]
    > <STRONG>SIPResourceIdentifier</STRONG> nell'esempio seguente deve essere impostato sull'indirizzo SIP dell'utente di Lync Server.

    
        enable-ummailbox -id <user name> -ummailboxpolicy <name of the mailbox policy for the dial plan created in step 1> -Extensions <extension> -SIPResourceIdentifier "<user name>@<full domain name>" -PIN <user pin>
    
    Per informazioni dettagliate, vedere quanto segue:
    
      - Per Exchange 2007, vedere "Enable-UMMailbox" nella documentazione di Exchange 2007 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268691\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268691%26clcid=0x410).
    
      - Per Exchange 2010, vedere "Enable-UMMailbox" nella documentazione di Exchange 2010 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268692\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268692%26clcid=0x410).

