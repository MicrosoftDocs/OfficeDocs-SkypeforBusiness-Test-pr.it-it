---
title: 'Lync Server 2013: Pianificazione delle distribuzioni ibride di Lync Server'
TOCTitle: Pianificazione delle distribuzioni ibride di Lync Server
ms:assetid: f8b3d240-bc2e-42c9-acf8-d532d641a14c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205403(v=OCS.15)
ms:contentKeyID: 49302536
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione delle distribuzioni ibride di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-08-19_

Durante la pianificazione di una distribuzione ibrida, prendere in considerazione i requisiti seguenti per gli utenti e per l'infrastruttura di rete.

## Requisiti dell'infrastruttura

Per implementare e configurare una distribuzione ibrida di Lync Server 2013, è necessario che gli elementi seguenti siano disponibili nell'ambiente.

  - Tenant di Office 365 con Lync Online abilitato.

  - Server di Active Directory Federation Services (AD FS) in locale o utilizzando Microsoft Azure. Per ulteriori informazioni su AD FS, vedere [Active Directory Federation Services 2.0 RTW - Italiano](http://go.microsoft.com/fwlink/p/?linkid=393795) oppure [Configurare Active Directory Federation Services per Windows Azure Pack](http://go.microsoft.com/fwlink/p/?linkid=522475).

  - Distribuzione locale di Lync Server 2013 o Lync Server 2010 con gli aggiornamenti cumulativi per Lync Server 2010 di marzo 2013 o successivi.

  - Strumenti amministrativi di Lync Server 2013.

  - Sincronizzazione directory. Per informazioni dettagliate su Sincronizzazione directory, vedere [Gestione ibrida delle identità](http://go.microsoft.com/fwlink/?linkid=231010).

## Supporto per client Lync

Le caratteristiche supportate nei client Lync, oltre che le caratteristiche disponibili negli ambienti locali e online, presentano alcune differenze. Prima di decidere dove si desidera ospitare gli utenti dell'organizzazione, è possibile visualizzare il supporto client per le diverse configurazioni di Lync Server. I seguenti client sono supportati con Skype for Business online in una distribuzione ibrida di Lync:

  - Lync 2010

  - Lync 2013

  - app Windows Store Lync

  - Lync Web App

  - Lync Mobile

  - Lync per Mac 2011

  - Lync Room System

  - Lync Basic 2013

Per informazioni dettagliate sul supporto client, vedere gli argomenti seguenti:

  - [Client per Lync Online](http://go.microsoft.com/fwlink/?linkid=281902)

  - [Tabelle di confronto dei client per Lync Server 2013](lync-server-2013-desktop-client-comparison-tables.md)

  - [Tabelle di confronto dei client mobili per Lync Server 2013](lync-server-2013-mobile-client-comparison-tables.md)

## Requisiti della topologia

Per configurare la distribuzione di Lync Server 2013 per l'utilizzo ibrido con Skype for Business online, sarà necessario disporre di una delle topologie supportate seguenti:

  - Microsoft Office Communications Server 2007 R2 con Lync Server 2013 in locale. È necessario che Lync Server 2013 con server perimetrale federativo e il server dell'hop successivo dal server perimetrale federativo eseguano Lync Server 2013 e che sia stato distribuito un Archivio di gestione centrale. Il server perimetrale e il pool devono essere distribuiti in locale.
    
    > [!important]  
    > Nonostante la topologia sia supportata, alcune funzionalità potrebbero essere limitate. È ad esempio possibile che le informazioni sulla presenza tra gli utenti di Microsoft Lync Online e gli utenti di Office Communications Server 2007 R2 in locale non funzionino nel modo previsto.

  - Microsoft Lync Server 2010 con aggiornamenti cumulativi per Lync Server 2010 di marzo 2013 (o aggiornamenti successivi) e gli strumenti amministrativi di Lync Server 2013 installati in locale. È necessario che il server perimetrale federativo e il server dell'hop successivo dal server perimetrale federativo eseguano Microsoft Lync Server 2010 con gli aggiornamenti cumulativi più recenti di marzo 2013 (o successivi) o Lync Server 2013.
    
    > [!important]  
    > Gli strumenti amministrativi di Lync Server 2013 devono essere installati in un server separato che può accedere e connettersi alla distribuzione esistente di Lync Server 2010. Il cmdlet Move-CsUser che consente di spostare utenti dalla distribuzione locale a Lync Online deve essere eseguito dagli strumenti amministrativi di Lync Server 2013 connessi alla distribuzione locale.

  - Una distribuzione di Lync Server 2013 con tutti i server che eseguono Lync Server 2013.

Per ulteriori informazioni sulle topologie supportate, vedere [Topologie supportate in Lync Server 2013](lync-server-2013-supported-topologies.md) e il documento relativo alle [topologie di riferimento di Lync Server 2013 per le distribuzioni aziendali ibride](http://go.microsoft.com/fwlink/p/?linkid=398709).

Per informazioni sulla risoluzione dei problemi relativi alle distribuzioni ibride e alla connessione di PowerShell a Lync Online, vedere l' [articolo corrispondente](http://go.microsoft.com/fwlink/p/?linkid=306718).

## Requisiti per gli elenchi di domini consentiti e bloccati della federazione

L'elenco dei domini consentiti include domini per cui è stato configurato un nome di dominio completo Edge di partner. Questi domini vengono a volte definiti *server partner consentiti* o *partner di federazione diretta* . È necessario comprendere la differenza tra federazione aperta e federazione chiusa, definite *individuazione del partner* ed *elenco di domini partner consentiti* , rispettivamente, nelle distribuzioni in locale.

Per configurare correttamente una distribuzione ibrida, è necessario soddisfare i requisiti seguenti:

  - La corrispondenza dei domini deve essere configurata in modo identico per la distribuzione in locale e per il tenant di Office 365. Se l'individuazione del partner è abilitata nella distribuzione in locale, sarà necessario configurare la federazione aperta per il tenant online. Se l'individuazione del partner non è abilitata, sarà necessario configurare la federazione chiusa per il tenant online.

  - L'elenco dei domini bloccati nella distribuzione in locale deve corrispondere esattamente all'elenco dei domini bloccati per il tenant online.

  - L'elenco dei domini consentiti nella distribuzione in locale deve corrispondere esattamente all'elenco dei domini consentiti per il tenant online.

  - La federazione deve essere abilitata per le comunicazioni esterne per il tenant online, che viene configurato tramite il Pannello di controllo di Lync Online.

## Impostazioni DNS

Quando si creano record SRV DNS per distribuzioni ibride, i record, \_sipfederationtls.\_tcp.\<dominio\> e \_sip.\_tls.\<dominio\>, devono fare riferimento al proxy di accesso locale.

## Considerazioni sul firewall

I computer presenti in rete devono essere in grado di eseguire ricerche DNS Internet standard. Se questi computer possono raggiungere siti Internet standard, la rete soddisferà questo requisito.

In base alla posizione del centro dati di Microsoft Online Services, è necessario configurare anche i dispositivi firewall della rete per accettare connessioni basate sui nomi di dominio jolly (ad esempio, tutto il traffico da \*.outlook.com). Se i firewall dell'organizzazione non supportano configurazioni con nomi jolly, sarà necessario determinare manualmente gli intervalli di indirizzi IP che si desidera consentire e le porte specificate.

Fare riferimento all'argomento della Guida [URL e intervalli di indirizzi IP per Office 365](http://go.microsoft.com/fwlink/?linkid=252942).

## Requisiti relative a porte e protocolli

Oltre ai requisiti relativi alle porte per la comunicazione interna di Lync Server 2013, è necessario configurare anche le porte seguenti.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo/Porta</th>
<th>Applicazioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 443</p></td>
<td><p>Aperta in ingresso</p><ul><li><p>Active Directory Federation Services (ruolo del server federativo)</p>
<p>Per ulteriori informazioni, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=281899">Informazioni sui servizi ruolo di ADFS</a>.</p></li><li><p>Active Directory Federation Services (ruolo del server proxy)</p></li><li><p>Portale di Microsoft Online Services</p></li><li><p>Portale aziendale</p></li><li><p>Outlook Web App</p></li><li><p>Client Lync (comunicazioni verso Lync Online da Lync Server in locale)</p></li></ul></td>
</tr>
<tr class="even">
<td><p>TCP 80 e 443</p></td>
<td><p>Aperta in ingresso</p><ul><li><p>Strumento di sincronizzazione della directory dei Microsoft Online Services</p></li></ul></td>
</tr>
<tr class="odd">
<td><p>TCP 5061</p></td>
<td><p>Aperta in ingresso/uscita sul server perimetrale</p></td>
</tr>
<tr class="even">
<td><p>PSOM/TLS 443</p></td>
<td><p>Aperta in ingresso/uscita per sessioni di condivisione dati</p></td>
</tr>
<tr class="odd">
<td><p>STUN/TCP 443</p></td>
<td><p>Aperta in ingresso/uscita per sessioni di condivisione audio, video e di applicazioni</p></td>
</tr>
<tr class="even">
<td><p>STUN/UDP 3478</p></td>
<td><p>Aperta in ingresso/uscita per sessioni audio e video</p></td>
</tr>
<tr class="odd">
<td><p>RTP/TCP 50000-59999</p></td>
<td><p>Aperta in uscita per sessioni audio e video</p></td>
</tr>
<tr class="even">
<td><p>TCP 443</p></td>
<td><p>Aperta in ingresso</p><ul><li><p>Active Directory Federation Services (ruolo del server federativo)</p>
<p>Per ulteriori informazioni, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=281899">Informazioni sui servizi ruolo di ADFS</a>.</p></li><li><p>Active Directory Federation Services (ruolo del server proxy)</p></li><li><p>Portale di Microsoft Online Services</p></li><li><p>Portale aziendale</p></li><li><p>Outlook Web App</p></li><li><p>Client Lync (comunicazioni verso Lync Online da Lync Server in locale)</p></li></ul></td>
</tr>
<tr class="odd">
<td><p>TCP 80 e 443</p></td>
<td><p>Aperta in ingresso</p><ul><li><p>Strumento di sincronizzazione della directory dei Microsoft Online Services</p></li></ul></td>
</tr>
<tr class="even">
<td><p>TCP 5061</p></td>
<td><p>Aperta in ingresso/uscita sul server perimetrale</p></td>
</tr>
<tr class="odd">
<td><p>PSOM/TLS 443</p></td>
<td><p>Aperta in ingresso/uscita per sessioni di condivisione dati</p></td>
</tr>
<tr class="even">
<td><p>STUN/TCP 443</p></td>
<td><p>Aperta in ingresso/uscita per sessioni di condivisione audio, video e di applicazioni</p></td>
</tr>
<tr class="odd">
<td><p>STUN/UDP 3478</p></td>
<td><p>Aperta in ingresso/uscita per sessioni audio e video</p></td>
</tr>
<tr class="even">
<td><p>RTP/TCP 50000-59999</p></td>
<td><p>Aperta in uscita per sessioni audio e video</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se è necessaria la federazione con partner che eseguono Office Communications Server 2007, sarà necessario aprire in ingresso/in uscita delle porte 50000-59999 RTP/UDP e RTP/TCP. Per ulteriori informazioni sui requisiti relativi al firewall A/V, vedere, <A href="lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md">Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013</A>. Per ulteriori informazioni su porte e protocolli, vedere <A href="lync-server-2013-port-summary-scaled-consolidated-edge-with-hardware-load-balancers.md">Riepilogo delle porte - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013</A>.



## Account e dati utente

In una distribuzione ibrida di Lync Server 2013, è necessario innanzitutto creare nella distribuzione in locale qualsiasi utente che si desidera ospitare in Lync Online, in modo che l'account utente venga creato in Servizi di dominio Active Directory. Sarà quindi possibile spostare l'utente in Skype for Business online, in modo da spostare l'elenco di contatti dell'utente.

Quando si sincronizzano gli account utente tra le distribuzioni di Lync locale e di Lync Online con ADFS e Dirsync, è necessario sincronizzare gli account di Active Directory per tutti gli utenti Lync nell'organizzazione tra le distribuzioni di Lync in locale e online, anche se gli utenti non vengono spostati in Lync Online. Se gli utenti non vengono sincronizzati, la comunicazione tra utenti locali e online nell'organizzazione potrebbe non funzionare come previsto.

> [!important]  
> Se l'utente viene creato utilizzando il portale online per Office 365, l'account utente non verrà sincronizzato con Active Directory in locale e l'utente non esisterà in Active Directory in locale. Se sono già stati creati utenti in Lync Online e si desidera impostare una configurazione ibrida con Lync Server in locale, vedere <a href="lync-server-2013-moving-users-from-lync-online-to-lync-on-premises.md">Spostare gli utenti da Lync Online a Lync in locale in Lync Server 2013</a>.

Durante la pianificazione di una distribuzione ibrida, è inoltre necessario prendere in considerazione le problematiche seguenti correlate agli utenti.

  - **Contatti utente**   Per gli utenti di Lync Online sono consentiti al massimo 250 contatti. Eventuali contatti oltre tale numero verranno rimossi dall'elenco di contatti dell'utente quando l'account viene spostato in Lync Online.

  - **Messaggistica istantanea e presenza** La migrazione di elenchi di contatti ed elenchi di controllo di accesso viene eseguita insieme alla migrazione dell'account utente.

  - **Dati per le conferenze, contenuto della riunione e riunioni pianificate** La migrazione di questi contenuto non viene eseguita insieme alla migrazione dell'account utente. Dopo la migrazione degli account a Lync Online, gli utenti dovranno ripianificare le riunioni.

## Criteri e caratteristiche relative agli utenti

  - In un ambiente ibrido di Lync Server 2013 è possibile abilitare gli utenti per la messaggistica istantanea, comunicazione vocale e riunioni in locale oppure online, ma non contemporaneamente.

  - **Client Lync** È possibile che, dopo lo spostamento a Lync Online, per alcuni utenti sia necessaria una nuova versione del client. Per Office Communications Server 2007 R2 è necessario spostare gli utenti nel pool di Lync Server 2013 prima della migrazione a Lync Online.
    
    Per ulteriori informazioni sul supporto client, vedere [Client per Lync Online](http://go.microsoft.com/fwlink/p/?linkid=281902) e [Client di Lync supportati e configurazioni delle porte di rete](http://go.microsoft.com/fwlink/p/?linkid=281901).

  - **Criteri e configurazione locali (non utente)** Per i criteri online e locali sono necessarie configurazioni separate. Non è possibile impostare criteri globali applicabili a entrambi.

