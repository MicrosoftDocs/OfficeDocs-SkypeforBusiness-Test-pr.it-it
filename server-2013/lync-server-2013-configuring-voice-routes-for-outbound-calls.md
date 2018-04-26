---
title: 'Lync Server 2013: Configurazione di route vocali per le chiamate in uscita'
TOCTitle: Configurazione di route vocali per le chiamate in uscita
ms:assetid: 3c182cdd-7a4a-4a9d-bdac-4199f0abd947
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425890(v=OCS.15)
ms:contentKeyID: 49300261
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di route vocali per le chiamate in uscita in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Una route vocale di Lync Server 2013 associa i numeri di telefono di destinazione a uno o più gateway PSTN (Public Switched Telephone Network) o trunk SIP e a uno o più record di utilizzo PSTN.

**Per visualizzare le route vocali tramite il Pannello di controllo di Lync Server**

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Fare clic su **Routing vocale** .

3.  Fare clic su **Route** .

4.  Fare doppio clic su una route vocale nell'elenco per visualizzare altre proprietà oppure selezionare la route e fare clic su **Modifica** . Quindi fare clic su **Mostra dettagli** .
    

    > [!NOTE]
    > È possibile visualizzare informazioni dettagliate per una sola route per volta.



**Per visualizzare le route vocali tramite Windows PowerShell**

  - Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.Le route vocali possono essere visualizzate con Windows PowerShell e il cmdlet **Get-CsVoiceRoute**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).
    
    Per visualizzare tutte le informazioni sulle route vocali, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsVoiceRoute
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity          : global
        Priority          : -1
        Description       :
        NumberPattern     : ^(\+1[0-9]{10})$
        PstnUsages        : {}
        PstnGatewayList   : {}
        Name              : global
        SuppressCallerId  :
        AlternateCallerId :


> [!NOTE]
> Per informazioni dettagliate, vedere <A href="lync-server-2013-voice-routes.md">Route vocali in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Argomenti della sezione

  - [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md)

  - [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md)

## Vedere anche

#### Ulteriori risorse

[Gestione del routing vocale in Lync Server 2013](lync-server-2013-managing-voice-routing.md)

