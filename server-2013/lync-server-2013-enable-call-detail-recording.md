---
title: Abilitare la registrazione dettagli chiamata
TOCTitle: Abilitare la registrazione dettagli chiamata
ms:assetid: 3b28e432-596f-45a5-a070-577d6fa748d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520980(v=OCS.15)
ms:contentKeyID: 49300247
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare la registrazione dettagli chiamata

 

_**Ultima modifica dell'argomento:** 2013-02-23_

La funzionalità di registrazione dettagli chiamata (CDR) registra le informazioni di utilizzo e di diagnostica per le attività peer-to-peer, tra cui la messaggistica istantanea, le chiamate VoIP (Voice over Internet Protocol), la condivisione applicazioni, il trasferimento file e le riunioni. I dati di utilizzo possono essere utilizzati per calcolare il rendimento dell'investimento, mentre i dati di diagnostica possono aiutare a risolvere problemi relativi alle attività peer-to-peer e alle riunioni.

Utilizzare la procedura seguente per abilitare la registrazione dettagli chiamata per l'intera organizzazione o per ogni sito dell'organizzazione.


> [!NOTE]
> Per abilitare la registrazione dettagli chiamata, è necessario configurare il monitoraggio e un database di monitoraggio. Per informazioni dettagliate, vedere <A href="lync-server-2013-deploying-monitoring.md">Distribuzione del monitoraggio in Lync Server 2013</A>.



## Per abilitare la funzionalità di registrazione dettagli chiamata mediante il Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Monitoraggio e archiviazione** e quindi su **Registrazione dettagli chiamata**.

4.  Nella pagina **Registrazione dettagli chiamata** fare clic sul sito appropriato nella tabella, su **Azione** e quindi su **Abilita registrazione dettagli chiamata**.
    

    > [!NOTE]
    > La funzionalità di registrazione dettagli chiamata è abilitata per impostazione predefinita.



## Per abilitare la funzionalità di registrazione dettagli chiamata mediante i cmdlet di Lync Server Management Shell

La funzionalità può essere abilitata anche mediante Windows PowerShell e il cmdlet **Set-CsCdrConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare la funzionalità CR per una sola postazione

  - Per abilitare la funzionalità di registrazione dettaglia chiamata, impostare il parametro EnableCDR su True ($True).
    
        Set-CsCdrConfiguration -Identity "site:Redmond" -EnableCDR $True

## Per disabilitare la funzionalità CDR per una sola postazione

  - Per disabilitare la funzionalità di registrazione dettaglia chiamata, impostare il parametro EnableCDR su False ($False). Questa impostazione non disinstalla il monitoraggio, ma interrompe la raccolta e l'archiviazione dei dati CDR.
    
        Set-CsCdrConfiguration -Identity "site:Redmond" -EnableCDR $False

## Per abilitare la funzionalità CDR in più postazioni con un solo comando

  - Questo comando abilita la funzionalità CDR per tutte le impostazioni di configurazione CDR attualmente in uso nell'organizzazione.
    
        Get-CsCdrConfiguration | Set-CsCdrConfiguration "site:Redmond" -EnableCDR $True

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsCdrConfiguration](set-cscdrconfiguration.md).

## Vedere anche

#### Ulteriori risorse

[Pianificazione del monitoraggio in Lync Server 2013](lync-server-2013-planning-for-monitoring.md)  
[Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md)

