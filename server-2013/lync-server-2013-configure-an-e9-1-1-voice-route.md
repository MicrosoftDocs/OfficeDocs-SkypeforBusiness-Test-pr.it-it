---
title: Configurare una route vocale E9-1-1 in Lync Server 2013
TOCTitle: Configurare una route vocale E9-1-1 in Lync Server 2013
ms:assetid: 6933b840-0e7b-4509-ae43-bc9065677547
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398496(v=OCS.15)
ms:contentKeyID: 49300852
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare una route vocale E9-1-1 in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Per distribuire il servizio E9-1-1, è innanzitutto necessario configurare una route vocale per le chiamate di emergenza. Per informazioni dettagliate sulla creazione di route vocali, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md). È possibile definire più di una route, ad esempio, se nella distribuzione sono inclusi un trunk SIP primario e un trunk SIP secondario.


> [!NOTE]
> Per includere informazioni sulla posizione in un messaggio INVITE E9-1-1, è necessario configurare il trunk SIP per la connessione al provider di servizi E9-1-1 in modo che esegua il routing delle chiamate di emergenza attraverso il gateway. A tale scopo, impostare il flag EnablePIDFLOSupport nel cmdlet <STRONG>set-cstrunkconfiguration</STRONG> su True. Il valore predefinito per EnablePIDFLOSupport è False. Ad esempio: <CODE>set-cstrunkconfiguration Service:PstnGateway:192.168.0.241 -EnablePIDFLOSupport $true.</CODE><BR>Non è necessario abilitare la ricezione delle posizioni per i gateway PSTN (Public Switched Telephone Network) di fallback e i gateway ELIN (Emergency Location Identification Number).



Per informazioni dettagliate sull'utilizzo delle route vocali, vedere la documentazione di Lync Server Management Shell per i cmdlet seguenti:

  - **Set-CsPstnUsage**

  - **Get-CsPstnUsage**

  - **New-CsVoiceRoute**

  - **Get-CsVoiceRoute**

  - **Set-CsVoiceRoute**

  - **Remove-CsVoiceRoute**

## Per configurare una route vocale E9-1-1

1.  Accedere al computer con un account membro del gruppo RTCUniversalServerAdmins o del ruolo amministrativo CsVoiceAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il cmdlet seguente per creare un nuovo record di utilizzo PSTN.
    
    Deve essere lo stesso nome che verrà utilizzato per l'impostazione **PSTN** nei criteri di percorso. Anche se nella distribuzione reale saranno disponibili più record di utilizzo del telefono, nell'esempio seguente viene aggiunto "Emergency Usage" all'elenco corrente di utilizzi PSTN disponibili. Per informazioni dettagliate, vedere [Configurazione di criteri vocali e record utilizzo PSTN per autorizzare privilegi e funzionalità di chiamata in Lync Server 2013](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md).
    
        Set-CsPstnUsage -Usage @{add='EmergencyUsage'}

4.  Eseguire il cmdlet seguente per creare una nuova route vocale con il record di utilizzo PSTN creato nel passaggio precedente.
    
    Il formato del numero deve essere lo stesso utilizzato nell'impostazione **Maschera di composizione di emergenza** nei criteri di percorso. È necessario un segno "+" perché Lync aggiunge il segno "+" alle chiamate di emergenza. "Co1-pstngateway-1" è l'ID di servizio del trunk SIP per il provider di servizi E9-1-1 o l'ID di servizio del gateway ELIN. Nell'esempio seguente viene utilizzato il nome "EmergencyRoute" per la route vocale.
    
        New-CsVoiceRoute -Name "EmergencyRoute" -NumberPattern "^\+911$" -PstnUsages @{add="EmergencyUsage"} -PstnGatewayList @{add="co1-pstngateway-1"}

5.  Facoltativamente, per le connessioni trunk SIP è consigliabile eseguire il cmdlet seguente per creare una route locale per le chiamate non gestite dal trunk SIP del provider di servizi E9-1-1. Questa route verrà utilizzata se la connessione al provider di servizi E9-1-1 non è disponibile.
    
    Nell'esempio seguente si presuppone che i criteri vocali dell'utente includano l'utilizzo 'Local'.
    
        New-CsVoiceRoute -Name "LocalEmergencyRoute" -NumberPattern "^\+911$" -PstnUsages @{add="Local"} -PstnGatewayList @{add="co1-pstngateway-2"}

