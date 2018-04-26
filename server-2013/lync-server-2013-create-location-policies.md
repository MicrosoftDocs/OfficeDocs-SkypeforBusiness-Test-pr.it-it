---
title: Creare criteri percorso in Lync Server 2013
TOCTitle: Creare criteri percorso in Lync Server 2013
ms:assetid: f1878194-c756-4794-8fa1-15dd2118b4b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413006(v=OCS.15)
ms:contentKeyID: 49302443
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare criteri percorso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In Lync Server viene utilizzato un criterio percorso per abilitare i client di Lync all'utilizzo del servizio E9-1-1 durante la registrazione. I criteri percorso contengono le impostazioni che definiscono la modalità di implementazione di E9-1-1.

È possibile modificare i criteri percorso globali e creare nuovi criteri percorso contrassegnati. Un client ottiene criteri globali quando non si trova in una subnet con criteri percorso associati oppure quando non è stato assegnato direttamente a criteri percorso. I criteri contrassegnati vengono assegnati a subnet o a utenti.

Per creare criteri percorso, è necessario utilizzare un account membro del gruppo RTCUniversalServerAdmins o del ruolo amministrativo CsVoiceAdministrator oppure che disponga di equivalenti diritti e autorizzazioni di amministratore.

Per una descrizione completa dei criteri percorso, vedere [Definizione di criteri percorso per Lync Server 2013](lync-server-2013-defining-the-location-policy.md). I cmdlet di questa procedura utilizzano criteri percorso definiti con i valori seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Valore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EnhancedEmergencyServicesEnabled</p></td>
<td><p><strong>True</strong></p></td>
</tr>
<tr class="even">
<td><p>LocationRequired</p></td>
<td><p><strong>Dichiarazione di non responsabilità</strong></p></td>
</tr>
<tr class="odd">
<td><p>EnhancedEmergencyServiceDisclaimer</p></td>
<td><p>È necessario impostare un percorso per il criterio aziendale. Se non si imposta un percorso, in caso di emergenza non sarà possibile essere individuati dai servizi di emergenza. Impostare un percorso.</p></td>
</tr>
<tr class="even">
<td><p>UseLocationForE911Only</p></td>
<td><p><strong>False</strong></p></td>
</tr>
<tr class="odd">
<td><p>PstnUsage</p></td>
<td><p><strong>EmergencyUsage</strong></p></td>
</tr>
<tr class="even">
<td><p>EmergencyDialString</p></td>
<td><p><strong>911</strong></p></td>
</tr>
<tr class="odd">
<td><p>EmergencyDialMask</p></td>
<td><p><strong>112</strong></p></td>
</tr>
<tr class="even">
<td><p>NotificationUri</p></td>
<td><p><strong>sip:security@litwareinc.com</strong></p></td>
</tr>
<tr class="odd">
<td><p>ConferenceUri</p></td>
<td><p><strong>sip:+14255550123@litwareinc.com</strong></p></td>
</tr>
<tr class="even">
<td><p>ConferenceMode</p></td>
<td><p><strong>twoway</strong></p></td>
</tr>
<tr class="odd">
<td><p>LocationRefreshInterval</p></td>
<td><p><strong>2</strong></p></td>
</tr>
</tbody>
</table>


Per informazioni dettagliate sull'utilizzo di criteri percorso, vedere la documentazione di Lync Server Management Shell relativa ai cmdlet seguenti:

  - New-CsLocationPolicy

  - Get-CsLocationPolicy

  - Set-CsLocationPolicy

  - Remove-CsLocationPolicy

  - Grant-CsLocationPolicy

## Per creare criteri percorso

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.
    

    > [!NOTE]
    > CsLocationPolicy non verrà eseguito correttamente se l'impostazione di <STRONG>PstnUsage</STRONG> non è già stata inserita nell'elenco Global di PstnUsages.



2.  Facoltativamente, eseguire il cmdlet seguente per modificare i criteri percorso globali:
    
        Set-CsLocationPolicy -Identity Global -EnhancedEmergencyServicesEnabled $true -LocationRequired "disclaimer" -EnhancedEmergencyServiceDisclaimer "Your company policy requires you to set a location. If you do not set a location emergency services will not be able to locate you in an emergency. Please set a location." -PstnUsage "emergencyUsage" -EmergencyDialString "911" -ConferenceMode "twoway" -ConferenceUri "sip:+14255550123@litwareinc.com" -EmergencyDialMask "112" NotificationUri "sip:security@litwareinc.com" -UseLocationForE911Only $true -LocationRefreshInterval 2

3.  Eseguire il cmdlet seguente per creare criteri percorso contrassegnati.
    
        New-CsLocationPolicy -Identity Tag:Redmond - EnhancedEmergencyServicesEnabled $true -LocationRequired "disclaimer" -EnhancedEmergencyServiceDisclaimer "Your company policy requires you to set a location. If you do not set a location emergency services will not be able to locate you in an emergency. Please set a location." -UseLocationForE911Only $false -PstnUsage "EmergencyUsage" -EmergencyDialString "911" -EmergencyDialMask "112" -NotificationUri "sip:security@litwareinc.com" -ConferenceUri "sip:+14255550123@litwareinc.com" -ConferenceMode "twoway" -LocationRefreshInterval 2

4.  Eseguire il cmdlet seguente per applicare i criteri percorso creati nel passaggio 3 ai criteri di un utente.
    
        (Get-CsUser | where { $_.Name -match "UserName" }) | Grant-CsLocationPolicy -PolicyName Redmond

