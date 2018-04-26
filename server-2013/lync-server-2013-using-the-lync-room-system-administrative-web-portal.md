---
title: 'Lync Server 2013: Uso del portale Web amministrativo di Lync Room System'
TOCTitle: Uso del portale Web amministrativo di Lync Room System
ms:assetid: c387b2a3-3e42-4642-af72-88126ed2820f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn743660(v=OCS.15)
ms:contentKeyID: 62268996
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso del portale Web amministrativo di Lync Room System in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-11-10_

Dopo aver distribuito Lync Room System (LRS) nel server, è possibile controllare lo stato di tutte le sale conferenze LRS eseguendo l'accesso al portale Web amministrativo di LRS da un browser.

## Accesso

1.  Passare all'URL seguente:
    
    https://\<server-front-end\>/lrs

2.  Immettere le credenziali per l'account LRSSupport o per un account aggiunto al gruppo di sicurezza LRSSupportAdminGroup.

![Schermata di accesso al portale di amministrazione di Lync Room System](images/Dn436326.050bcf70-2f3b-46b2-9b96-ebd12679b713(OCS.15).png "Schermata di accesso al portale di amministrazione di Lync Room System")

## Pagina di riepilogo del portale Web amministrativo di LRS

La pagina di riepilogo offre le informazioni seguenti per tutte le sale conferenze LRS distribuite nel server:

  - **Tag**   Nome personalizzato assegnato alla sala dall'amministratore. È possibile impostare il tag nel portale facendo clic sul nome della sala.

  - **Health**   Lo stato di integrità della sala, derivato dallo stato Aggregate Health indicato nella sezione Health della pagina Room Settings.

  - **Next Meeting**   Data e ora pianificate per la riunione successiva.

  - **LRS Version, Manufacturer, Model**   Questi valori sono preimpostati in LRS. A seconda del produttore, questi campi potrebbero essere vuoti.

  - **Last Refresh**   Visualizza data e ora dell'ultimo aggiornamento della pagina Web.

![Visualizzazione di riepilogo del portale di amministrazione di Lync Room System](images/Dn743660.f829ce90-dd95-4725-bd94-6870c5dcf046(OCS.15).png "Visualizzazione di riepilogo del portale di amministrazione di Lync Room System")

## Informazioni sulla sala conferenze LRS

Nella sezione Room Info del portale è possibile visualizzare e configurare le singole sale LRS. Sono disponibili quattro sezioni: Settings, Details, Logging e Health.

## Settings

Nella sezione Impostazioni è possibile impostare la password, il tag della sala e i livelli di volume predefiniti. Se si configurano queste impostazioni, le modifiche vengono replicate solo dopo il riavvio della console LRS.

![Impostazioni della sala nel portale di amministrazione di Lync Room System](images/Dn743660.ab162e19-41ac-4991-9b2a-92575aa53eda(OCS.15).png "Impostazioni della sala nel portale di amministrazione di Lync Room System")

## Dettagli

Nella sezione Details è disponibile un riepilogo di sola lettura delle impostazioni della sala LRS che include data/ora dell'ultimo aggiornamento, prossima riunione, ultimi aggiornamenti, manutenzione e calibratura, impostazioni predefinite per altoparlanti/microfono/suoneria, versione, URI SIP, numero di schermi e dettagli su ogni schermo, stato e attività.

![Visualizzazione dettagliata del portale di amministrazione di Lync Room System](images/Dn743660.2958bbba-db74-4670-a920-87fdfb2fc22d(OCS.15).png "Visualizzazione dettagliata del portale di amministrazione di Lync Room System")

## Logging

La sezione Logging può essere usata per la raccolta dei log in remoto e il salvataggio in una posizione specificata. È anche possibile riavviare la console LRS (interfaccia utente di LRS) o riavviare l'intero sistema.

![Registrazione della sala nel portale di amministrazione di Lync Room System](images/Dn743660.749aee71-deaa-4ace-a146-fe2b349f0f42(OCS.15).png "Registrazione della sala nel portale di amministrazione di Lync Room System")

## Health

La sezione Health offre una rappresentazione visiva dello stato di integrità della connessione a Lync Server, del dispositivo audio, del dispositivo video, dello stato di resilienza e del dispositivo schermo.

![Integrità della sala nel portale di amministrazione di Lync Room System](images/Dn743660.8cc644f8-8e3e-42d5-9079-045d8fe9daa7(OCS.15).png "Integrità della sala nel portale di amministrazione di Lync Room System")

## Note aggiuntive sul portale Web amministrativo


> [!NOTE]
> <UL>
> <LI>
> <P>Per motivi di sicurezza, il portale Web amministrativo disconnette l'utente ogni 15 minuti.</P>
> <LI>
> <P>Le modifiche delle applicazioni diventano effettive solo dopo il riavvio del sistema LRS.</P>
> <LI>
> <P>Le notifiche nel portale Web amministrativo di LRS sono permanenti, ovvero non scompaiono.</P>
> <LI>
> <P>Le notifiche vengono visualizzate solo dopo l'aggiornamento della pagina.</P>
> <LI>
> <P>Lo stato delle sale LRS viene visualizzato dopo l'aggiornamento della pagina.</P>
> <LI>
> <P>In caso di scadenza della password dell'account LRSApp, non sarà possibile visualizzare lo stato delle sale. Configurare la password dell'account LRSAppuser in modo che non scada mai oppure assicurarsi di aggiornarla in prossimità della scadenza.</P>
> <LI>
> <P>Il portale Web amministrativo di LRS è supportato solo per distribuzioni in locale.</P></LI></UL>



## Risoluzione dei problemi

## Perché non si riesce ad accedere al portale Web amministrativo?

  - All'apertura di https://localhost/lrs viene visualizzata la pagina di accesso, ma quando si digitano le credenziali l'accesso non riesce. In questo caso è necessario aprire https://FQDNofFEserver/lrs per accedere al portale Web amministrativo.

  - Se il computer da cui si accede al portale Web amministrativo è inclusa in un gruppo di lavoro, "http://" non funziona ed è invece necessario usare "https".

## Perché LRS non compare nel portale Web amministrativo?

  - Verificare che esistano account LRS nella distribuzione e che siano stati creati in base alle raccomandazioni per la distribuzione del portale Web amministrativo di LRS. Assicurarsi che il provisioning degli account LRS sia eseguito con Enable-CsMeetingRoom, e non con Enable-CsUser, nel server Lync.

  - Se sono stati creati account LRS ma questi non sono visibili nel portale Web amministrativo, raccogliere i log del server tramite lo strumento di registrazione di Lync Server selezionando il componente **MeetingPortal** e quindi inviarli al contatto per il supporto tecnico di LRS.

## Perché lo stato di LRS non è visibile nel portale Web amministrativo?

  - Verificare che l'account utente LRSApp sia abitato per SIP.

  - Se il problema persiste, inviare il file **Trace.log** nel sistema LRS in D:\\Tracing\\LRSAdminLogs\\ al contatto per il supporto tecnico di LRS.

