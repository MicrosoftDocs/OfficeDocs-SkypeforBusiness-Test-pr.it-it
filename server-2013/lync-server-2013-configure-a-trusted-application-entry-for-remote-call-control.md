---
title: "Lync Server 2013: Configura voce applicaz. fidata per controllo chiam. remote"
TOCTitle: Configurare una voce applicazione attendibile per il controllo delle chiamate remote
ms:assetid: 37777f93-8b24-40cf-808e-7c6230eb2132
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558636(v=OCS.15)
ms:contentKeyID: 49300176
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare una voce applicazione attendibile per il controllo delle chiamate remote in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Il gateway SIP/CSTA deve essere configurato come applicazione attendibile perché Lync Server possa applicare una route statica per instradare le chiamate al gateway.

> [!IMPORTANT]  
> Se si esegue la migrazione di utenti da una versione precedente della distribuzione di Lync Server prima di eseguire le procedure illustrate in questo argomento verificare di aver rimosso tutte le voci esistenti di applicazioni attendibili (precedentemente note come voci di host autorizzati) create per il gateway SIP/CSTA. Per informazioni dettagliate, vedere <a href="lync-server-2013-remove-a-legacy-authorized-host-optional.md">Rimuovere un host autorizzato legacy in Lync Server 2013 (facoltativo)</a>.

## Per configurare una voce di applicazione attendibile per il gateway SIP/CSTA

1.  Eseguire l'accesso al computer in cui è installato Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins o di un ruolo del controllo di accesso basato sui ruoli a cui è stato assegnato il cmdlet **New-CsTrustedApplicationPool**.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per creare una voce di applicazione attendibile, eseguire una delle operazioni seguenti:
    
      - Per una connessione TLS (Transport Layer Security), al prompt dei comandi digitare il comando seguente:
        
            New-CsTrustedApplicationPool -Identity <FQDN of the SIP/CSTA gateway> [-Registrar <Service ID or FQDN of the Registrar service>] -Site <Site ID for the site where you want to create the trusted application pool>
        
        Ad esempio:
        
            New-CsTrustedApplicationPool -Identity rccgateway.contoso.net -Registrar registrar1.contoso.net -Site co1 -TreatAsAuthenticated $true -ThrottleAsServer $true
    
      - Per una connessione TCP (Transmission Control Protocol), digitare il comando seguente al prompt dei comandi:
        
            New-CsTrustedApplicationPool -Identity <IP address or FQDN of the SIP/CSTA gateway> [-Registrar <Service ID or FQDN of the Registrar service>] -Site <Site ID for the site where you want to create the trusted application pool>
        
        Ad esempio:
        
            New-CsTrustedApplicationPool -Identity 192.168.0.240 -Registrar registrar1.contoso.net -Site co1 -TreatAsAuthenticated $true -ThrottleAsServer $true

4.  Per aggiungere l'applicazione attendibile al pool, eseguire una delle operazioni seguenti:
    
      - Per una connessione TLS, al prompt dei comandi digitare quanto segue:
        
            New-CsTrustedApplication -ApplicationID <application name> -TrustedApplicationPoolFqdn <FQDN of the SIP/CSTA gateway> -Port <SIP listening port on the gateway>
        
        Ad esempio:
        
            New-CsTrustedApplication -ApplicationID RccGateway-1 -TrustedApplicationPoolFqdn rccgateway.contoso.net -Port 5065
    
      - Per una connessione TCP, al prompt dei comandi digitare quanto segue:
        
            New-CsTrustedApplication -ApplicationID <application name> -TrustedApplicationPoolFqdn <IP address or FQDN of the SIP/CSTA gateway> -Port <SIP listening port on the gateway> -EnableTcp
        
        Ad esempio:
        
            New-CsTrustedApplication -ApplicationID RccGateway-1 -TrustedApplicationPoolFqdn 192.169.0.240 -Port 5065 -EnableTcp

5.  Per implementare le modifiche pubblicate apportate alla topologia, al prompt dei comandi digitare quanto segue:
    
        Enable-CsTopology

## Vedere anche

#### Attività

[Configurare una route statica per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-static-route-for-remote-call-control.md)  
[Definire l'indirizzo IP di un gateway SIP/CSTA in Lync Server 2013](lync-server-2013-define-a-sip-csta-gateway-ip-address.md)

