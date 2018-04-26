---
title: Abilitazione del routing in base alla posizione in Lync Server 2013
TOCTitle: Abilitazione del routing in base alla posizione in Lync Server 2013
ms:assetid: 029ede7e-0c4e-4ad2-af99-909ae674d6fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994014(v=OCS.15)
ms:contentKeyID: 52062084
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione del routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Dopo la distribuzione del VoIP aziendale e la definizione delle aree di rete, dei siti e delle subnet, è possibile abilitare il routing in base alla posizione. Questa operazione deve essere eseguita per gli elementi del VoIP aziendale seguenti:

  - Siti di rete

  - Configurazioni trunk

  - Criteri vocali

  - Configurazione del routing

## Abilitare il routing in base alla posizione per i siti di rete

Dopo aver distribuito il VoIP aziendale e configurato i siti di rete, è possibile configurare il routing in base alla posizione. A tale scopo, è innanzitutto necessario creare un criterio di routing vocale per associare il sito di rete con gli utilizzi PSTN appropriati. Quando si assegnano utilizzi PSTN a un criterio di routing vocale, assicurarsi di specificare solo gli utilizzi PSTN associati a route vocali che usano un gateway PSTN locale del sito oppure un gateway PSTN che si trova in un'area in cui le limitazioni del routing in base alla posizione non sono necessarie. Per creare criteri di routing vocale, utilizzare il comando New-CsVoiceRoutingPolicy di Lync ServerWindows PowerShell oppure il Pannello di controllo di Lync Server.

    New-CsVoiceRoutingPolicy -Identity <voice routing policy ID> -Name <voice routing policy name> -PstnUsages <usages>

Per ulteriori informazioni, vedere [New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md).

In questo esempio la tabella seguente e i comandi di Windows PowerShell illustrano due criteri di routing vocale con i relativi utilizzi PSTN associati definiti in questo scenario. Nella tabella sono incluse a titolo di esempio solo le impostazioni specifiche del routing in base alla posizione.

    New-CsVoiceRoutingPolicy -Identity "DelhiVoiceRoutingPolicy" -Name "Delhi voice routing policy" -PstnUsages @{add="Delhi usage", "PBX Del usage", "PBX Hyd usage"}
    New-CsVoiceRoutingPolicy -Identity "HyderabadVoiceRoutingPolicy" -Name " Hyderabad voice routing policy" -PstnUsages @{add="Hyderabad usage", "PBX Del usage", "PBX Hyd usage"}


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Criterio di routing vocale 1</th>
<th>Criterio di routing vocale 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID criterio vocale</p></td>
<td><p>Delhi voice routing policy</p></td>
<td><p>Hyderabad voice routing policy</p></td>
</tr>
<tr class="even">
<td><p>Utilizzi PSTN</p></td>
<td><p>Delhi usage, PBX Del usage, PBX Hyd usage</p></td>
<td><p>Hyderabad usage, PBX Hyd usage, PBX Del usage</p></td>
</tr>
</tbody>
</table>

  

Configurare quindi il routing in base alla posizione per i siti di rete pertinenti e associare i criteri di routing vocale a tali siti. Utilizzare il comando New-CsNetworkSite di Lync ServerWindows PowerShell per abilitare il routing in base alla posizione e associare i criteri di routing vocale ai siti di rete che devono applicare le limitazioni del routing.

    Set-CsNetworkSite -Identity <site ID> -EnableLocationBasedRouting <$true|$false> -VoiceRoutingPolicy <voice routing policy ID>

In questo esempio la tabella seguente illustra il routing in base alla posizione per due diversi siti di rete, ovvero Delhi e Hyderabad, definiti in questo scenario mediante Lync ServerWindows PowerShell. Nella tabella sono incluse a titolo di esempio solo le impostazioni specifiche del routing in base alla posizione.

    Set-CsNetworkSite -Identity "Delhi" -EnableLocationBasedRouting $true -VoiceRoutingPolicy "DelhiVoiceRoutingPolicy"
    Set-CsNetworkSite -Identity "Hyderabad" -EnableLocationBasedRouting $true -VoiceRoutingPolicy "HyderabadVoiceRoutingPolicy"


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Sito 1 (Delhi)</th>
<th>Sito 2 (Hyderabad)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome sito</p></td>
<td><p>Sito 1 (Delhi)</p></td>
<td><p>Sito 2 (Hyderabad)</p></td>
</tr>
<tr class="even">
<td><p>EnableLocationBasedRouting</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p>Criterio di routing vocale</p></td>
<td><p>Delhi voice routing policy</p></td>
<td><p>Hyderabad voice routing policy</p></td>
</tr>
<tr class="even">
<td><p>Subnet</p></td>
<td><p>Subnet 1 (Delhi)</p></td>
<td><p>Subnet 2 (Hyderabad)</p></td>
</tr>
</tbody>
</table>



## Abilitare il routing in base alla posizione per i trunk

Prima di poter abilitare una configurazione trunk per il routing in base alla posizione, è necessario creare una configurazione trunk per ogni trunk oppure per ogni sito di rete. A tale scopo, utilizzare il comando New-CsTrunkConfiguration di Lync ServerWindows PowerShell. Se più trunk sono associati a un determinato sistema, ad esempio gateway o PBX, è necessario modificare ogni configurazione trunk per abilitare le limitazioni del routing in base alla posizione.

    New-CsTrunkConfiguration -Identity < trunk configuration ID>

Per ulteriori informazioni, vedere [New-CsTrunkConfiguration](new-cstrunkconfiguration.md).

In questo esempio vengono utilizzati i comandi di Windows PowerShell seguenti per creare una configurazione trunk per ogni trunk della distribuzione definita in questo scenario.

    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 1 DEL-GW>"
    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 2 HYD-GW>"
    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 3 DEL-PBX>"
    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 4 HYD-PBX>"

Dopo aver applicato la configurazione trunk a ogni trunk, è possibile utilizzare il comando Set-CsTrunkConfiguration di Lync ServerWindows PowerShell per abilitare il routing in base alla posizione per i trunk che devono applicare le limitazioni del routing. Abilitare il routing in base alla posizione per i trunk che instradano le chiamate ai gateway PSTN che instradano le chiamate a PSTN e associare il sito di rete in cui si trova il gateway.

    Set-CsTrunkConfiguration -Identity <trunk configuration ID> -EnableLocationRestriction $true -NetworkSiteID <site ID>

Per ulteriori informazioni, vedere [New-CsTrunkConfiguration](new-cstrunkconfiguration.md).

In questo esempio il routing in base alla posizione viene abilitato per ogni trunk associato ai gateway PSTN di Delhi e Hyderabad:

    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 1 DEL-GW -EnableLocationRestriction $true -NetworkSiteID "Delhi"
    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 2 HYD-GW -EnableLocationRestriction $true -NetworkSiteID "Hyderabad"

  

Anche se non è necessario abilitare il routing in base alla posizione per i trunk che non instradano le chiamate a PSTN, il trunk deve essere comunque associato al sito di rete in cui si trova il sistema. Le limitazioni del routing in base alla posizione devono infatti essere applicate per le chiamate PSTN che raggiungono gli endpoint connessi tramite il trunk. In questo esempio il routing in base alla posizione non viene abilitato per tutti i trunk associati ai sistemi PBX di Delhi e Hyderabad:

    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 3 DEL-PBX -EnableLocationRestriction $false -NetworkSiteID "Delhi"
    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 4 HYD-PBX -EnableLocationRestriction $false -NetworkSiteID "Hyderabad"

  
Agli endpoint connessi ai sistemi che non instradano le chiamate a PSTN, ad esempio PBX, verranno applicate limitazioni simili a quelle applicate agli endpoint di Lync per gli utenti abilitati per il routing in base alla posizione. Ciò significa che tali utenti potranno ricevere ed effettuare chiamate da e verso gli utenti Lync indipendentemente dalla loro posizione. Potranno inoltre ricevere ed effettuare chiamate da e verso altri sistemi che non instradano le chiamate alla rete PSTN, ad esempio un endpoint connesso a un altro PBX, indipendentemente dal sito di rete a cui i sistemi sono associati. Tutte le chiamate in ingresso e le chiamate in uscita, nonché tutti i trasferimenti e gli inoltri di chiamata che coinvolgono gli endpoint PSTN saranno soggetti all'applicazione del routing in base alla posizione. Tali chiamate devono utilizzare solo i gateway PSTN definiti come locali in questi sistemi.

Nella tabella seguente viene illustrata la configurazione trunk di quattro trunk in due diversi siti di rete, due connessi ai gateway PSTN e due connessi ai sistemi PBX.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>EnableLocationRestriction</th>
<th>NetworkSiteID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PstnGateway:Trunk 1 DEL-GW</p></td>
<td><p>True</p></td>
<td><p>Sito 1 (Delhi)</p></td>
</tr>
<tr class="even">
<td><p>PstnGateway:Trunk 2 HYD-GW</p></td>
<td><p>True</p></td>
<td><p>Sito 2 (Hyderabad)</p></td>
</tr>
<tr class="odd">
<td><p>PstnGateway:Trunk 3 DEL-PBX</p></td>
<td><p>False</p></td>
<td><p>Sito 1 (Delhi)</p></td>
</tr>
<tr class="even">
<td><p>PstnGateway:Trunk 4 HYD-PBX</p></td>
<td><p>False</p></td>
<td><p>Sito 2 (Hyderabad)</p></td>
</tr>
</tbody>
</table>



## Abilitare il routing in base alla posizione per i criteri vocali

Per applicare il routing in base alla posizione a utenti specifici, è necessario configurare i criteri vocali di tali utenti in modo da impedire il bypass delle chiamate a tariffa PSTN. Utilizzare il comando New-CsVoicePolicy di Lync ServerWindows PowerShell per creare un nuovo criterio vocale oppure utilizzare il comando Set-CsVoicePolicy per un criterio vocale esistente per abilitare il routing in base alla posizione impedendo il bypass delle chiamate a tariffa PSTN.

    Set-CsVoicePolicy -Identity <voice policy ID> -PreventPSTNTollBypass <$true|$false>

Per ulteriori informazioni, vedere [New-CsVoicePolicy](new-csvoicepolicy.md).

In questo esempio la tabella seguente e i comandi di Windows PowerShell illustrano come impedire il bypass delle chiamate a tariffa PSTN per i criteri vocali di Delhi e Hyderabad definiti in questo scenario. Nella tabella sono incluse a titolo di esempio solo le impostazioni specifiche del routing in base alla posizione.

    Set-CsVoicePolicy -Identity "Delhi voice policy" -PreventPSTNTollBypass $true
    Set-CsVoicePolicy -Identity "Hyderabad voice policy" -PreventPSTNTollBypass $true


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Criterio vocale 1</th>
<th>Criterio vocale 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID criterio vocale</p></td>
<td><p>Delhi voice policy</p></td>
<td><p>Hyderabad voice policy</p></td>
</tr>
<tr class="even">
<td><p>Utilizzi PSTN</p></td>
<td><p>Delhi usage, PBX Del usage, PBX Hyd usage</p></td>
<td><p>Hyderabad usage, PBX Hyd usage, PBX Del usage</p></td>
</tr>
<tr class="odd">
<td><p>PreventPSTNTollBypass</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>



## Abilitare il routing in base alla posizione nella configurazione del routing

Infine, abilitare globalmente il routing in base alla posizione nella configurazione del routing. Utilizzare il comando New-CsRoutingConfiguration di Lync ServerWindows PowerShell per abilitare il routing in base alla posizione.

    Set-CsRoutingConfiguration -EnableLocationBasedRouting $true

Per ulteriori informazioni, vedere [Set-CsRoutingConfiguration](set-csroutingconfiguration.md).


> [!NOTE]
> Anche se il routing in base alla posizione deve essere abilitato mediante una configurazione globale, il set di regole verrà applicato solo per i siti, gli utenti e i trunk per cui è stato configurato, come specificato nel presente articolo.




## Vedere anche

#### Ulteriori risorse

[Configurazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-configuring-location-based-routing.md)

