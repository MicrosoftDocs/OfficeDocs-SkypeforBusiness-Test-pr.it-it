---
title: Processo di distribuzione per la risposta alle chiamate di gruppo
TOCTitle: Processo di distribuzione per la risposta alle chiamate di gruppo
ms:assetid: 082daeac-e667-4e2d-b78d-8e0901f9f0e9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945615(v=OCS.15)
ms:contentKeyID: 52062090
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per la risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione viene fornita una panoramica dei passaggi previsti per la distribuzione della funzionalità di risposta alle chiamate di gruppo. È necessario distribuire Enterprise Edition o Standard Edition con VoIP aziendale prima di configurare la risposta alle chiamate di gruppo. I componenti richiesti da tale funzionalità vengono installati e abilitati quando si distribuisce VoIP aziendale.

### Processo di distribuzione della risposta alle chiamate di gruppo

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Gruppi e ruoli obbligatori</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Abilitare lo strumento SEFAUtil del Resource Kit nella topologia</p></td>
<td><ol>
<li><p>Utilizzare il cmdlet <strong>New-CsTrustedApplicationPool</strong> per creare un nuovo pool di applicazioni attendibili.</p></li>
<li><p>Utilizzare il cmdlet <strong>New-CsTrustedApplication</strong> per specificare lo strumento SEFAUtil come applicazione attendibile.</p></li>
<li><p>Eseguire il cmdlet <strong>Enable-CsTopology</strong> per abilitare la topologia.</p></li>
<li><p>Installare gli strumenti del Resource Kit in un Front End Server situato nel pool di applicazioni attendibili creato nel passaggio 1.</p></li>
<li><p>Verificare la corretta esecuzione di SEFAUtil eseguendolo per visualizzare le impostazioni di inoltro chiamata di un utente nella distribuzione.</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-deploy-the-sefautil-tool.md">Distribuire lo strumento SEFAUtil</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare gli intervalli dei numeri di risposta alle chiamate nella tabella dei codici orbit del parcheggio di chiamata</p></td>
<td><p>Utilizzare il cmdlet <strong>New-CSCallParkOrbit</strong> per creare gli intervalli dei numeri di risposta alle chiamate nella tabella dei codici orbit del parcheggio di chiamata e assegnare il tipo GroupPickup agli intervalli di risposta alle chiamate.</p>
<div class="alert">

> [!NOTE]
> È necessario utilizzare Lync Server Management Shell per creare, modificare, rimuovere e visualizzare gli intervalli dei numeri di risposta alle chiamate di gruppo nella tabella dei codici orbit del parcheggio di chiamata. Gli intervalli dei numeri di risposta alle chiamate di gruppo non sono disponibili in Pannello di controllo di Lync Server.


</div>
<div class="alert">

> [!NOTE]
> Per l'integrazione completa con i dial plan esistenti, gli intervalli dei numeri in genere sono configurati come un blocco di estensioni virtuali. L'assegnazione di numeri DID (Direct Inward Dialing) come numeri di intervallo nella tabella dei codici orbit del parcheggio di chiamata non è supportata.


</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-call-pickup-group-numbers.md">Configurare i numeri per la risposta alle chiamate di gruppo</a></p></td>
</tr>
<tr class="odd">
<td><p>Assegnare agli utenti un numero di risposta alle chiamate e abilitare la risposta alle chiamate di gruppo per gli utenti</p></td>
<td><p>Utilizzare il parametro /enablegrouppickup nello strumento SEFAUtil del Resource Kit per abilitare la risposta alle chiamate di gruppo e assegnare un numero di risposta alle chiamate per gli utenti.</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-enable-group-call-pickup-for-users-and-assign-a-group-number.md">Abilitare la risposta alle chiamate di gruppo per gli utenti e assegnare un numero di gruppo</a></p></td>
</tr>
<tr class="even">
<td><p>Notificare agli utenti il relativo numero di risposta alle chiamate assegnato e altri numeri di interesse</p></td>
<td><p>Poiché qualsiasi utente può recuperare una chiamata fatta a un utente della risposta alle chiamate di gruppo, gli utenti possono monitorare più di un gruppo.</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-communicate-group-call-pickup-assignment-to-users.md">Comunicare l'assegnazione della risposta alle chiamate di gruppo agli utenti</a></p></td>
</tr>
<tr class="odd">
<td><p>Verificare la distribuzione della funzionalità di risposta alle chiamate di gruppo</p></td>
<td><p>Testare la possibilità di eseguire e riprendere le chiamate per verificare che la configurazione funzioni come previsto.</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-optional-verify-the-group-call-pickup-deployment.md">(Facoltativo) Verificare la distribuzione della risposta alle chiamate di gruppo</a></p></td>
</tr>
</tbody>
</table>

