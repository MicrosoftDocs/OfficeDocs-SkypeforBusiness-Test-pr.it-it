---
title: Disabilitazione del bypass multimediale della rete
TOCTitle: Disabilitazione del bypass multimediale della rete
ms:assetid: 936d2678-d712-4589-b172-b5793013652f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688141(v=OCS.15)
ms:contentKeyID: 49887661
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disabilitazione del bypass multimediale della rete

 

_**Ultima modifica dell'argomento:** 2012-10-15_

Le impostazioni di bypass multimediale si applicano a livello globale nella distribuzione di Microsoft Lync Server 2013. Il bypass multimediale consente alle chiamate di ignorare il Mediation Server. Per informazioni dettagliate sull'uso del bypass multimediale, vedere [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md) nella sezione relativa alla pianificazione. È possibile disabilitare il bypass multimediale dal Pannello di controllo di Lync Server. Per informazioni dettagliate sull'abilitazione e la configurazione del bypass multimediale, vedere [Abilitazione del bypass multimediale della rete](lync-server-2013-enabling-network-media-bypass.md)

## Per disabilitare il bypass multimediale

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Globale** .

4.  Nella pagina **Globale** fare clic sulla scheda della configurazione **Globale** . Esiste sempre una sola configurazione ed è sempre denominata Globale.

5.  Scegliere **Mostra dettagli** dal menu **Modifica** .

6.  Nella pagina **Modifica impostazioni globali** deselezionare la casella di controllo **Abilita bypass multimediale** .

7.  Fare clic su **Commit** per salvare le modifiche.

## Vedere anche

#### Attività

[Abilitazione del bypass multimediale della rete](lync-server-2013-enabling-network-media-bypass.md)

