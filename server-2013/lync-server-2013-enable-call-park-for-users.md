---
title: 'Lync Server 2013: Abilitare il parcheggio di chiamata per gli utenti'
TOCTitle: Abilitare il parcheggio di chiamata per gli utenti
ms:assetid: 9430763f-3394-467c-9c6d-426bf761604e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398753(v=OCS.15)
ms:contentKeyID: 49301358
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare il parcheggio di chiamata per gli utenti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-11_

Gli utenti non possono parcheggiare le chiamate né recuperare le chiamate parcheggiate finché non vengono abilitati per il Parcheggio di chiamata nel criterio vocale.


> [!NOTE]
> Per impostazione predefinita, l'applicazione Parcheggio di chiamata è disabilitata per tutti gli utenti.



È possibile abilitare il Parcheggio di chiamata nell'ambito globale, a livello di sito o per utente. L'ambito utente ha la precedenza rispetto all'ambito a livello di sito, che a sua volta ha la precedenza rispetto all'ambito globale. Se sono presenti più criteri vocali, controllarli tutti per abilitare Parcheggio di chiamata, non solo i criteri globali.

## Per usare Pannello di controllo di Lync Server per abilitare il Parcheggio di chiamata per gli utenti

1.  Accedere al computer come membro del gruppo **RTCUniversalServerAdmins** o come membro del ruolo amministrativo **CsVoiceAdministrator** , **CsServerAdministrator** o **CsAdministrator** .

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** .

4.  Fare clic sulla scheda **Criteri vocali** .

5.  Fare doppio clic su un criterio esistente per aprire la finestra di dialogo **Modifica criterio vocale** .

6.  In **Funzionalità di chiamata** selezionare **Abilita parcheggio di chiamata** .

7.  Fare clic su **OK** per salvare il criterio vocale.

## Per usare i cmdlet per abilitare Parcheggio di chiamata per gli utenti

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo amministrativo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Set-CsVoicePolicy -Identity <VoicePolicy> -EnableCallPark $true
    
    Ad esempio, per abilitare Parcheggio di chiamata per il criterio vocale globale predefinito:
    
        Set-CsVoicePolicy -EnableCallPark $true

## Vedere anche

#### Attività

[Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)

