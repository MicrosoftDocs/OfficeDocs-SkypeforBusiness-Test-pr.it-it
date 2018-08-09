---
title: "Lync Server 2013: Elimina intervallo di codici orbit del parcheggio"
TOCTitle: "Lync Server 2013: Elimina intervallo di codici orbit del parcheggio"
ms:assetid: 85e9f916-062d-450d-ac0a-aeaefc0f7cdc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182546(v=OCS.15)
ms:contentKeyID: 49301208
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Eseguire una delle seguenti procedure per rimuovere un intervallo orbit del Parcheggio di chiamata.

## Utilizzo di Pannello di controllo di Lync Server per l'eliminazione di un intervallo orbit di Parcheggio di chiamata

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Funzionalità vocali** e quindi su **Parcheggio di chiamata**.

4.  Nella pagina **Parcheggio di chiamata**, nel campo di ricerca, digitare il nome, o parte di esso, dell'intervallo di codici orbit che si desidera eliminare.

5.  Nell'elenco di codici orbit fare clic sui codici orbit, fare clic su **Modifica** e quindi su **Elimina**.

6.  Fare clic su **OK**.

## Utilizzo di cmdlet per l'eliminazione di un intervallo orbit di Parcheggio di chiamata

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare:
    
        Remove-CsCallParkOrbit -Identity "<orbit range name>" 
    
    Ad esempio:
    
        Remove-CsCallParkOrbit -Identity "Redmond orbit 1"
    

    > [!NOTE]
    > Per informazioni dettagliate sulle altre opzioni, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit">Remove-CsCallParkOrbit</A>.



## Vedere anche

#### Attività

[Creare o modificare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)  

#### Ulteriori risorse

[Remove-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit)  
[Get-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCallParkOrbit)

