---
title: Creazione o modifica di profili di criteri di larghezza di banda
TOCTitle: Creazione o modifica di profili di criteri di larghezza di banda
ms:assetid: 08a2e18f-9b0d-4a2f-aa14-13bbf79ec745
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520945(v=OCS.15)
ms:contentKeyID: 49299601
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione o modifica di profili di criteri di larghezza di banda

 

_**Ultima modifica dell'argomento:** 2012-10-15_

Nel servizio Controllo di ammissione di chiamata (CAC) vengono utilizzati criteri di larghezza di banda per definire le limitazioni della larghezza di banda per alcune modalità. In Microsoft Lync Server 2013 è possibile assegnare tali limitazioni solo alle modalità audio e video. È possibile impostare limitazioni della larghezza di banda globali o per le sessioni. Il Pannello di controllo di Lync Server consente di creare, modificare o eliminare un profilo contenitore per questi criteri. Ogni profilo di criteri della larghezza di banda può essere associato a uno o più siti di rete. Usare le procedure seguenti per creare o modificare un profilo di criteri della larghezza di banda. Per eliminare un profilo di criteri della larghezza di banda, vedere [Eliminazione dei profili criteri larghezza di banda della rete](lync-server-2013-deleting-network-bandwidth-policy-profiles.md)

## Per creare un nuovo profilo di criteri della larghezza di banda

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri larghezza di banda**.

4.  Nella pagina **Criteri larghezza di banda** fare clic su **Nuovo**.

5.  In **Nuovo profilo criteri larghezza di banda** digitare un nome nel campo **Nome**. Tale nome deve essere univoco fra tutti i profili di criteri della larghezza di banda.

6.  Nel campo **Limite audio** digitare un valore numerico. Tale valore rappresenta la larghezza di banda massima da allocare per tutte le connessioni audio, espressa in kbps.

7.  Immettere un valore numerico nel campo **Limite sessione audio**. Tale valore rappresenta la larghezza di banda massima da allocare per una singola connessione audio, espressa in kbps. Il valore deve essere almeno pari a 40.

8.  Immettere un valore numerico nel campo **Limite video**. Tale valore rappresenta la larghezza di banda massima da allocare per tutte le connessioni video, espressa in kbps.

9.  Immettere un valore numerico nel campo **Limite sessione video**. Tale valore rappresenta la larghezza di banda massima da allocare per una singola connessione video, espressa in kbps. Il valore deve essere almeno pari a 100.

10. (Facoltativo) Digitare un valore nel campo **Descrizione** per fornire ulteriori informazioni sul profilo di criteri della larghezza di banda che non possono essere espresse dal solo nome.

11. Fare clic su **Commit**.
    

    > [!NOTE]
    > Creando un nuovo profilo di criteri della larghezza di banda, non vengono automaticamente applicate le restrizioni relative alla larghezza di banda. È necessario prima associare il profilo di criteri a un sito. Per informazioni dettagliate a questo proposito, vedere <A href="lync-server-2013-creating-or-modifying-network-sites.md">Creazione o modifica dei siti di rete</A>.



## Per modificare un profilo di criteri della larghezza di banda

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri larghezza di banda**.

4.  Nella pagina **Criteri larghezza di banda** fare clic sul profilo di criteri della larghezza di banda che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Nella pagina **Modifica Profilo criteri larghezza di banda** modificare i campi in base alle proprie esigenze. Per informazioni dettagliate, vedere "Per creare un nuovo profilo di criteri della larghezza di banda" più indietro in questo argomento.

7.  Fare clic su **Commit**.
    

    > [!NOTE]
    > Quando si modifica il profilo di criteri della larghezza di banda, vengono immediatamente aggiornate le limitazioni relative alla larghezza di banda per tutti i siti di rete associati al profilo.



## Vedere anche

#### Attività

[Eliminazione dei profili criteri larghezza di banda della rete](lync-server-2013-deleting-network-bandwidth-policy-profiles.md)  

#### Ulteriori risorse

[Configurare il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-configure-call-admission-control.md)  
[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

