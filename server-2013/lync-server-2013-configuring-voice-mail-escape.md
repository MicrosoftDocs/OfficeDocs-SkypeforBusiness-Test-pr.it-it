---
title: Configurazione dell'escape della segreteria telefonica in Lync Server 2013
TOCTitle: Configurazione dell'escape della segreteria telefonica in Lync Server 2013
ms:assetid: a1d19e6c-82ff-4768-8ae5-da981368ce40
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688157(v=OCS.15)
ms:contentKeyID: 49887682
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'escape della segreteria telefonica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Quando un utente configura lo squillo simultaneo su un telefono cellulare, un chiamante in genere viene instradato alla segreteria telefonica personale dell'utente se il telefono cellulare è spento, scarico o in una zona senza copertura. Con Microsoft Lync Server 2013 gli utenti possono scegliere di instradare le chiamate di lavoro alla segreteria telefonica aziendale. Più specificamente, è possibile configurare un timer e, se alla chiamata risponde la segreteria telefonica del vettore entro l'intervallo di tempo definito, Lync Server 2013 si disconnetterà dalla segreteria telefonica del vettore (e dalla segreteria telefonica personale dell'utente), mentre gli endpoint restanti dell'utente nel sistema aziendale continueranno a squillare. In questo modo il chiamante viene instradato automaticamente alla segreteria telefonica aziendale dell'utente.

Questa configurazione viene eseguita mediante il cmdlet Set-CsVoicePolicy di Lync Server Management Shell, a livello di criterio vocale, con i parametri seguenti.

## Configurare l'escape dalla segreteria telefonica

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Specificare i parametri seguenti per **Set-CsVoicePolicy**:
    
      - **EnableVoicemailEscapeTimer** - Consente di abilitare o disabilitare il timer di escape.
    
      - **PSTNVoicemailEscapeTimer** - Consente di specificare il valore di timeout in millisecondi. Il valore predefinito è 1500 millisecondi e i valori consentiti sono compresi tra 0 e 8000 millisecondi.

## Esempio

    Set-CsVoicePolicy UserVoicePolicy -EnableVoiceMailEscapeTimer $true - PSTNVoicemailEscapeTimer 2000
    
    Set-CsVoicePolicy -Identity site:SitePolicy -EnableVoiceMailEscapeTimer $true -PSTNVoicemailEscapeTimer 1500

## Vedere anche

#### Ulteriori risorse

[Configurazione di criteri vocali e record utilizzo PSTN per autorizzare privilegi e funzionalità di chiamata in Lync Server 2013](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md)

