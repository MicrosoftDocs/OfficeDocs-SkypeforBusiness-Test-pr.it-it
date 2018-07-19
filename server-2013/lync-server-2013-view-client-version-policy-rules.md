---
title: Visualizzare le regole dei criteri delle versioni client
TOCTitle: Visualizzare le regole dei criteri delle versioni client
ms:assetid: f3a0215f-f72f-4e9b-a07b-25858dc4203a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ923060(v=OCS.15)
ms:contentKeyID: 52062481
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le regole dei criteri delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Un criterio versione client è costituito da un set di regole relative ai criteri versione client. Tali regole definiscono le azioni da eseguire quando gli utenti tentano di effettuare l'accesso con client specifici e determinate versioni di client. È possibile visualizzare le regole dei criteri versione client da Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell.

## Per visualizzare le regole dei criteri versione client tramite Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Criteri versione client**.

4.  Nella pagina **Criteri versione client** fare doppio clic su un criterio versione client da visualizzare.

5.  Le regole vengono visualizzate nella pagina **Modifica Criteri versione client**. Per visualizzare le informazioni dettagliate per una regola, selezionare la regola, quindi fare clic su **Mostra dettagli**.

## Visualizzazione delle regole relative ai criteri versione client tramite i cmdlet Windows PowerShell

È possibile visualizzare le regole relative ai criteri versione client tramite Lync Server Management Shell e il cmdlet **Get-CsClientVersionPolicyRule**. Tale cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare le regole relative ai criteri versione client

  - Per visualizzare le regole relative ai criteri versione client, digitare il comando seguente in Lync Server Management Shell, quindi premere INVIO:
    
        Get-CsClientVersionPolicyRule
    
    Verranno restituite informazioni analoghe alle seguenti per ogni regola configurata:
    
        Identity          : Global/2336c611-a243-4c5d-994b-eea8a524d0e4
        Priority          : 0
        RuleId            : 2336c611-a243-4c5d-994b-eea8a524d0e4
        Description       :
        Action            : Block
        ActionUrl         :
        MajorVersion      : 1
        MinorVersion      : 3
        BuildNumber       :
        QfeNumber         :
        UserAgent         : RTC
        UserAgentFullName :
        Enabled           : True
        CompareOp         : LEQ

Per informazioni dettagliate, vedere l'argomento della guida relativo al cmdlet [Get-CsClientVersionPolicyRule](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClientVersionPolicyRule).

