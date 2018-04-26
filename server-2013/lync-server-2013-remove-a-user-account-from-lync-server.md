---
title: Rimuovere un account utente da Lync Server
TOCTitle: Rimuovere un account utente da Lync Server
ms:assetid: 2f512aba-e358-45ae-af58-74312ee9c514
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688008(v=OCS.15)
ms:contentKeyID: 49887498
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere un account utente da Lync Server

 

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile usare la procedura che segue per rimuovere un account utente aggiunto in precedenza in Lync Server 2013.


> [!NOTE]
> La rimozione di un utente comporterà la perdita delle impostazioni configurate per l'account utente. Se invece si desidera disabilitare temporaneamente un account utente, vedere l'argomento <A href="lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md">Disabilitare o abilitare nuovamente gli account utente per Lync Server</A>.



## Per rimuovere un account utente di Lync Server Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Cerca utenti** digitare anche solo la prima parte del nome visualizzato, nome, cognome, nome dell'account Gestione account di protezione, indirizzo SIP o URI (Uniform Resource Identifier) di linea dell'account utente da disabilitare o riabilitare e quindi fare clic su **Trova**.

5.  Nella tabella fare clic sull'account utente da rimuovere.

6.  Nel menu **Azione** selezionare **Rimuovi da Lync Server**. Verrà visualizzata una finestra di dialogo.

7.  Dalla finestra di dialogo selezionare **OK** per rimuovere l'utente.

## Rimozione di un account utente mediante i cmdlet PowerShell di Lync Server

Per rimuovere gli account utente è anche possibile usare il cmdlet Disable-CsUser, che può essere eseguito da Lync Server 2013 Management Shell o da una Windows PowerShell di una sessione remota. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Rimozione di un account utente

  - Per rimuovere un account utente, usare il cmdlet Disable-CsUser. Ad esempio:
    
        Disable-CsUser -Identity "Ken Myer"
    
    Dopo aver eseguito questo comando, non sarà più possibile riabilitare l'account e le relative impostazioni precedenti. Sarà invece necessario usare il cmdlet Enable-CsUser per creare un account completamente nuovo per Davide Garghentini.

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Disable-CsUser](disable-csuser.md).

## Vedere anche

#### Attività

[Disabilitare o abilitare nuovamente gli account utente per Lync Server](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)  

#### Ulteriori risorse

[Abilitazione e disabilitazione degli utenti per Lync Server 2013](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

