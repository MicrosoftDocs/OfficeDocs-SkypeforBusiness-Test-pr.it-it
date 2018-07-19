---
title: Abilitare o disabilitare il controllo delle versioni client
TOCTitle: Abilitare o disabilitare il controllo delle versioni client
ms:assetid: 33a98cb9-a979-4bb6-afb2-512f601d7ac5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898475(v=OCS.15)
ms:contentKeyID: 52062127
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare il controllo delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le impostazioni di configurazione della versione client vengono utilizzate per attivare o disattivare il controllo della versione client, globalmente o per siti specifici. La configurazione globale della versione client viene installata con Lync Server 2013 e utilizzata per attivare o disattivare il controllo della versione client per l'intera distribuzione server. Se la configurazione globale è abilitata, tutti i criteri relativi alla versione client disponibili verranno applicati quando gli utenti tentano l'accesso. Se non si desidera che venga eseguito il controllo della versione client, è possibile disabilitare la configurazione globale della versione client. È possibile abilitare o disabilitare la versione client dal Pannello di controllo di Lync Server 2013 o da Lync Server 2013 Management Shell.


> [!NOTE]
> Poiché gli utenti anonimi non sono associati ad alcun utente, sito o servizio, sono interessati solo dai criteri a livello globale.



## Per abilitare o disabilitare la versione client utilizzando Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione versione client**.

4.  Eseguire le operazioni seguenti:
    
      - Per abilitare o disabilitare globalmente la versione client, fare doppio clic sulla configurazione **Globale**, quindi modificare le impostazioni.
    
      - Per abilitare o disabilitare la versione client per un sito specifico, fare clic su **Nuovo**, selezionare un sito, fare clic su **OK** e quindi modificare le impostazioni per il sito.

## Abilitazione o disabilitazione della versione client utilizzando i cmdlet Windows PowerShell

È possibile abilitare o disabilitare la versione client utilizzando il cmdlet **Set-CsClientVersionConfiguration** che può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare la versione client

  - È possibile abilitare la versione client impostando la proprietà **Enabled** su True ($True).
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -Enabled $True

## Per disabilitare la versione client

  - È possibile disabilitare la versione client impostando la proprietà **Enabled** su False ($False).
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -Enabled $True

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Set-CsClientVersionConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionConfiguration).

