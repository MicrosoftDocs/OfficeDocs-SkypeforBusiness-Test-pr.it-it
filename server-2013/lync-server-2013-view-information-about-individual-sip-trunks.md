---
title: Visualizzare informazioni sui singoli trunk SIP
TOCTitle: Visualizzare informazioni sui singoli trunk SIP
ms:assetid: adfacb74-7ea5-4c53-934e-ba7ec59879eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721847(v=OCS.15)
ms:contentKeyID: 49887702
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare informazioni sui singoli trunk SIP

 

_**Ultima modifica dell'argomento:** 2013-02-21_

I trunk SIP vengono utilizzati per connettere la rete telefonica VoIP (Voice over IP) di Microsoft Lync Server 2013 alla rete PSTN (Public Switched Telephone Network). Nella versione precedente del prodotto i trunk vengono utilizzati per instradare le chiamate in uscita da un Mediation Server a un gateway PSTN e ogni gateway è limitato a un singolo trunk. Un gateway PSTN e un trunk SIP in questo caso pertanto sono essenzialmente identici. Per gli amministratori, questo significa che possono visualizzare le informazioni relative a un trunk SIP semplicemente visualizzando le informazioni relative al gateway PSTN associato.

In Lync Server 2013 invece è ora possibile assegnare più trunk a un singolo gateway PSTN, pertanto i gateway e i trunk non sono più identici. Questo di conseguenza significa che gli amministratori devono utilizzare il nuovo cmdlet [Get-CsTrunk](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTrunk) per visualizzare le informazioni relative a un singolo trunk SIP.

Il cmdlet Get-CsTrunk può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione delle informazioni relative a tutti i trunk SIP

  - Il comando seguente restituisce informazioni su tutti i trunk SIP in uso nell'organizzazione:
    
        Get-CsTrunk

## Visualizzazione delle informazioni relative a un trunk SIP specifico

  - Questo comando restituisce informazioni solo sul trunk SIP con l'identità (Identity) PstnGateway:192.168.0.240:
    
        Get-CsTrunk -Identity "PstnGateway:192.168.0.240"

## Visualizzazione delle informazioni relative a tutti i trunk SIP assegnati a un pool

  - In questo esempio vengono restituite le informazioni su tutti i trunk SIP assegnati al pool atl-cs-001.litwareinc.com:
    
        Get-CsTrunk -PoolFqdn "atl-cs-001.litwareinc.com"

