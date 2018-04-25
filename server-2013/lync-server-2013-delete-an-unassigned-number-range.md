---
title: Eliminare un intervallo di numeri non assegnati
TOCTitle: Eliminare un intervallo di numeri non assegnati
ms:assetid: a8141bfb-b94d-4d0f-a7a9-2e60d10b103a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182565(v=OCS.15)
ms:contentKeyID: 49301585
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un intervallo di numeri non assegnati

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per eliminare un intervallo di numeri non assegnati per gli annunci, eseguire le procedure illustrate di seguito.

## Per eliminare un intervallo di numeri non assegnati utilizzando il Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Funzionalità vocali** e quindi su **Numero non assegnato**.

4.  Nel campo di ricerca della pagina **Numero non assegnato** digitare per intero o in parte il nome dell'intervallo di numeri non assegnati che si desidera eliminare.

5.  Nell'elenco risultante degli intervalli di numeri fare clic sul nome, su **Modifica** e quindi su **Elimina**.

6.  Fare clic su **Salva tutto**.

## Per eliminare un intervallo di numeri non assegnati utilizzando i cmdlet

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare:
    
        Remove-CsUnassignedNumber -Identity "<name of unassigned number range>" 
    
    Ad esempio:
    
        Remove-CsUnassignedNumber -Identity "Unassigned range 1"
    

    > [!NOTE]
    > Per informazioni dettagliate su ulteriori opzioni, vedere <A href="remove-cscallparkorbit.md">Remove-CsCallParkOrbit</A>.



## Vedere anche

#### Attività

[Creare o modificare un intervallo di numeri non assegnati in Lync Server 2013](lync-server-2013-create-or-modify-an-unassigned-number-range.md)  

#### Ulteriori risorse

[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)

