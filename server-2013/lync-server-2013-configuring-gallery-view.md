---
title: Configurazione della visualizzazione Raccolta
TOCTitle: Configurazione della visualizzazione Raccolta
ms:assetid: 4a609178-47d8-4682-ac8d-29f882801924
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204871(v=OCS.15)
ms:contentKeyID: 49300432
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della visualizzazione Raccolta

 

_**Ultima modifica dell'argomento:** 2012-10-30_

In Lync Server 2013 la configurazione delle conferenze video della visualizzazione Raccolta avviene tramite criteri di conferenza. La visualizzazione Raccolta è attivata per impostazione predefinita. Se non si vuole consentire la visualizzazione Raccolta o la si vuole consentire solo per alcuni utenti, è necessario disattivarla nei criteri di conferenza.

Se per un partecipante della conferenza le funzionalità video non sono disponibili, l'esperienza della visualizzazione Raccolta può essere migliorata per l'utente con la distribuzione di foto ad alta risoluzione, una nuova funzionalità di Lync Server 2013. Le foto ad alta risoluzione sono un'alternativa alle foto dei contatti, più piccole e con una risoluzione limitata, archiviate in Servizi di dominio Active Directory. Le foto ad alta risoluzione sono archiviate in una cassetta postale Exchange 2013 dell'utente e quindi richiedono l'integrazione di Lync Server 2013 con Exchange 2013. Per informazioni dettagliate, vedere l'articolo del blog NextHop "Integrazione di Exchange 2013 e Lync Server 2013" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=260987\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=260987%26clcid=0x410).


> [!NOTE]
> Il contenuto di ogni blog e i relativi URL sono soggetti a modifiche senza preavviso.



Per visualizzare o modificare i parametri della visualizzazione Raccolta tramite il Pannello di controllo di Lync Server 2013 o uno dei cmdlet seguenti:

  - **Get-CsConferencingPolicy**

  - **Set-CsConferencingPolicy**

  - **New-CsConferencingPolicy**

Configurare la visualizzazione Raccolta con le impostazioni dei criteri di conferenza seguenti:

  - **AllowMultiview**   Questo parametro controlla se gli utenti sono autorizzati a organizzare conferenze video della visualizzazione Raccolta. Si applica a riunioni programmate e ad hoc create dall'utente.
    
    Esempi:
    
      - Questo parametro è impostato su True per l'utente A, disponibile in un pool Lync Server 2013. Le riunioni organizzate dall'utente A consentono agli utenti di partecipare e ricevere più flussi video.
    
      - Questo parametro è impostato su False per l'utente B, disponibile in un pool Lync Server 2013. Le riunioni organizzate dall'utente B offrono un unico flusso video, simile alle conferenze video consentite da Lync Server 2010.
    
    Questo parametro determina chi può organizzare riunioni con più flussi video. I partecipanti di riunioni che consentono più flussi video possono o non possono ricevere più flussi video, a seconda delle autorizzazioni individuali. Vedere la descrizione del parametro EnableMultiviewJoin.

  - **EnableMultiviewJoin**   Questo parametro controlla se i partecipanti possono usufruire dell'esperienza video della visualizzazione Raccolta durante le riunioni che la consentono. Il parametro controlla l'esperienza utente per tutte le riunioni a cui gli utenti partecipano.
    
    Esempi:
    
      - Questo parametro è impostato su True per l'utente C. L'utente C può ricevere più flussi video quando partecipa a riunioni organizzate o avviate dall'utente A. Quando partecipa alle riunioni organizzate o avviate dall'utente B, l'utente C riceve un unico flusso video, simile alle conferenze video consentite da Lync Server 2010.
    
      - Questo parametro è impostato su False per l'utente D. Quando partecipa alle riunioni organizzate o avviate dall'utente A o B, l'utente D riceve un unico flusso video, simile alle conferenze video consentite da Lync Server 2010.

La procedura seguente è un esempio di uso di Lync Server Management Shell per consentire le conferenze video della visualizzazione Raccolta.

## Per modificare i criteri di conferenza per le conferenze video della visualizzazione Raccolta

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per modificare i criteri di conferenza, dalla riga di comando eseguire il cmdlet seguente:
    
        Set-CsConferencingPolicy -Identity Pool01ConferencingPolicy -AllowMultiview $true -EnableMultiviewJoin $true

