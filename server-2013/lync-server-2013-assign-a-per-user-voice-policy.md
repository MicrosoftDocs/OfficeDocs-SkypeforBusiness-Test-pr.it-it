---
title: Assegnare criteri vocali per utente
TOCTitle: Assegnare criteri vocali per utente
ms:assetid: 9ee47ee7-1030-43b8-a4dc-bf685ea24659
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688155(v=OCS.15)
ms:contentKeyID: 49887677
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri vocali per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I criteri vocali globali e a livello di sito vengono automaticamente assegnati a tutti gli account utente di Lync Server 2013 abilitati per il VoIP aziendale. È inoltre possibile assegnare i criteri vocali a utenti specifici mediante il Pannello di controllo di Lync Server 2013 o la Lync Server 2013 Management Shell. Usare le procedure descritte in questo argomento per assegnare in modo esplicito criteri per utente agli utenti di Lync Server.

## Per assegnare un criterio vocale specifico dell'utente mediante il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti** e quindi cercare l'account utente da configurare.

4.  Nella tabella in cui sono elencati i risultati di ricerca, fare clic sull'account utente, scegliere **Modifica** e quindi **Mostra dettagli**.

5.  In **Modifica utente di Lync Server**, in **Criteri vocali**, selezionare i criteri utente da applicare.
    

    > [!NOTE]
    > Le impostazioni <STRONG>&lt;automatiche&gt;</STRONG> applicano le impostazioni predefinite del server o dei criteri globali.



## Per assegnare un criterio vocale specifico dell'utente mediante la Lync Server Management Shell

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per assegnare un criterio vocale esistente a un utente, eseguire quanto segue al prompt dei comandi:
    
        Grant-CsVoicePolicy -Identity <UserIdParameter> -PolicyName <String>
    
    Esempio:
    
        Grant-CsVoicePolicy -Identity "Bob Kelly" -PolicyName VoicePolicyJapan
    
    In questo esempio, all'utente con il nome visualizzato Davide Milano è assegnato il criterio vocale con nome **VoicePolicyJapan**.

Per dettagli sull'assegnazione di un criterio vocale specifico dell'utente o sull'esecuzione del cmdlet **Grant-CsVoicePolicy**, vedere la documentazione [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Assegnazione di un criterio vocale per utente mediante i cmdlet di Windows PowerShell

I criteri vocali per utente possono anche essere assegnati mediante Windows PowerShell e il cmdlet **Grant-CsVoicePolicy**. Questo cmdlet può essere eseguito dalla Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Assegnazione di un criterio vocale per utente a un singolo utente

  - Il comando seguente assegna il criterio vocale per utente RedmondVoicePolicy all'utente Ken Myer.
    
        Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

## Assegnazione di un criterio vocale per utente a più utenti

  - Questo comando assegnare il criterio vocale per utente FinanceVoicePolicy a tutti gli utenti con account nell'unità organizzativa Finance in Active Directory. Per ulteriori informazioni nel parametro OU usato in questo comando, vedere la documentazione relativa al cmdlet [Get-CsUser](get-csuser.md).
    
        Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com" | Grant-CsVoicePolicy -PolicyName "FinanceVoicePolicy"

## Annullamento dell'assegnazione di un criterio vocale per utente

  - Il comando seguente annulla l'assegnazione di qualsiasi criterio vocale per utente precedentemente assegnato a Ken Myer. Dopo aver annullato l'assegnazione del criterio vocale per utente, Ken Myer verrà automaticamente gestito mediante i criteri globali oppure, se esistente, i criteri a livello di sito locale. I criteri a livello di sito hanno precedenza sui criteri globali.
    
        Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Grant-CsVoicePolicy](grant-csvoicepolicy.md).

## Vedere anche

#### Attività

[Disabilitare un utente per VoIP aziendale](lync-server-2013-disable-a-user-for-enterprise-voice.md)  

#### Ulteriori risorse

[Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md)

