---
title: "Lync Server 2013: Configura funzion. multimed. per ignorare Mediation Server"
TOCTitle: "Lync Server 2013: Configura funzion. multimed. per ignorare Mediation Server"
ms:assetid: 370c4f54-e520-4d77-96a3-84c5e84a9996
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425846(v=OCS.15)
ms:contentKeyID: 49300174
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la funzionalità bypass multimediale in modo che Mediation Server venga sempre ignorato

 

_**Ultima modifica dell'argomento:** 2013-02-25_


> [!NOTE]
> In questo argomento si presuppone che la funzionalità di bypass multimediale sia già stata configurata per qualsiasi connessione trunk a un peer (un gateway PSTN (Public Switched Telephone Network), un IP-PBX (IP-Public Branch Exchange) o un SBC (Session Border Controller) presso un provider di servizi di telefonia Internet ITSP) per un sito o un servizio specifico per il quale si vuole ignorare il Mediation Server.<BR>Non è possibile configurare il contenuto multimediale in modo da ignorare sempre il Mediation Server e abilitare contemporaneamente il servizio Controllo di ammissione di chiamata. Queste impostazioni sono incompatibili e pertanto si escludono a vicenda nell'interfaccia utente del Pannello di controllo di Lync Server.



Oltre ad abilitare il bypass multimediale per le singole connessioni trunk associate a un peer del Mediation Server, è inoltre necessario configurare le impostazioni globali per il bypass multimediale. Se si utilizzano i passaggi descritti in questo argomento per configurare le impostazioni globali per il bypass multimediale, si presuppone che si disponga di una buona connettività tra gli endpoint di Lync e gli eventuali peer per cui è stato configurato il bypass multimediale nella connessione trunk.

Se invece non si dispone di una buona connettività tra gli endpoint di Lync Server e tutti i peer del Mediation Server le cui connessioni trunk sono state abilitate per il bypass multimediale, sarà necessario configurare le impostazioni di bypass multimediale globali in modo che, per l'utilizzo del bypass multimediale, vengano utilizzate le informazioni dei siti e delle aree. Ciò consente di specificare in modo più preciso quando il contenuto multimediale deve ignorare il Mediation Server. A tale scopo, utilizzare i passaggi descritti in [Configurare le impostazioni globali di bypass multimediale per l'utilizzo delle informazioni del sito e dell'area geografica](lync-server-2013-configure-media-bypass-global-settings-to-use-site-and-region-information.md) e [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md).

## Per abilitare il bypass multimediale globalmente in modo che il Mediation Server venga ignorato sempre

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete**.

3.  Fare doppio clic sulla configurazione **Globale** nell'elenco.

4.  Nella pagina **Modifica impostazioni globali** selezionare la casella di controllo **Abilita bypass multimediale**.

5.  Fare clic su **Ignora sempre**.

6.  Fare clic su **Commit**.

## Vedere anche

#### Concetti

[Configurare il bypass multimediale in Lync Server 2013](lync-server-2013-configure-media-bypass.md)  
[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)  
[Bypass multimediale e Mediation Server in Lync Server 2013](lync-server-2013-media-bypass-and-mediation-server.md)  

#### Ulteriori risorse

[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

