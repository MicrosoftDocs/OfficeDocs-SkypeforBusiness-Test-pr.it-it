---
title: "Lync Server 2013: Abilitare gli utenti per l'archivio contatti unificato"
TOCTitle: Abilitare gli utenti per l'archivio contatti unificato
ms:assetid: 7b46a01f-beb5-4a33-adb0-35f0502b168d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205024(v=OCS.15)
ms:contentKeyID: 49301087
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare gli utenti per l'archivio contatti unificato in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-07_

Quando si distribuisce Lync Server 2013 e si pubblica la topologia, l'archivio unificato per i contatti viene abilitato per impostazione predefinita per tutti gli utenti. Dopo la distribuzione di Lync Server 2013, non è necessario eseguire ulteriori operazioni. Tuttavia, è possibile utilizzare il cmdlet **Set-CsUserServicesPolicy** per decidere a quali utenti rendere l'archivio unificato per i contatti disponibile. È possibile abilitare questa caratteristica a livello globale, di sito, tenant, o per utenti singoli o gruppi di utenti.

## Per abilitare gli utenti all'archivio unificato contatti

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Effettuare una delle operazioni seguenti:
    
      - Per abilitare l'archivio unificato per i contatti a livello globale per tutti gli utenti di Lync Server, digitare quanto segue nella riga di comando:
        
            Set-CsUserServicesPolicy -Identity global -UcsAllowed $True
    
      - Per abilitare l'archivio unificato per i contatti a livello globale per gli utenti di un sito specifico, digitare quanto segue nella riga di comando:
        
            New-CsUserServicesPolicy -Identity site:<site name> -UcsAllowed $True
        
        Ad esempio:
        
            New-CsUserServicesPolicy -Identity site:Redmond -UcsAllowed $True
    
      - Per abilitare l'archivio unificato per tenant, digitare quanto segue nella riga di comando:
        
            Set-CsUserServicesPolicy -Tenant <tenantId> -UcsAllowed $True
        
        Ad esempio:
        
            Set-CsUserServicesPolicy -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -UcsAllowed $True
    
      - Per abilitare l'archivio unificato per utente specifico, digitare quanto segue nella riga di comando:
        
            New-CsUserServicesPolicy -Identity "<policy name>" -UcsAllowed $True
            Grant-CsUserServicesPolicy -Identity "<user display name>" -PolicyName <"policy name">
        

        > [!NOTE]
        > Al posto del nome visualizzato dell'utente, è inoltre possibile utilizzare alias utente o URI SIP.

        
        Ad esempio:
        
            New-CsUserServicesPolicy -Identity "UCS Enabled Users" -UcsAllowed $True
            Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName "UCS Enabled Users"
        

        > [!NOTE]
        > Nell'esempio precedente, il primo comando crea un nuovo criterio per utente chiamato <EM>UCS Enabled Users</EM> , con il contrassegno UcsAllowed impostato su True. Il secondo comando assegna il criterio all'utente con nome visualizzato Ken Myer, e pertanto Ken Myer è ora abilitato all'archivio unificato per i contatti.


