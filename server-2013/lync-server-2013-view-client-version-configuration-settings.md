---
title: Visualizzare le impostazioni di configurazione delle versioni client
TOCTitle: Visualizzare le impostazioni di configurazione delle versioni client
ms:assetid: c72df4e6-a889-4cb6-86f7-8334d7774c6e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ923062(v=OCS.15)
ms:contentKeyID: 52062262
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le impostazioni di configurazione delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le impostazioni di configurazione della versione client vengono utilizzate per attivare o disattivare il controllo della versione client. La configurazione globale della versione client viene installata con Lync Server 2013 e utilizzata per attivare o disattivare il controllo della versione client per l'intera distribuzione server. Se la configurazione globale è abilitata, tutti i criteri relativi alla versione client disponibili verranno applicati quando gli utenti tentano l'accesso. È possibile visualizzare le impostazioni della configurazione della versione client dal Pannello di controllo di Lync Server 2013 o da Lync Server 2013 Management Shell.


> [!NOTE]
> Poiché gli utenti anonimi non sono associati ad alcun utente, sito o servizio, sono interessati solo dai criteri a livello globale.



## Per visualizzare le impostazioni della configurazione della versione client dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione versione client**.

4.  Fare doppio clic sul nome della configurazione della versione client che si desidera visualizzare.

## Visualizzazione delle impostazioni della configurazione della versione client utilizzando i cmdlet di Windows PowerShell

È possibile visualizzare le impostazioni della configurazione della versione client utilizzando il cmdlet **Get-CsClientVersionConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare le informazioni sulla configurazione della versione client

  - Per visualizzare informazioni su tutte le impostazioni della configurazione della versione client, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsClientVersionConfiguration
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity      : Global
        DefaultAction : Allow
        DefaultURL    :
        Enabled       : True

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Get-CsClientVersionConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClientVersionConfiguration).

