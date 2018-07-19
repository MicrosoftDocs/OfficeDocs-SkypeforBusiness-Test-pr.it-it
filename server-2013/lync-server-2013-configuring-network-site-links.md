---
title: Configurazione dei collegamenti di siti di rete
TOCTitle: Configurazione dei collegamenti di siti di rete
ms:assetid: 7e9147ae-e727-46c8-8c1a-6c13201f09be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521023(v=OCS.15)
ms:contentKeyID: 49301118
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei collegamenti di siti di rete

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Nell'ambito della configurazione del servizio Controllo di ammissione di chiamata, è possibile creare criteri tra siti di rete per la definizione di limiti di larghezza di banda tra siti direttamente collegati. Se due siti di rete condividono un collegamento diretto, è possibile definire limiti di larghezza di banda per le connessioni audio e video tra tali siti. Non è possibile utilizzare il Pannello di controllo di Lync Server per configurare i criteri sito di rete. A tale scopo è possibile utilizzare solo i cmdlet di Lync Server Management Shell. È possibile creare, modificare e rimuovere un collegamento di sito di rete (conosciuto anche come criterio tra siti) da Lync Server Management Shell.

## Per creare un collegamento di sito di rete

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Al prompt dei comandi digitare il comando seguente, utilizzando valori validi per la configurazione in uso:
    
        New-CsNetworkInterSitePolicy -Identity Reno_Portland -NetworkSiteID1 Reno -NetworkSiteID2 Portland -BWPolicyProfileID LowBWLimits
    
    In questo esempio viene creato un nuovo collegamento di sito di rete denominato Reno\_Portland, che consente di impostare le limitazioni di larghezza di banda tra i siti di rete di Reno e Portland. Il profilo dei criteri di larghezza di banda e siti di rete deve essere già presente prima dell'esecuzione di questo comando.

Per descrizioni dettagliate dei parametri, vedere [New-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterSitePolicy) nella documentazione di Lync Server Management Shell. Per ottenere un elenco dei profili dei criteri di larghezza di banda che è possibile applicare al collegamento di sito di rete, chiamare il cmdlet **Get-CsNetworkBandwidthPolicyProfile**. Per informazioni dettagliate, vedere [Get-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkBandwidthPolicyProfile) nella documentazione di Lync Server Management Shell.

## Per modificare un collegamento di sito di rete

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Utilizzare il cmdlet **CsNetworkInterSitePolicy Set** per modificare le proprietà di un collegamento di sito di rete specifico. È possibile modificare uno dei siti connessi o entrambi ed è possibile modificare il profilo dei criteri di larghezza di banda associato al collegamento. Di seguito è riportato un esempio di modifica del profilo dei criteri di larghezza di banda di un collegamento di sito denominato Reno\_Portland:
    
        Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

Per descrizioni dettagliate dei parametri, vedere [Set-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterSitePolicy) nella documentazione di Lync Server Management Shell.

## Per eliminare un collegamento di sito di rete

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Utilizzare il cmdlet **Remove-CsNetworkInterSitePolicy** per rimuovere un collegamento di sito di rete. Nell'esempio seguente viene eliminato il collegamento di sito di rete Reno\_Portland:
    
        Remove-CsNetworkInterSitePolicy -Identity Reno_Portland

Per descrizioni dettagliate dei parametri, vedere [Remove-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterSitePolicy) nella documentazione di Lync Server Management Shell.

## Vedere anche

#### Concetti

[Cmdlet per il servizio Controllo di ammissione di chiamata](lync-server-2013-call-admission-control-cmdlets.md)  

#### Ulteriori risorse

[New-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterSitePolicy)  
[Set-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterSitePolicy)  
[Remove-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterSitePolicy)  
[Get-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkInterSitePolicy)  
[Get-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkBandwidthPolicyProfile)

