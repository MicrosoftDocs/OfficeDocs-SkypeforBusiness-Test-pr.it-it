---
title: Visualizzare informazioni sulle regole di aggiornamento dispositivi
TOCTitle: Visualizzare informazioni sulle regole di aggiornamento dispositivi
ms:assetid: d6677ca4-024b-4816-8511-8d7630788107
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994077(v=OCS.15)
ms:contentKeyID: 52062448
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare informazioni sulle regole di aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile visualizzare i dettagli delle regole di aggiornamento dispositivi già importate, inclusi tipo, modello e marchio dei dispositivi a cui si applica l'aggiornamento, versione e tipo di aggiornamento e impostazioni locali e pool per l'aggiornamento. Le informazioni sono disponibili per tutte le regole di aggiornamento dei dispositivi importate: con approvazione in sospeso, distribuite (approvate), richiamate (ripristinate) e che si è deciso di non utilizzare (reimpostate). Accedere a queste informazioni dal Pannello di controllo di Lync Server o da Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate su come importare, approvare, reimpostare, ripristinare e rimuovere le regole, vedere gli argomenti elencati in <A href="lync-server-2013-device-update-rules.md">Regole di aggiornamento dispositivi in Lync Server 2013</A>.



## Per visualizzare le regole di aggiornamento dei dispositivi utilizzando il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Aggiornamento dispositivi**. Le regole importate vengono visualizzate nella pagina **Aggiornamento dispositivi**.

## Visualizzazione di regole di aggiornamento dispositivi tramite i cmdlet di Windows PowerShell

Le informazioni dettagliate su tutte le regole di aggiornamento dispositivi possono essere visualizzate anche con Windows PowerShell e il cmdlet **Get-CsDeviceUpdateRule**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



## Per visualizzare tutte le regole di aggiornamento dispositivi

  - Il comando seguente restituisce informazioni su tutte le regole di aggiornamento dispositivi configurate per l'utilizzo nell'organizzazione:
    
        Get-CsDeviceUpdateRule
    
    Per ogni regola di aggiornamento dispositivi il comando restituisce informazioni analoghe alle seguenti:
    
        Identity        : Service:WebServer:pool0.vdomain.com/2de8cbf6-9441-4f61-b755-1e4bef1effde
        Id              : 2de8cbf6-9441-4f61-b755-1e4bef1effde
        DeviceType      : UCPhone
        Brand           : Microsoft
        Model           : CPE
        Revision        : A
        Locale          : ENU
        UpdateType      : CPE
        ApprovedVersion :
        RestoreVersion  :
        PendingVersion  : 4.0.7577.4066

## Per visualizzare tutte le regole di aggiornamento dispositivi in un server Web specifico

  - Per visualizzare le regole di aggiornamento dispositivi in un computer specifico, utilizzare il parametro Filter seguito dall'identità del server e dal carattere jolly (\*). Ad esempio:
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*"

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Get-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsDeviceUpdateRule).

