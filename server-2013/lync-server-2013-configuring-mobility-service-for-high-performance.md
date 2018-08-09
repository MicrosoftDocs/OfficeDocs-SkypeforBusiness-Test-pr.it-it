---
title: "Lync Server 2013: Configura servizio dispositivi mobili per prestaz. elevate"
TOCTitle: "Lync Server 2013: Configura servizio dispositivi mobili per prestaz. elevate"
ms:assetid: c2b8aadb-cffb-49f0-ba7a-e8541a1ff475
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690042(v=OCS.15)
ms:contentKeyID: 49301875
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del servizio per dispositivi mobili per ottenere prestazioni elevate

 

_**Ultima modifica dell'argomento:** 2013-02-17_

Quando si installa Lync Server 2013 Mobility Service in Internet Information Services (IIS) 7.5, il relativo programma di installazione configura alcune impostazioni per le prestazioni nel Front End Server. È consigliabile utilizzare IIS 7.5 per i dispositivi mobili. Se si utilizza IIS 7.0 in Windows Server 2008, è necessario configurare queste impostazioni manualmente. Le impostazioni influiscono sul numero massimo di richieste utente simultanee e il numero massimo di thread consentiti per il servizio per dispositivi mobili.

Le impostazioni per le prestazioni sono le seguenti:

  - Il valore **maxConcurrentThreadsPerCPU** viene impostato su zero (0).

  - Il valore **maxConcurrentRequestsPerCPU** viene impostato su zero (0).

  - Il modello di processo ASP.NET viene impostato su AutoConfig (solo per IIS 7.5).

  - Il limite di coda HTTP.sys viene impostato su 1.000 per impostazione predefinita.

Se si utilizza IIS 7.0, è consigliabile installare l'aggiornamento disponibile tramite l'articolo 2290617 della Microsoft Knowledge Base "FIX: Un hotfix è disponibile per consentire la configurazione di alcune proprietà ASP.NET per ogni pool di applicazioni in IIS 7.0" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x410) in modo da poter applicare le modifiche solo per il servizio per dispositivi mobili senza effetti su altri servizi Web.

La procedura seguente descrive come modificare il numero massimo di richieste simultanee e thread ASP.NET in IIS 7.0 se non si installa l'aggiornamento reso disponibile tramite l'articolo 2290617 della Knowledge Base. Anche se non si installa questo aggiornamento, è comunque possibile fare riferimento alla documentazione disponibile nell'articolo per applicare alcune modifiche solo ai pool di applicazioni di IIS interni ed esterni per la mobilità. In questo caso, si utilizza un file di configurazione separato per le impostazioni ASP.NET.

> [!IMPORTANT]  
> Se si utilizza la procedura seguente per modificare i valori massimi, le modifiche influiscono su tutti i pool di applicazioni IIS.

Per informazioni dettagliate sulla configurazione di queste impostazioni, vedere [http://go.microsoft.com/fwlink/?linkid=234537\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=234537%26clcid=0x410).

## Per modificare il numero massimo di richieste simultanee e thread

1.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui**.

2.  Nella casella **Esegui** digitare il comando seguente:
    
        notepad %SystemRoot%\Microsoft.NET\Framework64\v2.0.50727\Aspnet.config

3.  Fare clic su **OK**.

4.  Aggiungere o sostituire l'elemento \<system.web\> seguente come elemento figlio dell'elemento \<configuration\> nel file Aspnet.config:
    
        <system.web>
        <applicationPool maxConcurrentRequestsPerCPU="<#>" maxConcurrentThreadsPerCPU="0" requestQueueLimit="5000"/>
        </system.web>
    
    dove \# corrisponde a 0 per rimuovere il limite o al nuovo numero, come descritto più indietro in questa sezione.

5.  Salvare il file Aspnet.config e chiudere il Blocco note.

