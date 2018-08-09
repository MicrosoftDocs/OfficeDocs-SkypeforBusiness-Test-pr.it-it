---
title: "Lync Server 2013: Visualizza numeri accesso per conference call"
TOCTitle: "Lync Server 2013: Visualizza numeri accesso per conference call"
ms:assetid: 41a7dfb4-0c89-4650-b61b-0e1bf875c62b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688037(v=OCS.15)
ms:contentKeyID: 49887536
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare i numeri di accesso per le conferenze telefoniche con accesso esterno

 

_**Ultima modifica dell'argomento:** 2013-02-23_

In Pannello di controllo di Lync Server 2013 vengono forniti i numeri di accesso esterno agli utenti per consentirgli di partecipare a una riunione esternamente.

## Per visualizzare i numeri di accesso esterno

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Servizi di conferenza** e quindi fare clic su **Numero di accesso esterno**.

4.  Nella pagina **Numero di accesso esterno** fare clic sul numero di accesso che si desidera visualizzare.

5.  In **Modifica** selezionare la casella di controllo **Mostra dettagli**.

## Visualizzazione dei numeri di accesso per le conferenze telefoniche con accesso esterno mediante i cmdlet di Lync Server PowerShell

I numeri di accesso per le conferenze telefoniche con accesso esterno possono anche essere visualizzati utilizzando Lync Server PowerShell e il cmdlet Get-CsDialInConferencingAccessNumber, che può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione delle informazioni di configurazione del trunking SIP

  - Per visualizzare informazioni su tutti i numeri di accesso per le conferenze telefoniche con accesso esterno, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsDialInConferencingAccessNumber
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity           : CN={20ca8dc8-5ff8-41f4-b5bb-22ba9972ae2e},
                             CN=Application Contacts,CN=RTCService=Services,
                             CN=Configuration,DC=litwareinc,DC=com
        PrimaryUri         : sip:testnumber@litwareinc.com
        DisplayName        : Test
        DisplayNumber      : 1-425-555-1019
        LineUri            : tel:+14255551019
        PrimaryLanguage    : en-US
        SecondaryLanguages : {}
        Pool               : atl-cs-001.litwareinc.com
        HostingProvider    :
        Regions            : {US}

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsDialInConferencingAccessNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsDialInConferencingAccessNumber).

