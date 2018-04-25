---
title: Eliminazione dei profili criteri larghezza di banda della rete
TOCTitle: Eliminazione dei profili criteri larghezza di banda della rete
ms:assetid: 4d6beda8-6aa5-4d5e-8a07-363598f0e0c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688050(v=OCS.15)
ms:contentKeyID: 49887555
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione dei profili criteri larghezza di banda della rete

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Nel servizio Controllo di ammissione di chiamata (CAC) vengono usati criteri di larghezza di banda per definire le limitazioni della larghezza di banda per alcune modalità. In Microsoft Lync Server 2013, è possibile assegnare tali limitazioni solo alle modalità audio e video. È possibile impostare limitazioni della larghezza di banda globali o per le sessioni. Il Pannello di controllo di Lync Server consente di creare, modificare o eliminare un profilo contenitore per questi criteri. Usare le procedure seguenti per eliminare profili di criteri della larghezza di banda di rete. Per informazioni dettagliate sulla creazione o la modifica di un profilo di criteri della larghezza di banda di rete, vedere [Creazione o modifica di profili di criteri di larghezza di banda](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md).

## Per eliminare un profilo di criteri della larghezza di banda

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri larghezza di banda**.

4.  Nella pagina **Criteri larghezza di banda** fare clic sul profilo di criteri della larghezza di banda che si desidera eliminare.
    

    > [!NOTE]
    > È possibile eliminare più profili contemporaneamente. A tale scopo, tenere premuto CTRL e selezionare i diversi profili. In alternativa, per selezionare tutti i profili, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG>.



5.  Scegliere **Elimina** dal menu **Modifica**.
    

    > [!WARNING]
    > Non è possibile eliminare un profilo di criteri della larghezza di banda associato a un sito di rete. È necessario rimuovere l'associazione al sito di rete prima di poter eliminare il profilo. Per informazioni dettagliate su come modificare il sito di rete, vedere <A href="lync-server-2013-creating-or-modifying-network-sites.md">Creazione o modifica dei siti di rete</A>.



## Vedere anche

#### Attività

[Creazione o modifica di profili di criteri di larghezza di banda](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md)  
[Visualizzazione delle informazioni sul profilo dei criteri di larghezza di banda della rete](lync-server-2013-viewing-network-bandwidth-policy-profile-information.md)  

#### Ulteriori risorse

[Configurare il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-configure-call-admission-control.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)

