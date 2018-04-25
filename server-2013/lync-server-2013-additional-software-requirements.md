---
title: 'Lync Server 2013: Requisiti software aggiuntivi'
TOCTitle: Requisiti software aggiuntivi
ms:assetid: 87b318e3-03ae-41f7-af5e-29bb294f6af0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398686(v=OCS.15)
ms:contentKeyID: 49301219
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti software aggiuntivi per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-20_

Oltre ai requisiti hardware e del sistema operativo per le piattaforme server, Lync Server 2013 richiede l'installazione di software aggiuntivo nei server distribuiti.


> [!NOTE]
> Per informazioni dettagliate sui requisiti della piattaforma per i server che eseguono Lync Server, vedere <A href="lync-server-2013-server-hardware-platforms.md">Piattaforme hardware server per Lync Server 2013</A> e <A href="lync-server-2013-server-and-tools-operating-system-support.md">Supporto del sistema operativo per server e strumenti in Lync Server 2013</A>. Per informazioni dettagliate sui requisiti di sistema per i dispositivi e i computer client, vedere <A href="lync-server-2013-planning-for-clients-and-devices.md">Pianificazione dei client e dei dispositivi in Lync Server 2013</A> nella documentazione relativa alla pianificazione. Per informazioni dettagliate sui requisiti software per gli strumenti di amministrazione, vedere <A href="lync-server-2013-administrative-tools-software-requirements.md">Requisiti software degli strumenti di amministrazione in Lync Server 2013</A>.



## Software aggiuntivo necessario per tutti i ruoli del server interni

In questa sezione è elencato il software necessario in tutti i ruoli del server interni, ovvero tutti i ruoli del server Lync Server con l'eccezione del server perimetrale. I requisiti per i server perimetrali e i pool di server perimetrali sono elencati di seguito in questo argomento nella sezione **Software aggiuntivo per i server perimetrali**.

## Windows PowerShell 3.0

In ciascun server che esegue Lync Server 2013 deve essere installata la versione corretta di Windows PowerShell 3.0. Per ulteriori informazioni, vedere [Installazione di Windows PowerShell 3.0 per Lync Server 2013](lync-server-2013-installing-windows-powershell-3-0.md).

## Microsoft .NET Framework 4.5

Lync Server richiede Microsoft .NET Framework 4.5 in tutti i ruoli del server interni e in qualsiasi computer in cui verranno eseguiti gli strumenti di amministrazione di Lync Server o Microsoft Lync Server 2013, Strumento di pianificazione. Per Lync Server 2013 è necessario installare manualmente l'edizione a 64 bit di Microsoft .NET Framework 4.5 nel server prima di installare Lync Server 2013. Per eseguire l'installazione manualmente, scaricare Microsoft .NET 4.5 Framework dall'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=268529](http://go.microsoft.com/fwlink/p/?linkid=268529)

## Installazione di Microsoft .NET Framework 4.5 su server che eseguono Windows Server 2012

Quando si installa Microsoft .NET Framework 4.5 su server che eseguiranno Lync Server 2013 e Windows Server 2012, è necessario eseguire un ulteriore passaggio. Dopo l'installazione di .NET Framework 4.5, utilizzare Server Manager per installare il programma di attivazione di HTTP.

**Installazione del programma di attivazione di HTTP di .NET 4.5 su Windows Server 2012**

1.  Dal menu **Start** , fare clic su **Programmi** , selezionare **Strumenti di amministrazione** e fare clic su **Server Manager** .

2.  In Server Manager, sotto **Riepilogo funzionalità** , selezionare **Aggiungi funzionalità** .

3.  Espandere **.NET Framework 4.5** .

4.  Se deselezionato, selezionare **Attivazione WCF** , quindi selezionare **Attivazione HTTP** .

5.  Fare clic su **Avanti** e completare i passaggi dell'installazione.

## Windows Identity Foundation

**Windows Identity Foundation** in Lync Server 2013 richiede l'installazione di Windows Identity Foundation per supportare gli scenari di autenticazione da server a server. Windows Server 2008 R2 e Windows Server 2012 richiedono procedure differenti per l'installazione di Windows Identify Foundation. Selezionare il proprio sistema operativo server dall'elenco seguente:

  - Windows Server 2008 R2   Per Windows Server 2008 R2, controllare se è già stato installato nel computer. A questo scopo, andare a **Installazione applicazioni**, **Visualizza aggiornamenti installati** e in **Windows** cercare la voce **Windows Identity Foundation (KB974405)**. Per informazioni dettagliate sull'installazione di Windows Identity Foundation, vedere la pagina all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=204657](http://go.microsoft.com/fwlink/p/?linkid=204657).

  - Windows Server 2012   Per Windows Server 2012, utilizzare **Server Manager** per installare Windows Identity Foundation. Nell' **Aggiunta guidata ruoli e funzionalità** di Server Manager selezionare **Funzionalità** . Selezionare **Windows Identity Foundation 3.5** dall'elenco. Fare clic su **Avanti** e quindi su **Installa** .

## Software aggiuntivo per tutti i Front End Server e server Standard Edition

In tutti i server Standard Edition e Front End Server deve inoltre essere in esecuzione Internet Information Services (IIS) con determinati moduli. In tutti i server Standard Edition e Front End Server in cui sono distribuite le funzionalità di conferenza, applicazione Parcheggio di chiamata, Annuncio o Response Group deve anche essere in esecuzione Runtime formato Windows Media.

## Internet Information Services (IIS)

Nei server Standard Edition e Front End Server deve essere in esecuzione Internet Information Services (IIS) con i moduli seguenti.

  - Contenuto statico

  - Documento predefinito

  - Errori HTTP

  - ASP.NET

  - Estendibilità .NET

  - Estensioni ISAPI (Internet Server API)

  - Filtri ISAPI

  - Registrazione HTTP

  - Strumenti di registrazione

  - Funzionalità di traccia

  - Autenticazione di Windows

  - Filtro richieste

  - Compressione contenuto statico

  - Compressione contenuto dinamico

  - Console di gestione IIS

  - Strumenti e script di gestione IIS

  - Autenticazione anonima (modulo installato per impostazione predefinita durante l'installazione di IIS)

  - Autenticazione mapping certificati client

## Runtime formato Windows Media e Windows Desktop Experience

**Windows Desktop Experience** In tutti i Front End Server e Standard Edition in cui devono essere installate le funzionalità di conferenza è necessario installare Runtime formato Windows Media che, ad eccezione di Windows Server 2012, è installato come parte di Windows Desktop Experience. Windows Server 2012 richiede Microsoft Media Foundation. Runtime formato Windows Media è obbligatorio per l'esecuzione di file Windows Media Audio (con estensione wma) riprodotti dalle applicazioni Parcheggio di chiamata, Annuncio e Response Group per gli annunci e la musica.

È consigliabile installare Windows Desktop Experience prima di installare Lync Server 2013. Se Lync Server 2013 non trova questo software nel server, viene richiesto di installarlo e sarà quindi necessario riavviare il server per completare l'installazione.

## Software aggiuntivo per Front End Server e server Standard Edition eseguiti su Windows Server 2012

Front End Server richiede .NET 3.5, che non è installato per impostazione predefinita su Windows Server 2012. Per installarlo, inserire il supporto di installazione di Windows Server 2012 nell'unità D, e digitare:

    Add-WindowsFeature RSAT-ADDS, Web-Server, Web-Static-Content, Web-Default-Doc, Web-Http-Errors, Web-Asp-Net, Web-Net-Ext, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Http-Logging, Web-Log-Libraries, Web-Request-Monitor, Web-Http-Tracing, Web-Basic-Auth, Web-Windows-Auth, Web-Client-Auth, Web-Filtering, Web-Stat-Compression, Web-Dyn-Compression, NET-WCF-HTTP-Activation45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Scripting-Tools, Web-Mgmt-Compat, Desktop-Experience, Telnet-Client, BITS -Source D:\sources\sxs

Per informazioni dettagliate sull'installazione di .NET 3.5 nei server che eseguono Windows Server 2012, vedere le considerazioni sulla distribuzione di Microsoft .NET Framework 3.5 all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=275032>.

## Software aggiuntivo per i server Director

Nei server Director deve essere in esecuzione Internet Information Services (IIS) con i moduli seguenti:

  - Contenuto statico

  - Documento predefinito

  - Errori HTTP

  - ASP.NET

  - Estendibilità .NET

  - Estensioni ISAPI (Internet Server API)

  - Filtri ISAPI

  - Registrazione HTTP

  - Strumenti di registrazione

  - Funzionalità di traccia

  - Autenticazione di Windows

  - Filtro richieste

  - Compressione contenuto statico

  - Console di gestione IIS

  - Strumenti e script di gestione IIS

  - Autenticazione anonima (modulo installato per impostazione predefinita durante l'installazione di IIS)

  - Autenticazione mapping certificati client

## Software aggiuntivo per Front End Server della chat persistente

I Front End Server della chat persistente devono eseguire il servizio Accodamento messaggi (MSMQ), che è un componente di Windows Server.

Per informazioni sull'abilitazione di MSMQ, [fare clic qui](http://technet.microsoft.com/it-it/library/cc771474.aspx)

## Software aggiuntivo per i server perimetrali

Per i server perimetrali è richiesto il software seguente:

  - In ciascun server che esegue Lync Server 2013 deve essere installata la versione corretta di Windows PowerShell 3.0. Per ulteriori informazioni, vedere [Installazione di Windows PowerShell 3.0 per Lync Server 2013](lync-server-2013-installing-windows-powershell-3-0.md).

  - Lync Server richiede Microsoft .NET Framework 4.5. Per Lync Server 2013 installato in Windows Server 2008 R2, è necessario installare manualmente l'edizione a 64 bit di Microsoft .NET Framework 4.5 nel server prima di installare Lync Server 2013. Per installare manualmente questa edizione, scaricare Microsoft .NET 4.5 Framework dall'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=268529](http://go.microsoft.com/fwlink/p/?linkid=268529)

  - **Windows Identity Foundation** in Lync Server 2013 richiede l'installazione di Windows Identity Foundation per supportare gli scenari di autenticazione da server a server. Windows Server 2008 R2 e Windows Server 2012 richiedono procedure differenti per l'installazione di Windows Identify Foundation. Selezionare il proprio sistema operativo server dall'elenco seguente:
    
      - Windows Server 2008 R2   Per Windows Server 2008 R2, controllare se è già stato installato nel computer. A questo scopo, andare a **Installazione applicazioni**, **Visualizza aggiornamenti installati** e in **Windows** cercare la voce **Windows Identity Foundation (KB974405)**. Per informazioni dettagliate sull'installazione di Windows Identity Foundation, vedere la pagina all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=204657](http://go.microsoft.com/fwlink/p/?linkid=204657).
    
      - Windows Server 2012   Per Windows Server 2012, utilizzare **Server Manager** per installare Windows Identity Foundation. Nell' **Aggiunta guidata ruoli e funzionalità** di Server Manager selezionare **Funzionalità** . Selezionare **Windows Identity Foundation 3.5** dall'elenco. Fare clic su **Avanti** e quindi su **Installa** .

## Non installare provider LSP (Layered Service Provider) nei server multimediali

Non installare software client Microsoft Internet Security and Acceleration (ISA) Server o altro software LSP (Layered Service Provider) Winsock in Front End Server o Mediation Server autonomi. L'installazione di software di questo tipo può comportare un peggioramento delle prestazioni del traffico multimediale.

## Vedere anche

#### Concetti

[Requisiti software degli strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-software-requirements.md)

