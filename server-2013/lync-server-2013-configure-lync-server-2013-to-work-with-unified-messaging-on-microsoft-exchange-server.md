---
title: "Lync Server 2013: Configura LS 2013 per uso messaggi in MS Exchange Server"
TOCTitle: Configurare Lync Server 2013 per l'utilizzo della messaggistica unificata in Microsoft Exchange Server
ms:assetid: 1098ae4d-f57f-44f3-804e-39889d9fc14e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398193(v=OCS.15)
ms:contentKeyID: 49299717
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare Lync Server 2013 per l'utilizzo della messaggistica unificata in Microsoft Exchange Server

 

_**Ultima modifica dell'argomento:** 2013-04-03_

Per questo passaggio è necessaria l'utilità di integrazione della messaggistica unificata di Exchange (OcsUmUtil.exe). Tale strumento è disponibile in Lync Server 2013 nella cartella ..\\Programmi\\File comuni\\Microsoft Lync Server 2013\\Support.

## Esecuzione dell'utilità di integrazione della messaggistica unificata di Exchange

L'utilità di integrazione della messaggistica unificata di Exchange deve essere eseguita con un account utente dotato delle caratteristiche seguenti:

  - Membro dei gruppi RTCUniversalServerAdmins e RtcUniversalUserAdmins (è inclusa l'autorizzazione per la lettura delle impostazioni di messaggistica unificata di Exchange Server)

  - Diritti utente a livello di dominio per creare oggetti contatto nel contenitore unità organizzativa (OU) specificato

L'utilità di integrazione della messaggistica unificata di Exchange consente di eseguire le attività seguenti:

  - Creazione di oggetti contatto per ogni numero di operatore automatico e di accesso del sottoscrittore che gli utenti di VoIP aziendale devono utilizzare.

  - Verifica della corrispondenza tra il nome di ogni dial plan di VoIP aziendale e il contesto telefonico del dial plan di messaggistica unificata corrispondente. Questa corrispondenza è necessaria solo se il dial plan di messaggistica unificata viene eseguito in una versione di Exchange *precedente* a Exchange 2010 Service Pack 1 (SP1).

> [!IMPORTANT]  
> Prima di eseguire l'utilità di integrazione della messaggistica unificata di Exchange, eseguire le operazioni seguenti:<ul><li><p>Creare uno o più dial plan di Messaggistica unificata di Exchange come illustrato nella documentazione relativa al prodotto Exchange.</p>
> <p>Per Microsoft Exchange Server 2010, vedere &quot;Creazione di un dial plan di messaggistica unificata&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=186177">http://go.microsoft.com/fwlink/p/?linkId=186177</a>.</p>
> <p>Per Microsoft Exchange Server 2007 Service Pack 1 (SP1), vedere &quot;Creazione di un dial plan di messaggistica unificata URI SIP&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=185771">http://go.microsoft.com/fwlink/p/?linkId=185771</a>.</p></li><li><p>Creare uno o più dial plan di Lync Server corrispondenti come illustrato in <a href="lync-server-2013-create-a-dial-plan.md">Creare un dial plan in Lync Server 2013</a>.</p>

> [!IMPORTANT]  
> Se si utilizza una versione di Exchange precedente a Microsoft Exchange Server 2010 SP1, sarà necessario immettere il nome di dominio completo (FQDN) del dial plan di messaggistica unificata SIP di Messaggistica unificata di Exchange corrispondente nel campo <strong>Nome semplice</strong> del dial plan di Lync Server 2013. Se si utilizza Microsoft Exchange Server 2010 SP1 o un Service Pack più recente, tale corrispondenza del nome del dial plan non è necessaria.</li>
> <li>Creare un operatore automatico e verificare che il numero di accesso del sottoscrittore e il numero dell'operatore automatico siano nel formato E.164.</li></ul>


## Per eseguire l'utilità di integrazione della messaggistica unificata di Exchange

1.  In un Front End Server aprire una finestra del prompt dei comandi, digitare **cd %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support** e quindi premere INVIO.

2.  Digitare **OcsUmUtil.exe** e quindi premere INVIO.

3.  Fare clic su **Carica dati** per trovare tutte le foreste trusted di Exchange.

4.  Nell'elenco **Dial plan SIP** selezionare un dial plan SIP di messaggistica unificata per cui creare gli oggetti contatto, quindi fare clic su **Aggiungi** .

5.  Nella casella **Contatto** accettare l'unità organizzativa predefinita oppure fare clic su **Sfoglia** per avviare **Selezione unità organizzativa** . Nella casella **Selezione unità organizzativa** è possibile selezionare un'unità organizzativa e fare clic su **OK** oppure è possibile fare clic su **Crea nuova unità organizzativa** per creare una nuova unità organizzativa nella radice o in qualsiasi altra unità organizzativa del dominio, ad esempio OU=Account speciali RTC,DC=fourthcoffee,DC=com", e quindi fare clic su **OK** .
    

    > [!NOTE]
    > Il nome distinto dell'unità organizzativa selezionata o creata verrà visualizzato nella casella <STRONG>Unità organizzativa</STRONG> .



6.  Nella casella **Nome** accettare il nome predefinito del dial plan o digitare un nuovo nome visualizzato per l'oggetto contatto che si sta creando.
    

    > [!NOTE]
    > Se ad esempio si sta creando un oggetto contatto accesso sottoscrittore, è possibile denominarlo semplicemente Accesso sottoscrittore.



7.  Nella casella **Indirizzo SIP** accettare l'indirizzo SIP predefinito o digitarne uno nuovo.
    

    > [!NOTE]
    > Se si digita un nuovo indirizzo SIP, tale indirizzo deve iniziare con <STRONG>SIP:</STRONG> , ovvero "SIP:" comprensivo dei due punti.



8.  Nell'elenco **Server o pool** selezionare il server Standard Edition o il pool Front End in cui deve essere abilitato l'oggetto contatto.
    

    > [!NOTE]
    > Il pool selezionato preferibilmente deve coincidere con quello in cui sono distribuiti gli utenti abilitati per VoIP aziendale e la messaggistica unificata di Exchange.



9.  Nell'elenco **Numero di telefono** selezionare **Specifica numero di telefono** o **Usa questo numero pilota dalla messaggistica unificata di Exchange** , quindi immettere un numero di telefono.

10. Nell'elenco **Tipo di contatto** selezionare il tipo di contatto che si desidera creare e quindi fare clic su **OK** .

11. Ripetere i passaggi da 1 a 10 per gli ulteriori oggetti contatto da creare.
    

    > [!NOTE]
    > È consigliabile creare almeno un contatto per ogni operatore automatico. Se si desidera disporre dell'accesso esterno, è inoltre necessario un contatto Accesso sottoscrittore e specificare numeri DID (Direct Inward Dial).



Per verificare che gli oggetti contatto siano stati creati correttamente, aprire Utenti e computer di Active Directory e selezionare l'unità organizzativa in cui sono stati creati gli oggetti. Gli oggetti contatto dovrebbero essere visualizzati nel riquadro dei dettagli.

