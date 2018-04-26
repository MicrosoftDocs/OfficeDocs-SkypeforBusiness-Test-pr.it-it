---
title: Risoluzione dei problemi relativi al Pannello di controllo di Lync Server 2013
TOCTitle: Risoluzione dei problemi relativi al Pannello di controllo di Lync Server 2013
ms:assetid: 54e7ab57-34ce-4a07-bcc9-643379eb4eb7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg195689(v=OCS.15)
ms:contentKeyID: 49300548
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Risoluzione dei problemi relativi al Pannello di controllo di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In questo argomento sono disponibili informazioni e procedure utili per risolvere i problemi di accesso al Pannello di controllo di Lync Server 2013.

## Requisiti per il browser Internet

Per utilizzare il Pannello di controllo di Lync Server è necessario che sia installato plug-in per il browser Microsoft Silverlight versione 4.0.50524.0 o versione successiva. Se Silverlight non è disponibile o è installata una versione precedente, seguire le istruzioni nel messaggio per installare la versione richiesta.


> [!NOTE]
> Gli altri requisiti del software per il Pannello di controllo di Lync Server riguardano il sistema operativo in cui è possibile installare il Pannello di controllo di Lync Server e tutti gli altri strumenti di amministrazione di Lync Server 2013. Per informazioni dettagliate, vedere <A href="lync-server-2013-server-and-tools-operating-system-support.md">Supporto del sistema operativo per server e strumenti in Lync Server 2013</A> nella documentazione relativa alla supportabilità.



Se il browser Internet impedisce l'installazione di Silverlight a causa di problematiche relative alla sicurezza, aggiungere l'URL (Uniform Resource Locator) per l'apertura del Pannello di controllo di Lync Server all'elenco dei siti attendibili. Nelle impostazioni di sicurezza di Internet Explorer, assicurarsi che l'opzione **Esegui controlli ActiveX e plug-in** sia impostata su **Attivato**. Per informazioni dettagliate vedere [http://go.microsoft.com/fwlink/?linkid=214060\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=214060%26clcid=0x410). Assicurarsi inoltre che il browser sia configurato per l'utilizzo di SSL 3.0.

Se il browser Internet è configurato per l'utilizzo di un server proxy, verificare che il browser sia configurato per il bypass del server proxy per i siti rilevati automaticamente come siti interni. In alternativa aggiungere l'indirizzo all'elenco delle eccezioni del browser nelle impostazioni di configurazione del server proxy.

## Requisiti per record DNS e certificati per l'URL di accesso amministrativo

Se è stato configurato un URL semplice per l'accesso al Pannello di controllo di Lync Server, assicurarsi di avere configurato anche il record di risorse (A) host DNS (Domain Name System) statico e il certificato necessario per utilizzare l'URL di accesso amministrativo. Se si modifica l'URL di base in qualsiasi momento, assicurarsi che la modifica venga riportata nel record DNS e nel certificato appropriati, nonché di eseguire *Enable-CsComputer* in ogni Server Director e Front End Server per registrare la modifica. Per informazioni dettagliate, vedere gli argomenti seguenti nella documentazione relativa alla pianificazione:

  - [Pianificazione degli URL semplici in Lync Server 2013](lync-server-2013-planning-for-simple-urls.md)

  - [Requisiti DNS per gli URL semplici in Lync Server 2013](lync-server-2013-dns-requirements-for-simple-urls.md)

  - [Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md)

Per istruzioni dettagliate per la configurazione dell'URL di accesso amministrativo, vedere [Modificare o configurare URL semplici in Lync Server 2013](lync-server-2013-edit-or-configure-simple-urls.md) nella documentazione relativa alla distribuzione.


> [!NOTE]
> Se nel server Web sono disponibili più schede di rete, è necessario configurare manualmente DNS per ogni scheda di rete aggiuntiva per ottenere il corretto funzionamento della risoluzione DNS.



## Requisiti di IIS (Internet Information Services)

Il Pannello di controllo di Lync Server è uno dei componenti di Lync Server 2013 che richiede Internet Information Services (IIS). In particolare, assicurarsi che siano abilitate le funzionalità di reindirizzamento HTTP e di autenticazione di Windows e che sia in esecuzione il servizio Pubblicazione sul Web (W3SVC).

## Dipendenze per il servizio Pubblicazione sul Web di Windows

Quando il servizio Pubblicazione sul Web è arrestato, non è possibile accedere al Pannello di controllo di Lync Server. È possibile riavviare il servizio tramite la console MMC (Microsoft Management Console) Servizi di Windows.

**Per avviare il servizio Pubblicazione sul Web**

1.  Accedere al computer in cui è installato il servizio Pubblicazione sul Web incluso in Internet Information Services (IIS).

2.  Fare clic sul pulsante **Start**, scegliere **Strumenti di amministrazione** e quindi **Servizi**.

3.  Fare clic con il pulsante destro del mouse su **Servizio Pubblicazione sul Web** e quindi fare clic su **Avvia**.

## Modalità del pool di applicazioni

Configurare IIS in modo che il pool di applicazioni CsManagementAppPool utilizzi l'account Servizio di rete come identità del modello di elaborazione.

## Diritti utente e autorizzazioni

È necessario accedere al Pannello di controllo di Lync Server con un account di dominio membro del gruppo CsAdministrator o con un account a cui sono stati delegati diritti utente e autorizzazioni. Non è possibile accedere al Pannello di controllo di Lync Server tramite un account computer locale. Per informazioni dettagliate sulla delega delle attività amministrative tramite il controllo di accesso basato sui ruoli, vedere [Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013](lync-server-2013-planning-for-role-based-access-control.md) nella documentazione relativa alla pianificazione.

Se si utilizza un URL semplice per accedere al Pannello di controllo di Lync Server, assicurarsi che i server Web vengano aggiunti ai gruppi RTCUniversalServerAdmins e RTCUniversalUserAdmins.

## Vedere anche

#### Concetti

[Strumenti di amministrazione di Lync Server 2013](lync-server-2013-lync-server-administrative-tools.md)

