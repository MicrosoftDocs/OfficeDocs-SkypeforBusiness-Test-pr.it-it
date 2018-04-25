---
title: Configurazione della larghezza di banda video in Lync Server 2013
TOCTitle: Configurazione della larghezza di banda video in Lync Server 2013
ms:assetid: 446bed91-b26f-4ab2-b2f5-36e6810b405b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204842(v=OCS.15)
ms:contentKeyID: 49300365
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della larghezza di banda video in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Lync Server 2013 include diverse impostazioni per la gestione dei video di chiamate con due partecipanti e conferenze con più partecipanti. Quando si distribuisce Lync Server 2013, è consigliabile verificare se le impostazioni predefinite sono appropriate per l'organizzazione, e modificarle se necessario.

I parametri descritti in questa sezione si applicano sia alle chiamate con due partecipanti che alle conferenze con più partecipanti. Visualizzare o modificare queste impostazioni usando uno dei cmdlet seguenti:

  - **Get-CsConferencingPolicy**

  - **Set-CsConferencingPolicy**

  - **New-CsConferencingPolicy**

Verificare le impostazioni seguenti nei criteri conferenza:

  - **VideoBitRateKb**   Questa impostazione specifica la velocità video in bit massima, espressa in kilobit al secondo (kbps), utilizzata per il video inviato da un utente. Il valore predefinito è 50000 kbps. I valori validi sono compresi tra 0 e 50000.
    
    Questa impostazione si applica separatamente al video principale e alla panoramica.
    
    Esempio: se si specifica il valore 2000 kbps, Lync Server può inviare 2000 kbps per il flusso del video principale e 2000 kbps per il flusso della panoramica.
    

    > [!NOTE]
    > La larghezza di banda massima di rete dei video per un endpoint Lync 2013 è pari a 8000 kbps per il video principale e a 2500 kbps per la panoramica. Questi valori massimi vengono raggiunti solo nel caso di invio o ricezione di più video. Per informazioni dettagliate, vedere la sezione "Utilizzo della rete per il traffico multimediale" in <A href="lync-server-2013-network-bandwidth-requirements-for-media-traffic.md">Requisiti di larghezza di banda di rete per il traffico multimediale in Lync Server 2013</A>. In questa sezione sono elencati i valori massimi e tipici della larghezza di base dei flussi video per tutte le risoluzioni supportate.



  - **TotalReceiveVideoBitRateKb**   Questa impostazione, che costituisce una novità in Lync Server 2013, specifica la velocità in bit massima consentita (in kilobit al secondo) per tutti i flussi video ricevuti da un client. In altre parole, specifica il totale combinato per tutti i flussi video, ad eccezione di quelli della panoramica, che un client può ricevere. Se si specifica il valore 1500 kbps, un client può ad esempio ricevere fino a 1500 kbps di video, in cui possono essere compresi uno o più flussi video. Questa impostazione si applica solo ai client Lync Server 2013.
    
    Il valore predefinito di **TotalReceiveVideoBitRateKb** è 50000 kbps. Se l'impostazione **EnableMultiviewJoin** della visualizzazione Raccolta corrisponde a True, **TotalReceiveVideoBitRateKb** non deve essere impostato al di sotto di 420 kbps. Se l'impostazione **EnableMultiviewJoin** relativa alla visualizzazione Raccolta corrisponde a False, **TotalReceiveVideoBitRateKb** non deve essere impostato al di sotto di 100 kbps. Se **EnableMultiviewJoin** è impostato su True e il valore impostato è al di sotto di 420 kbps, i valori assumeranno per impostazione predefinita quello della soglia. Il valore della soglia impedisce un'errata configurazione accidentale che potrebbe determinare un'esperienza scarsa per gli utenti.
    

    > [!NOTE]
    > Per informazioni dettagliate sull'impostazione <STRONG>EnableMultiviewJoin</STRONG>, vedere <A href="lync-server-2013-configuring-gallery-view.md">Configurazione della visualizzazione Raccolta</A>.



  - **MaxVideoConferencingResolution**   Questo parametro non viene più utilizzato per i client Lync Server 2013 nelle conferenze Lync Server 2013. Nelle conferenze Lync Server 2013 vengono usati i controlli della velocità in bit descritti prima in questa sezione. Questa impostazione viene ancora utilizzata per i client legacy che partecipano a una conferenza Lync Server 2013. Da questo parametro dipende la risoluzione massima consentita per i client legacy nelle conferenze organizzate dagli utenti ospitati in Lync Server 2013. In altre parole, i client legacy vengono considerati come nelle versioni precedenti di Lync Server o Office Communications Server.

Oltre alle impostazioni dei criteri conferenza che si applicano agli utenti, prendere in considerazione l'uso delle impostazioni di configurazione multimediale. Visualizzare o modificare queste impostazioni usando uno dei cmdlet seguenti:

  - **Get-CsMediaConfiguration**

  - **Set- CsMediaConfiguration**

  - **New- CsMediaConfiguration**

Verificare l'impostazione seguente:

  - **MaxVideoRateAllowed**   Questa impostazione per pool specifica la velocità massima di trasferimento dei segnali video agli endpoint client. Si applica solo alle versioni precedenti dei client Lync Server.
    

    > [!NOTE]
    > I client Lync Server 2013 la ignorano e utilizzano invece l'impostazione TotalReceiveVideoBitRateKb nei criteri conferenza.

    
    Il valore predefinito è HD720P. I valori validi sono HD720p15M, VGA600K e CIF250K.
    
    Esempio: se si specifica il valore 1500 kbps, tutti i client legacy del pool possono ricevere fino a 1500 kbps di video in conferenze con due o più partecipanti.

Le procedure seguenti sono esempi dell'utilizzo di Lync Server Management Shell per la modifica delle impostazioni descritte in questa sezione.

## Per modificare i criteri conferenza per le impostazioni video

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Alla riga di comando eseguire il cmdlet seguente per modificare i criteri conferenza:
    
        Set-CsConferencingPolicy -Identity Pool01ConferencingPolicy -VideoBitRateKb 2000 -TotalReceiveVideoBitRateKb 2000 

## Per modificare la configurazione multimediale per i client legacy

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Alla riga di comando eseguire il cmdlet seguente per modificare la configurazione multimediale:
    
        Set-CsMediaConfiguration -Identity site:Redmond01 -MaxVideoRateAllowed CIF250K

