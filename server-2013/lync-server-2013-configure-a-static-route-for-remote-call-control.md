---
title: 'Lync Server 2013: Configurare una route statica per il controllo delle chiamate remote'
TOCTitle: Configurare una route statica per il controllo delle chiamate remote
ms:assetid: f7003023-443d-48ee-989b-71e8b0b0abbd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615051(v=OCS.15)
ms:contentKeyID: 49302512
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare una route statica per il controllo delle chiamate remote in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

Per il controllo delle chiamate remote è necessario che ogni pool Lync Server sia configurato con un percorso dal pool al gateway SIP/CSTA di connessione al PBX (Private Branch Exchange). Questo percorso richiede che ogni pool disponga di una route statica per ogni gateway che verrà utilizzato dal pool come proxy per i messaggi di controllo delle chiamate SIP associati alle chiamate al PBX. Se si configura una route statica globale per il controllo delle chiamate remote, ogni pool che non è configurato con una route statica a livello del pool utilizzerà la route statica globale.

## Per configurare una route statica per il controllo delle chiamate remote

1.  Accedere a un computer in cui è installato Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins o un ruolo di controllo di accesso basato sui ruoli a cui è stato assegnato il cmdlet **New-CsStaticRoute**.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per creare una route statica e inserirla nella variabile $TLSRoute o $TCPRoute, effettuare una delle operazioni seguenti:
    
    > [!TIP]  
    > Per includere tutti i domini figlio di un dominio, è possibile specificare un valore con caratteri jolly nel parametro MatchUri, ad esempio <strong>*.contoso.net</strong> . Tale valore consente di includere qualsiasi dominio che termina con il suffisso <strong>contoso.net</strong> .    
      - Per una connessione TLS (Transport Layer Security), al prompt dei comandi digitare il comando seguente:
        
            $TLSRoute = New-CsStaticRoute -TLSRoute -Destination <gateway FQDN> -Port <gateway SIP listening port> -UseDefaultCertificate $true -MatchUri <destination domain>
        
        Ad esempio:
        
            $TLSRoute = New-CsStaticRoute -TLSRoute -Destination rccgateway.contoso.net -Port 5065 -UseDefaultCertificate $true -MatchUri *.contoso.net
        
        Se UseDefaultCertificate è impostato su False, è necessario specificare i parametri TLSCertIssuer e TLSCertSerialNumber. Questi parametri indicano rispettivamente il nome dell'Autorità di certificazione che ha emesso il certificato utilizzato nella route statica e il numero di serie di tale certificato. Per informazioni dettagliate su questi parametri, vedere la Guida di Lync Server Management Shell digitando il comando seguente al prompt dei comandi:
        
            Get-Help New-CsStaticRoute -Full
    
      - Per una connessione TCP (Transmission Control Protocol), digitare il comando seguente al prompt dei comandi:
        

        > [!NOTE]
        > Se si specifica un nome di dominio completo (FQDN), è necessario configurare precedentemente un record DNS (Domain Name System) A.

        
            $TCPRoute = New-CsStaticRoute -TCPRoute -Destination <gateway IP address or FQDN> -Port <gateway SIP listening port> -MatchUri <destination domain>
        
        Ad esempio:
        
            $TCPRoute = New-CsStaticRoute -TCPRoute -Destination 192.168.0.240 -Port 5065 -MatchUri *.contoso.net
        
        Di seguito sono riportati i valori predefiniti per parametri facoltativi per route statiche:
        
          - Enabled = True
        
          - MatchOnlyPhoneUri = False
        
          - ReplaceHostInRequestUri = False
        
        È consigliabile non modificare questi valori predefiniti. Tuttavia, se fosse necessario modificare qualsiasi di questi parametri, vedere la Guida di Lync Server Management Shell digitando il comando seguente al prompt dei comandi:
        
            Get-Help New-CsStaticRoute -Full

4.  Per conservare una route statica appena creata nell' archivio di gestione centrale, eseguire uno dei comandi seguenti, a seconda delle esigenze:
    
    ```
    Set-CsStaticRoutingConfiguration -Route @{Add=$TLSRoute}
    ```
    ```
    Set-CsStaticRoutingConfiguration -Route @{Add=$TCPRoute}
    ```

## Vedere anche

#### Attività

[Configurare una voce applicazione attendibile per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)  
[Definire l'indirizzo IP di un gateway SIP/CSTA in Lync Server 2013](lync-server-2013-define-a-sip-csta-gateway-ip-address.md)

