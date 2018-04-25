---
title: Visualizzare lo stato dei servizi in esecuzione in un computer in Lync Server 2013
TOCTitle: Visualizzare lo stato dei servizi in esecuzione in un computer in Lync Server 2013
ms:assetid: f41918e7-4c02-431e-840a-88a1f36ae499
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182606(v=OCS.15)
ms:contentKeyID: 49302471
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare lo stato dei servizi in esecuzione in un computer in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile utilizzare Pannello di controllo di Lync Server 2013 per visualizzare tutti i servizi in esecuzione in un computer specifico nella topologia di Lync Server ed esaminare lo stato di ogni servizio.

## Per visualizzare lo stato dei servizi in esecuzione in un computer

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Topologia**.

4.  Nella pagina **Stato** ordinare l'elenco oppure effettuare una ricerca per trovare il computer desiderato e fare clic sul nome del computer.

5.  Effettuare una delle operazioni seguenti:
    
      - Per visualizzare lo stato più recente dei servizi in esecuzione sul computer, fare clic su **Ottieni stato servizio**.
    
      - Per visualizzare un elenco di servizi specifici in esecuzione sul computer e lo stato di ogni servizio, fare clic su **Proprietà** e quindi su **Chiudi** per tornare all'elenco.

## Visualizzazione dello stato del servizio mediante i cmdlet Lync Server Management Shell

È inoltre possibile visualizzare lo stato del servizio utilizzando Lync Server Management Shell e il cmdlet **Get-CsWindowsService**. È possibile eseguire il cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare lo stato del servizio

  - Per visualizzare lo stato del servizio in un computer, digitare un comando simile al seguente in Lync Server Management Shell, quindi premere INVIO:
    
        Get-CsWindowsService -ComputerName atl-cs-001.litwareinc.com | Select-Object RoleName, Status
    
    Il comando restituisce informazioni simili a quelle riportate di seguito:
    
        RoleName                                  Status
        --------                                  ------
        {W3SVC}                                   Running
        {CentralManagement}                       Running
        {ClsAgent}                                Running
        {Registrar, UserServer, EdgeServer}       Running
        {ApplicationServer}                       Running
        {ConferencingServer}                      Running
        {MediationServer}                         Running

Per informazioni dettagliate, vedere [Get-CsWindowsService](get-cswindowsservice.md).

## Vedere anche

#### Ulteriori risorse

[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

