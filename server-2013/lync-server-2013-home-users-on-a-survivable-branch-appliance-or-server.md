---
title: 'Lync Server 2013: Ospitare utenti in Survivable Branch Appliance o Survivable Branch Server'
TOCTitle: Ospitare utenti in Survivable Branch Appliance o Survivable Branch Server
ms:assetid: faf1ebb9-6d7d-4a58-8ff7-801b7b31d3ba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413066(v=OCS.15)
ms:contentKeyID: 49302550
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ospitare utenti in Survivable Branch Appliance o Survivable Branch Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-12-10_

Il processo per ospitare gli utenti in Survivable Branch Appliance o Survivable Branch Server è simile a quello per ospitare gli utenti in un pool Front End. Eseguire la procedura per Survivable Branch Appliance o Survivable Branch Server nel sito centrale.

## Per ospitare utenti in Survivable Branch Appliance o Survivable Branch Server

1.  Prima di spostare gli utenti in Survivable Branch Server o Survivable Branch Server, aprire Lync Server Management Shell ed eseguire le operazioni seguenti:
    
      - Eseguire il cmdlet **Test-CsPstnOutboundCall** per verificare che Survivable Branch Server sia in esecuzione e che la connettività PSTN (Public Switched Telephone Network) sia configurata. Se è necessario modificare le proprietà del gateway PSTN, utilizzare il cmdlet **Set-CsPstnGateway**.
    
      - Eseguire il cmdlet **Get-CsVoicePolicy** per verificare che gli utenti che verranno ospitati in Survivable Branch Server dispongano del criterio di routing VoIP appropriato. Se è necessario modificare il criterio VoIP, utilizzare il cmdlet **Set-CsVoicePolicy**.
    
      - Eseguire il cmdlet **Get-CsVoicemailReroutingConfiguration** per verificare che siano state configurate le impostazioni di reindirizzamento della segreteria telefonica. Se è necessario modificare le impostazioni di reindirizzamento della segreteria telefonica, utilizzare il cmdlet **Set-CsVoicemailReroutingConfiguration**.

2.  In Lync Server Management Shell eseguire il cmdlet **Move-CsUser** per spostare gli utenti ospitati.


> [!NOTE]
> È anche possibile utilizzare Pannello di controllo di Lync Server per verificare i prerequisiti e ospitare gli utenti.



## Vedere anche

#### Ulteriori risorse

[Test-CsPstnOutboundCall](test-cspstnoutboundcall.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)  
[Move-CsUser](move-csuser.md)

