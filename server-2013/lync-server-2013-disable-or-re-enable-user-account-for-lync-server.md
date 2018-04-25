---
title: Disabilitare o abilitare nuovamente gli account utente per Lync Server
TOCTitle: Disabilitare o abilitare nuovamente gli account utente per Lync Server
ms:assetid: 12497d00-f665-4a97-be68-854c5a8be4fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429696(v=OCS.15)
ms:contentKeyID: 49299734
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disabilitare o abilitare nuovamente gli account utente per Lync Server

 

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile eseguire la procedura seguente per disabilitare un account utente precedentemente abilitato in Lync Server 2013 senza perdere le impostazioni di Lync Server configurate per l'account utente. Dal momento che le impostazioni dell'account utente di Lync Server non vanno perdute, è possibile riabilitare un account utente abilitato in precedenza senza doverlo riconfigurare.

## Per disabilitare o abilitare di nuovo un account utente abilitato in precedenza per Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Cerca utenti** digitare tutto o solo la prima parte del nome visualizzato, del nome, del cognome, del nome di account SAM (Security Accounts Manager), dell'indirizzo SIP o dell'URI (Uniform Resource Identifier) linea dell'account utente che si desidera disabilitare o abilitare di nuovo e quindi fare clic su **Trova**.

5.  Nella tabella fare clic sull'account utente che si desidera disabilitare o abilitare di nuovo.

6.  Dal menu **Azione** scegliere uno dei comandi seguenti:
    
      - Per disabilitare temporaneamente l'account utente per Lync Server 2013, scegliere **Disabilita temporaneamente per Lync Server**.
    
      - Per abilitare l'account utente per Lync Server 2013, scegliere **Riabilita per Lync Server**.

## Disabilitazione e riabilitazione di un account utente mediante i cmdlet di Windows PowerShell

Gli account utente possono anche essere disabilitati temporaneamente e riabilitati in un secondo momento utilizzando il cmdlet **Set-CsUser**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Disabilitazione di un account utente

  - Per disabilitare temporaneamente un account utente, impostare il valore della proprietà Enabled su False ($False), ad esempio:
    
        Set-CsUser -Identity "Ken Myer" -Enabled $False

## Riabilitazione di un account utente

  - Per riabilitare un account utente, impostare il valore della proprietà Enabled su True ($True), ad esempio:
    
        Set-CsUser -Identity "Ken Myer" -Enabled $True

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Set-CsUser](set-csuser.md).

## Vedere anche

#### Attività

[Aggiungere e abilitare un account utente per Lync Server](lync-server-2013-add-and-enable-user-account-for-lync-server.md)  

#### Ulteriori risorse

[Abilitazione e disabilitazione degli utenti per Lync Server 2013](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

