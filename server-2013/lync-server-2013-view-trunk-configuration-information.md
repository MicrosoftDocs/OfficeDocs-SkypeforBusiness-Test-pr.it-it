---
title: Visualizzare le informazioni sulla configurazione dei trunk
TOCTitle: Visualizzare le informazioni sulla configurazione dei trunk
ms:assetid: ebe10e14-08c2-4797-9254-9ed89516d5cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721927(v=OCS.15)
ms:contentKeyID: 49887806
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sulla configurazione dei trunk

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Le impostazioni per la configurazione trunk SIP definiscono le relazioni e le funzionalità abilitate tra un Mediation Server e il gateway PSTN (Public Switched Telephone Network), un sistema IP-PBX (Public Branch Exchange) o un servizio SBC (Session Border Controller) presso il provider di servizi. Queste impostazioni consentono di specificare, ad esempio:

  - Se il bypass multimediale deve essere abilitato nei trunk.

  - Le condizioni in cui vengono inviati i pacchetti RTCP (Real-time Transport Control Protocol).

  - Se la crittografia SRTP (Secure Real-Time Protocol) è richiesta in ogni trunk.

Quando si installa Microsoft Lync Server 2013, viene creata una raccolta globale di impostazioni di configurazione trunk SIP. Gli amministratori possono inoltre creare raccolte di impostazioni personalizzate nell'ambito del sito o del servizio (solo per il servizio gateway PSTN).

## Visualizzazione di informazioni di configurazione trunk SIP tramite l'utilizzo del Pannello di controllo di Lync Server

1.  Nel Pannello di controllo di Lync Server fare clic su **Routing vocale** e quindi su **Configurazione trunk**.

2.  Nella scheda **Configurazione trunk** verrà visualizzato un elenco di tutte le raccolte di impostazioni di configurazione trunk. Per ogni raccolta verranno visualizzati i valori delle proprietà **Nome**, **Ambito**, **Stato** e **Bypass multimediale**, insieme al numero di **Utilizzi PSTN**, alle **Regole per il numero del chiamante** e alle **Regole per il numero chiamato** associati alla raccolta. Per visualizzare ulteriori dettagli su una raccolta di impostazioni di configurazione trunk, fare clic sulla raccolta, quindi su **Modifica** e su **Mostra dettagli**. Si noti che è possibile visualizzare informazioni dettagliate per una sola raccolta di impostazioni di configurazione trunk alla volta.

## Visualizzazione di informazioni di configurazione trunk SIP tramite l'utilizzo di cmdlet di PowerShell per Lync Server

Le impostazioni di configurazione trunk SIP possono essere visualizzate anche utilizzando PowerShell per Lync Server e il cmdlet Get-CsTrunkConfiguration. Tale cmdlet può essere eseguito da Lync Server 2013 Management Shell o da Windows PowerShell remoto. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione di informazioni di configurazione trunk SIP

  - Per visualizzare informazioni su tutte le impostazioni di configurazione trunk SIP, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsTrunkConfiguration
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity                                  : Global
        OutboundTranslationRulesList              : {}
        SipResponseCodeTranslationRulesList       : {}
        OutboundCallingNumberTranslationRulesList : {}
        PstnUsages                                : {}
        Description                               :
        ConcentratedTopology                      : True
        EnableBypass                              : False
        EnableMobileTrunkSupport                  : False
        EnableReferSupport                        : True
        EnableSessionTimer                        : False
        EnableSignalBoost                         : False
        MaxEarlyDialogs                           : 20
        RemovePlusFromUri                         : False
        RTCPActiveCalls                           : True
        RTCPCallsOnHold                           : True
        SRTPMode                                  : Required
        EnablePIDFLOSupport                       : False
        EnableRTPLatching                         : False
        EnableOnlineVoice                         : False
        ForwardCallHistory                        : False
        Enable3pccRefer                           : False
        ForwardPAI                                : False
        EnableFastFailoverTimer                   : True

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Get-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTrunkConfiguration).

