---
title: Visualizzazione delle informazioni sulle interfacce di rete
TOCTitle: Visualizzazione delle informazioni sulle interfacce di rete
ms:assetid: e7dbb1ec-62b3-48be-a419-c493df5740e6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721916(v=OCS.15)
ms:contentKeyID: 49887797
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sulle interfacce di rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

## Visualizzazione di informazioni sulle interfacce di rete tramite i cmdlet di Lync Server Management Shell

Per visualizzare informazioni sulle interfacce di rete, è possibile utilizzare Lync Server Management Shell e il cmdlet **Get-CsNetworkInterface**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare informazioni sulle interfacce di rete

  - Per visualizzare informazioni sulle interfacce di rete, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsNetworkInterface
    
    Questo comando restituisce informazioni simili alle seguenti per ogni interfaccia di rete:
    
        Identity              : dc.vdomain.com/Primary/1
        ComputerFqdn          : dc.vdomain.com
        IPAddress             : 0.0.0.0
        IPv6Address           :
        Interface             : Primary
        InterfaceNumber       : 1
        ConfiguredFqdn        :
        ConfiguredIPAddress   :
        ConfiguredIPv6Address :

Per informazioni dettagliate, vedere [Get-CsNetworkInterface](get-csnetworkinterface.md).

