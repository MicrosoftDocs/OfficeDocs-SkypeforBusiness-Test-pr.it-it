---
title: Popolare il database delle posizioni
TOCTitle: Popolare il database delle posizioni
ms:assetid: fb84f5b6-c991-4893-bdbf-f195b4b7d28e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413069(v=OCS.15)
ms:contentKeyID: 49302551
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Popolare il database delle posizioni

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per individuare automaticamente i client in una rete è necessario innanzitutto popolare il database delle posizioni con una *mappa delle posizioni (wiremap)* che esegue il mapping tra gli elementi di rete e gli indirizzi civici. È possibile utilizzare subnet, punti di accesso wireless, switch e porte per definire la mappa delle posizioni (wiremap).

È possibile aggiungere indirizzi al database delle posizioni singolarmente o in massa utilizzando un file CSV contenente i formati di colonna descritti nella tabella seguente.

Se si utilizza un gateway ELIN (Emergency Location Identification Number), includere ELIN nel campo **CompanyName** di ogni posizione. È possibile includere più ELIN per ogni posizione, ognuno separato da un punto e virgola.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento di rete</th>
<th>Colonne richieste</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Punto di accesso wireless</strong></p></td>
<td><p>&lt;BSSID&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,&lt;PreDirectional&gt;,…</p>
<p>…&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
<tr class="even">
<td><p><strong>Subnet</strong></p></td>
<td><p>&lt;Subnet&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,&lt;PreDirectional&gt;,…</p>
<p>…&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
<tr class="odd">
<td><p><strong>Port</strong></p></td>
<td><p>&lt;ChassisID&gt;,&lt;PortIDSubType&gt;,&lt;PortID&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,…</p>
<p>…&lt;PreDirectional&gt;,&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
<tr class="even">
<td><p><strong>Switch</strong></p></td>
<td><p>&lt;ChassisID&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,&lt;PreDirectional&gt;,…</p>
<p>…&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
</tbody>
</table>


Se non si popola il database delle posizioni e **Location Required** nei criteri percorso è impostato su **Yes** o **Disclaimer**, il client richiederà all'utente di immettere manualmente una posizione.

Per informazioni dettagliate sul database delle posizioni, vedere la documentazione di Lync Server Management Shell per i seguenti cmdlet:

  - **Get-CsLisSubnet**

  - **Set-CsLisSubnet**

  - Remove-CsLisSubnet

  - **Get-CsLisWirelessAccessPoint**

  - **Set-CsLisWirelessAccessPoint**

  - **Remove-CsLisWirelessAccessPoint**

  - **Get-CsLisSwitch**

  - **Set-CsLisSwitch**

  - **Remove-CsLisSwitch**

  - **Get-CsLisPort**

  - **Set-CsLisPort**

  - **Remove-CsLisPort**

## Per aggiungere elementi di rete al database delle posizioni

1.  Eseguire il cmdlet seguente per aggiungere una posizione subnet al database delle posizioni.
    
        Set-CsLisSubnet -Subnet 157.56.66.0 -Description "Subnet 1" -Location Location1 -CompanyName "Litware" -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Redmond -State WA -PostalCode 99123 -Country US
    
    Per i gateway ELIN, inserire il gateway ELIN nel campo CompanyName. È possibile includere più di un ELIN. Ad esempio:
    
        Set-CsLisSubnet -Subnet 157.56.66.0 -Description "Subnet 1" -Location Location1 -CompanyName 425-555-0100; 425-555-0200; 425-555-0300 -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Redmond -State WA -PostalCode 99123 -Country US
    
    In alternativa, è possibile eseguire i cmdlet seguenti per l'aggiornamento di massa delle posizioni subnet utilizzando un file denominato "subnets.csv".
    
        $g = Import-Csv subnets.csv
        $g | Set-CsLisSubnet

2.  Eseguire il cmdlet seguente per aggiungere posizioni wireless al database delle posizioni.
    
        Set-CsLisWirelessAccessPoint -BSSID 0A-23-CD-16-AA-2E -Description "Wireless1" -Location Location2 -CompanyName "Litware" -HouseNumber 2345 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Bellevue -State WA -PostalCode 99234 -Country US
    
    In alternativa, è possibile eseguire i cmdlet seguenti per l'aggiornamento di massa delle posizioni wireless utilizzando un file denominato "waps.csv".
    
        $g = Import-Csv waps.csv
        $g | Set-CsLisWirelessAccessPoint

3.  Eseguire il cmdlet seguente per aggiungere posizioni switch al database delle posizioni.
    
        Set-CsLisSwitch-ChassisID 0B-23-CD-16-AA-BB -Description "Switch1" -Location Location1 -CompanyName "Litware" -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Redmond -State WA -PostalCode 99123 -Country US
    
    In alternativa, è possibile eseguire i cmdlet seguenti per l'aggiornamento di massa delle posizioni switch utilizzando un file denominato "switches.csv".
    
        $g = Import-Csv switches.csv
        $g | Set-CsLisSwitch

4.  Eseguire il cmdlet seguente per aggiungere posizioni delle porte al database delle posizioni.
    
        Set-CsLisPort -ChassisID 0C-23-CD-16-AA-CC -PortID 0A-abcd -Description "Port1" -Location Location2 -CompanyName "Litware" -HouseNumber 2345 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Bellevue -State WA -PostalCode 99234 -Country US
    
    L'impostazione predefinita per PortIDSubType è LocallyAssigned. È anche possibile impostare l'opzione su InterfaceAlias o InterfaceName.
    
    In alternativa, è possibile eseguire i cmdlet seguenti per l'aggiornamento di massa delle posizioni porta utilizzando un file denominato "ports.csv".
    
        $g = Import-Csv ports.csv
        $g | Set-CsLisPort

