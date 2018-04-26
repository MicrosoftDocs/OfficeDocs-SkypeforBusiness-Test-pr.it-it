---
title: 'Lync Server 2013: Abilitare gli utenti per VoIP aziendale'
TOCTitle: Abilitare gli utenti per VoIP aziendale
ms:assetid: f252b23b-9641-4160-aa81-bf06dc2eced3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413011(v=OCS.15)
ms:contentKeyID: 49302450
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare gli utenti per VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Dopo l'installazione dei file per uno o più Mediation Server, configurare il routing delle chiamate in uscita e, facoltativamente, la distribuzione di una o più caratteristiche VoIP aziendale avanzate. Utilizzare le procedure seguenti per consentire a un utente di effettuare chiamate tramite VoIP aziendale:


> [!NOTE]
> Solo la prima delle procedure seguenti può essere eseguita utilizzando Pannello di controllo di Lync Server. Per le altre procedure, è possibile utilizzare solo Lync Server Management Shell.



  - Abilitare l'account utente per VoIP aziendale.

  - (Facoltativo) Assegnare all'account utente criteri vocali specifici dell'utente.

  - (Facoltativo) Assegnare all'account utente un dial plan specifico dell'utente.

## Per abilitare un account utente per VoIP aziendale

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti** .

4.  Nella casella **Cerca utenti** digitare anche solo la prima parte del nome visualizzato, nome, cognome, nome dell'account Gestione account di protezione, indirizzo SIP o URI (Uniform Resource Identifier) di linea dell'account utente da abilitare e quindi fare clic su **Trova** .

5.  Nella tabella fare clic sull'account utente che si desidera abilitare per VoIP aziendale.

6.  Scegliere **Mostra dettagli** dal menu **Modifica** .

7.  Nella pagina **Modifica utente Lync Server** , in **Telefonia** , fare clic su **VoIP aziendale** .

8.  Fare clic su **URI linea** e quindi digitare un numero di telefono normalizzato univoco, ad esempio tel:+14255550200.

9.  Fare clic su **Commit** .

Per completare l'abilitazione di un utente per VoIP aziendale, verificare che all'utente siano assegnati un dial plan e criteri vocali globali (assegnati per impostazione predefinita) o specifici dell'utente.

Per impostazione predefinita, tutti gli utenti vengono assegnati a criteri vocali e dial plan globali. Se nel sito principale dell'utente esistono criteri vocali o un dial plan a livello di sito, i criteri del sito verranno applicati automaticamente all'utente. Per applicare criteri vocali o un dial plan per utente, è necessario eseguire i cmdlet **Grant-CsVoicePolicy** e **Grant-CsDialPlan**. Per informazioni dettagliate, vedere la documentazione di [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Assegnazione di criteri vocali

I criteri vocali globali e a livello di sito vengono assegnati automaticamente a tutti gli account utente abilitati per VoIP aziendale. È inoltre possibile creare criteri vocali applicabili a utenti o gruppi specifici. Questi criteri per utente devono essere assegnati esplicitamente agli utenti o ai gruppi. Se si desidera utilizzare i criteri vocali globali o a livello di sito per tutti gli utenti abilitati per VoIP aziendale, è possibile ignorare questa sezione e passare alla sezione Assegnazione di dial plan più avanti in questo argomento.

## Per assegnare criteri vocali specifici dell'utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per assegnare criteri vocali specifici già esistenti, eseguire quanto segue al prompt dei comandi:
    
        Grant-CsVoicePolicy -Identity <UserIdParameter> -PolicyName <String>
    
    Ad esempio:
    
        Grant-CsVoicePolicy -Identity "Bob Kelly" -PolicyName VoicePolicyJapan
    
    In questo esempio all'utente con nome visualizzato Davide Milano vengono assegnati i criteri vocali denominati **VoicePolicyJapan**.

Per informazioni dettagliate sull'assegnazione di criteri vocali specifici dell'utente o sull'esecuzione del cmdlet **Grant-CsVoicePolicy** , vedere la documentazione di [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Assegnazione di dial plan

Per completare la configurazione degli account utente per gli utenti di VoIP aziendale o delle conferenze telefoniche con accesso esterno, è necessario assegnare un dial plan all'utente. Gli account utente utilizzeranno automaticamente il dial plan globale oppure, se disponibile, il dial plan a livello di sito se non si assegna esplicitamente un dial plan per utente. Se si desidera utilizzare il dial plan globale o a livello di sito per tutti gli utenti abilitati per VoIP aziendale, è possibile ignorare questa sezione.

## Per assegnare un dial plan

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per assegnare un dial plan specifico dell'utente, eseguire quanto segue al prompt dei comandi:
    
        Grant-CsDialPlan -Identity <UserIdParameter> -PolicyName <String>
    
    Ad esempio:
    
        Grant-CsDialPlan -Identity "Bob Kelly" -PolicyName DialPlanJapan
    
    In questo esempio all'utente con nome visualizzato Davide Milano viene assegnato il dial plan **DialPlanJapan**.

Per informazioni dettagliate sull'assegnazione di criteri vocali specifici dell'utente o sull'esecuzione del cmdlet **Grant-CsDialPlan** , vedere la documentazione di [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Vedere anche

#### Attività

[Disabilitare un utente per VoIP aziendale](lync-server-2013-disable-a-user-for-enterprise-voice.md)

