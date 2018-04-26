---
title: Configurazione di VoIP aziendale in Lync Server 2013
TOCTitle: Configurazione di VoIP aziendale in Lync Server 2013
ms:assetid: 7df179fa-d3a2-4b23-a433-b750aedf980b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994041(v=OCS.15)
ms:contentKeyID: 52062186
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per distribuire VoIP aziendale, sarà necessario configurare quanto segue:

  - Creare un trunk

  - Definire criteri vocali

  - Definire route vocali

  - Abilitare gli utenti per VoIP aziendale

## Creare un trunk

È necessario definire i trunk nella distribuzione del VoIP aziendale. Per il routing in base alla posizione è necessario creare una configurazione per ogni singolo trunk. Utilizzare lo strumento Generatore di topologie di Lync Server per definire i trunk e il comando New-CsTrunkConfiguration di Windows PowerShell per Lync Server oppure Pannello di controllo di Lync Server per definire le configurazioni di trunk corrispondenti. Per ulteriori informazioni su come abilitare il routing in base alla posizione in configurazioni di trunk, vedere la sezione corrispondente nell'argomento [Abilitazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-enabling-location-based-routing.md). Per questo esempio nella tabella seguente sono illustrati i trunk utilizzati in questo scenario.

Per ulteriori informazioni, vedere [Definire ulteriori trunk in Generatore di topologie in Lync Server 2013](lync-server-2013-define-additional-trunks-in-topology-builder.md).


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del trunk</th>
<th>Tipo di sistema</th>
<th>Nome</th>
<th>Posizione</th>
<th>Mediation Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Trunk 1 DEL-GW</p></td>
<td><p>Gateway PSTN</p></td>
<td><p>DEL-GW</p></td>
<td><p>Delhi</p></td>
<td><p>MS1</p></td>
</tr>
<tr class="even">
<td><p>Trunk 2 HYD-GW</p></td>
<td><p>Gateway PSTN</p></td>
<td><p>HYD-GW</p></td>
<td><p>Hyderabad</p></td>
<td><p>MS1</p></td>
</tr>
<tr class="odd">
<td><p>Trunk 3 DEL-PBX</p></td>
<td><p>PBX</p></td>
<td><p>DEL-PBX</p></td>
<td><p>Delhi</p></td>
<td><p>MS1</p></td>
</tr>
<tr class="even">
<td><p>Trunk 4 HYD-PBX</p></td>
<td><p>PBX</p></td>
<td><p>HYD-PBX</p></td>
<td><p>Hyderabad</p></td>
<td><p>MS1</p></td>
</tr>
</tbody>
</table>



## Definire criteri vocali

È necessario definire i criteri vocali per l'implementazione del VoIP aziendale. La definizione di un criterio vocale consente di applicare restrizioni per il routing in base alla posizione a un sottoinsieme di utenti se solo un sottoinsieme deve utilizzare tale tipo di routing. Per questo esempio nella tabella seguente sono illustrati i criteri vocali utilizzati in questo scenario. A titolo di esempio la tabella include solo le impostazioni specifiche del routing in base alla posizione.

Per ulteriori informazioni, vedere [Configurazione di criteri vocali e record utilizzo PSTN per autorizzare privilegi e funzionalità di chiamata in Lync Server 2013](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md).


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
<td><p>False</p></td>
<td><p>False</p></td>
</tr>
</tbody>
</table>



## Definire route vocali

È necessario definire le route vocali per l'implementazione del VoIP aziendale. Per questo esempio nella tabella seguente sono illustrate le route vocali utilizzate in questo scenario. A titolo di esempio la tabella include solo le impostazioni specifiche del routing in base alla posizione.

Per ulteriori informazioni, vedere [Configurazione di route vocali per le chiamate in uscita in Lync Server 2013](lync-server-2013-configuring-voice-routes-for-outbound-calls.md).


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Route vocale 1</th>
<th>Route vocale 2</th>
<th>Route vocale 3</th>
<th>Route vocale 4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome</p></td>
<td><p>Delhi route</p></td>
<td><p>Hyderabad route</p></td>
<td><p>PBX Del route</p></td>
<td><p>PBX Hyd route</p></td>
</tr>
<tr class="even">
<td><p>Utilizzi PSTN</p></td>
<td><p>Delhi usage</p></td>
<td><p>Hyderabad usage</p></td>
<td><p>PBX Del usage</p></td>
<td><p>PBX Hyd usage</p></td>
</tr>
<tr class="odd">
<td><p>Trunk</p></td>
<td><p>Trunk 1 DEL-GW</p></td>
<td><p>Trunk 2 HYD-GW</p></td>
<td><p>Trunk 3 DEL-PBX</p></td>
<td><p>Trunk 4 HYD-PBX</p></td>
</tr>
</tbody>
</table>



## Abilitare gli utenti per VoIP aziendale

Abilitare gli utenti per VoIP aziendale e assegnare loro un criterio vocale definito in precedenza. Per questo esempio nella tabella seguente è illustrata l'assegnazione utilizzata in questo scenario. A titolo di esempio la tabella include solo le impostazioni specifiche del routing in base alla posizione.

Per ulteriori informazioni, vedere [Abilitare gli utenti per VoIP aziendale in Lync Server 2013](lync-server-2013-enable-users-for-enterprise-voice.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Utenti di Delhi</th>
<th>Utenti di Hyderabad</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Criterio vocale associato</p></td>
<td><p>Delhi voice policy</p></td>
<td><p>Hyderabad voice policy</p></td>
</tr>
<tr class="even">
<td><p>Utenti di esempio</p></td>
<td><p>DEL-LYNC-1,DEL-LYNC-2,DEL-LYNC-3</p></td>
<td><p>HYD-LYNC-1, HYD-LYNC-2, HYD-LYNC-3</p></td>
</tr>
</tbody>
</table>



## Vedere anche

#### Ulteriori risorse

[Configurazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-configuring-location-based-routing.md)

