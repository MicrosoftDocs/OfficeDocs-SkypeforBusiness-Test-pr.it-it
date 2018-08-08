---
title: "Lync Server 2013: Crea/modifica configurazione delle versioni client"
TOCTitle: "Lync Server 2013: Crea/modifica configurazione delle versioni client"
ms:assetid: 4e6faffd-a36f-40f1-8734-78d84b7df921
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898477(v=OCS.15)
ms:contentKeyID: 52062147
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una raccolta di impostazioni di configurazione delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le impostazioni di configurazione delle versioni client vengono utilizzate per attivare o disattivare il controllo delle versioni client. La configurazione globale delle versioni client viene installata con Lync Server e utilizzata per attivare o disattivare il controllo delle versioni client per l'intera distribuzione server. È inoltre possibile configurare le impostazioni di configurazione delle versioni client per singoli siti. Per la creazione o la modifica di queste impostazioni è possibile utilizzare il Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell.


> [!NOTE]
> Poiché gli utenti anonimi non sono associati ad alcun utente, sito o servizio, sono interessati solo dai criteri a livello globale.



## Per creare o modificare le impostazioni di configurazione delle versioni client tramite il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione versione client**.

4.  Nella pagina **Configurazione versione client** eseguire le operazioni seguenti:
    
      - Per creare una nuova configurazione, fare clic su **Nuovo**, selezionare un sito, fare clic su **OK** e aggiornare le impostazioni.
    
      - Per modificare una configurazione, selezionarla, fare clic su **Modifica** e su **Mostra dettagli**, quindi apportare le modifiche alle impostazioni.

## Creazione o modifica delle impostazioni di configurazione delle versioni client tramite cmdlet di Windows PowerShell

È possibile creare impostazioni di configurazione delle versioni client tramite il cmdlet **New-CsClientVersionConfiguration** e modificarle con il cmdlet **Set-CsClientVersionConfiguration**. Questi cmdlet possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per creare una nuova raccolta delle impostazioni di configurazione delle versioni client

  - Il comando seguente consente di creare una nuova raccolta di impostazioni di configurazione delle versioni client da applicare al sito Redmond. In questo esempio, il controllo delle versioni client è disabilitato per il sito Redmond.
    
        New-CsClientVersionConfiguration -Identity "site:Redmond" -Enabled $False

## Per abilitare il controllo delle versioni client per un sito

  - Questo comando consente di abilitare il controllo delle versioni client per il sito Redmond.
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -Enabled $True

## Per disabilitare il controllo delle versioni client in tutta l'organizzazione

  - L'esempio seguente consente di disabilitare il controllo delle versioni client per tutte le impostazioni di configurazione delle versioni client attualmente in uso nell'organizzazione.
    
        Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration  -Enabled $False

Per informazioni dettagliate, vedere l'argomento della Guida per i cmdlet [New-CsClientVersionConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientVersionConfiguration) e [Set-CsClientVersionConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionConfiguration).

