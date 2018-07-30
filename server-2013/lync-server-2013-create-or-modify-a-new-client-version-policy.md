---
title: Creare o modificare un nuovo criterio delle versioni client
TOCTitle: Creare o modificare un nuovo criterio delle versioni client
ms:assetid: 4be6e449-aa82-4b46-abb1-d31281573a72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898476(v=OCS.15)
ms:contentKeyID: 52062157
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un nuovo criterio delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile utilizzare i criteri delle versioni client per specificare le versioni dei client supportate nel proprio ambiente. Il controllo delle versioni dei client può essere utile per ridurre i costi associati al supporto di più versioni dei client e consente inoltre di migliorare l'esperienza utente. In caso di interazioni tra versioni precedenti e successive dei client, infatti, è possibile limitare le funzionalità disponibili a quelle della versione precedente del client. È possibile creare o modificare i criteri delle versioni client dal Pannello di controllo di Lync Server 2013 o con Lync Server 2013 Management Shell.

## Per creare o modificare i criteri delle versioni client tramite il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client**.
    

    > [!NOTE]
    > Per impostazione predefinita, la scheda <STRONG>Criteri versione client</STRONG> è selezionata.



4.  Nella pagina **Criteri versione client** eseguire una delle operazioni seguenti:
    
      - Per creare criteri delle versioni client, fare clic su **Nuovo**, selezionare **Criteri sito**, **Criteri pool** o **Criteri utente** e quindi fare clic su **OK**.
    
      - Per modificare i criteri globali o altri criteri esistenti delle versioni client, selezionare i criteri, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  Nella pagina**Modifica criteri versione client** creare o modificare le regole come descritto in [Creare o modificare una nuova regola dei criteri delle versioni client](lync-server-2013-create-or-modify-a-new-client-version-policy-rule.md).

## Creazione o modifica dei criteri delle versioni client tramite cmdlet di Windows PowerShell

È possibile creare criteri delle versioni client tramite il cmdlet **New-CsClientVersionPolicy** e modificarli con il cmdlet **Set-CsClientVersionPolicy**. Questi cmdlet possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per creare nuovi criteri delle versioni client con ambito sito

  - Il comando seguente consente di creare nuovi criteri delle versioni client da applicare al sito Redmond. Dato che non vengono specificati ulteriori parametri, per i nuovi criteri, verranno utilizzate le impostazioni predefinite.
    
        New-CsClientVersionPolicy -Identity "site:Redmond"

## Per creare nuovi criteri delle versioni client per utente

  - Per creare un criterio per utente, utilizzare un comando simile al seguente:
    
        New-CsClientVersionPolicy -Identity "RedmondClientVersionPolicy"

Per informazioni dettagliate, vedere gli argomenti della Guida per i cmdlet [New-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientVersionPolicy) e [Set-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionPolicy).

