---
title: Assegnare criteri dial plan per utente
TOCTitle: Assegnare criteri dial plan per utente
ms:assetid: 9fea861f-7770-4cae-9b1f-2a960595bfc9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688156(v=OCS.15)
ms:contentKeyID: 49887680
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri dial plan per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Per completare la configurazione degli account per gli utenti di VoIP aziendale o per gli utenti delle conferenze telefoniche con accesso esterno, è necessario che all'utente sia assegnato un dial plan. Quando non si assegna esplicitamente un dial plan per utente esistente, gli account utente utilizzeranno automaticamente il dial plan globale oppure il dial plan a livello di sito, se disponibile. Se si desidera utilizzare il dial plan globale o il dial plan del sito per tutti gli utenti abilitati per VoIP aziendale, è possibile ignorare questa sezione.

## Per assegnare un dial plan tramite il Pannello di controllo di Lync Server 2013

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Cerca utenti** digitare tutto o solo la prima parte del nome visualizzato, del nome, del cognome, del nome dell'account SAM (Security Accounts Manager), dell'indirizzo SIP o dell'URI (Uniform Resource Identifier) di linea dell'account utente che si desidera abilitare e quindi fare clic su **Trova**.

5.  Nella tabella fare clic sull'account utente a cui si desidera assegnare un dial plan.

6.  Scegliere **Mostra dettagli** dal menu **Modifica**.

7.  Nella pagina **Modifica utente di Lync Server**, in **Telefonia**, fare clic su **VoIP aziendale**.

8.  Fare clic su **Criteri dial plan** e quindi scegliere il dial plan desiderato.

9.  Fare clic su **Commit**.

Per informazioni dettagliate sulla configurazione dei dial plan, vedere l'argomento [Configurazione dei dial plan in Lync Server 2013](lync-server-2013-configuring-dial-plans.md).

## Per assegnare un dial plan tramite Lync Server 2013 Management Shell

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per assegnare un dial plan specifico dell'utente, al prompt dei comandi eseguire quanto segue:
    
        Grant-CsDialPlan -Identity <UserIdParameter> -PolicyName <String>
    
    Ad esempio:
    
        Grant-CsDialPlan -Identity "Bob Kelly" -PolicyName DialPlanJapan
    
    In questo esempio all'utente con il nome visualizzato Davide Milano viene assegnato il dial plan denominato **DialPlanJapan**.

Per informazioni dettagliate sull'assegnazione di un dial plan utente o sull'esecuzione del cmdlet **Grant-CsDialPlan**, vedere la documentazione di [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Assegnazione di un dial plan per utente tramite i cmdlet di Windows PowerShell

È possibile assegnare dial plan per utente anche utilizzando Windows PowerShell e il cmdlet **Grant-CsdialPlan**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Assegnazione di un dial plan per utente a un singolo utente

  - Il comando seguente assegna il dial plan per utente RedmondDialPlan all'utente Ken Myer:
    
        Grant-CsDialPlan -Identity "Ken Myer" -PolicyName "RedmondDialPlan"

## Assegnazione di un dial plan per utente a più utenti

  - Questo comando assegna il dial plan per utente RedmondDialPlan a tutti gli utenti che lavorano nella città di Redmond. Per ulteriori informazioni sul parametro LdapFilter utilizzato nel comando, vedere la documentazione relativa al cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -LdapFilter "l=Redmond" | Grant-CsDialPlan -PolicyName "RedmondDialPlan"

## Annullamento dell'assegnazione di un dial plan per utente

  - Il comando seguente annulla l'assegnazione di qualsiasi dial plan per utente precedentemente assegnato a Ken Myer. Dopo l'annullamento dell'assegnazione del dial plan per utente, Ken Myer verrà gestito automaticamente mediante il dial plan globale, il dial plan del sito locale (se esistente) o il dial plan dell'ambito del servizio assegnato alla funzione di registrazione o al gateway PSTN. Un dial plan dell'ambito del servizio ha la precedenza su qualsiasi dial plan del sito, mentre un dial plan del sito ha la precedenza sul dial plan globale.
    
        Grant-CsDialPlan -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Grant-CsDialPlan](grant-csdialplan.md).

## Vedere anche

#### Ulteriori risorse

[Configurazione dei dial plan in Lync Server 2013](lync-server-2013-configuring-dial-plans.md)  
[Account utente abilitati per Lync Server 2013](lync-server-2013-user-accounts-enabled-for-lync-server.md)

