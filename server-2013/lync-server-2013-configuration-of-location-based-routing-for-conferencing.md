---
title: 'Lync Server 2013: configurazione del routing in base alla posizione per le conferenze'
TOCTitle: Configurazione del routing in base alla posizione per le conferenze
ms:assetid: d8c708cc-a1b1-48b1-808c-a64df15f7701
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362846(v=OCS.15)
ms:contentKeyID: 56269989
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del routing in base alla posizione per le conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-09-29_

L'applicazione per conferenze con routing in base alla posizione si basa sulla configurazione del routing in base alla posizione di Lync Server 2013. Le configurazioni principali sono le seguenti:

  - La posizione dei partecipanti a una riunione viene determinata in base al relativo sito di rete. Per applicare il routing in base alla posizione è necessario definire un sito di rete e le subnet associate in Lync Server.

  - Per applicare il routing in base alla posizione delle riunioni, i partecipanti di Lync devono essere abilitati per questa funzionalità.

  - Per applicare il routing in base alla posizione degli endpoint PSTN che partecipano alle riunioni, il trunk SIP usato per connettere gli endpoint PSTN deve essere configurato per questa funzionalità.

Per altre informazioni sulla distribuzione e la configurazione del routing in base alla posizione in Lync Server 2013, vedere [Configurazione del routing in base alla posizione](lync-server-2013-configuring-location-based-routing.md).

## Abilitazione dell'applicazione per conferenze con routing in base alla posizione

L'applicazione per conferenze con routing in base alla posizione è disabilitata per impostazione predefinita. Prima di abilitarla, è necessario determinare la corretta priorità da assegnare all'applicazione. Per determinare la priorità, eseguire il cmdlet seguente in Lync Server Management Shell:

Get-CsServerApplication -Identity Service:Registrar:\<Pool FQDN\>

In questo cmdlet, \<Pool FQDN\> è il pool in cui l'applicazione per conferenze con routing in base alla posizione deve essere abilitata.

Questo cmdlet restituisce l'elenco delle applicazioni ospitate da Lync Server e il valore di priorità di ciascuna. All'applicazione per conferenze con routing in base alla posizione deve essere assegnato un valore di priorità maggiore di quello dell'applicazione "UdcAgent" e minore di quello delle applicazioni "DefaultRouting", "ExumRouting" e "OutboundRouting". È consigliabile assegnarle un valore di priorità di un punto superiore al valore di priorità dell'applicazione "UdcAgent".

Ad esempio, se il valore di priorità è "2" per l'applicazione "UdcAgent", "8" per l'applicazione "DefaultRouting", "9" per l'applicazione "ExumRouting" e "10" per l'applicazione "OutboundRouting", è necessario assegnare all'applicazione per conferenze con routing in base alla posizione un valore di priorità pari a "3". In questo modo le applicazioni risultano ordinate in base alla priorità seguente: altre applicazioni (priorità: 0-1), "UdcAgent" (priorità: 2), applicazione per conferenze con routing in base alla posizione (priorità: 3), altre applicazioni (priorità: 4-8), "DefaultRouting" (priorità: 9), "ExumRouting" (priorità: 10) e "OutboundRouting" (priorità: 11).

Dopo aver trovato il valore di priorità corretto per l'applicazione per conferenze con routing in base alla posizione, digitare il cmdlet seguente per ogni pool Front End o server Standard Edition che ospita utenti abilitati per il routing in base alla posizione:

New-CsServerApplication -Identity Service:Registrar:\<Pool FQDN\>/LBRouting -Priority \<Application Priority\> -Enabled $true -Critical $true -Uri http://www.microsoft.com/LCS/LBRouting

Ad esempio:

New-CsServerApplication -Identity Service:Registrar:LS2013CU2LBRPool.contoso.com/LBRouting -Priority 3 -Enabled $true -Critical $true -Uri http://www.microsoft.com/LCS/LBRouting

Dopo aver eseguito il cmdlet, riavviare tutti i server front-end nel pool o i server Standard Edition in cui è stata abilitata l'applicazione per conferenze con routing in base alla posizione.

> [!IMPORTANT]  
> Il routing in base alla posizione non viene applicato alle conferenze o ai trasferimenti con consultazione finché non vengono riavviati tutti i server Standard Edition o i server front-end nei pool interessati. Se <strong>–Critical</strong> viene impostato su <strong>$true</strong> nei cmdlet precedenti, i servizi di Lync verranno riavviati immediatamente. Se non si desidera che questi servizi vengano riavviati immediatamente, impostare momentaneamente <strong>–Critical</strong> su <strong>$false</strong> e utilizzare <strong>Set-CsServerApplication</strong> per modificare il valore di <strong>-Critical</strong> in <strong>$true</strong> in un secondo momento, in seguito al riavvio dei servizi.

Dopo avere abilitato l'applicazione per conferenze con routing in base alla posizione e riavviato tutti i server Lync applicabili, tutte le conferenze organizzate da utenti di Lync abilitati per il routing in base alla posizione vengono monitorate allo scopo di impedire il bypass delle chiamate a tariffa PSTN.

