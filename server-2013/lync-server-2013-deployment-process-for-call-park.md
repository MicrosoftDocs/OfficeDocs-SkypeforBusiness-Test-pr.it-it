---
title: 'Lync Server 2013: Processo di distribuzione per il parcheggio di chiamata'
TOCTitle: Processo di distribuzione per il parcheggio di chiamata
ms:assetid: 2000d672-a85f-4262-9d69-0bee9ae3709a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398283(v=OCS.15)
ms:contentKeyID: 49299897
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per il parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione viene fornita una panoramica dei passaggi previsti per la distribuzione dell' applicazione Parcheggio di chiamata. È necessario distribuire Enterprise Edition o Standard Edition con VoIP aziendale prima di configurare Parcheggio di chiamata. I componenti richiesti da Parcheggio di chiamata vengono installati e abilitati quando si distribuisce VoIP aziendale.

### Processo di distribuzione di Parcheggio di chiamata

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
<td><p>Configurare gli intervalli dei codici orbit di parcheggio di chiamata nella tabella dei codici orbit</p></td>
<td><p>Utilizzare il Pannello di controllo di Lync Server o il cmdlet <strong>New-CSCallParkOrbit</strong> per creare gli intervalli dei codici orbit nella tabella dei codici orbit di parcheggio di chiamata e associarli al Servizio applicazione che ospita l' applicazione Parcheggio di chiamata.</p>

> [!NOTE]
> Per l'integrazione completa con i dial plan esistenti, gli intervalli dei codici orbit in genere sono configurati come un blocco di estensioni virtuali. L'assegnazione di numeri Direct Inward Dialing (DID) come numeri di codici orbit nella tabella dei codici orbit di parcheggio di chiamata non è supportata.


</td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-create-or-modify-a-call-park-orbit-range.md">Creare o modificare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare le impostazioni di Parcheggio di chiamata</p></td>
<td><p>Utilizzare il cmdlet <strong>Set-CsCpsConfiguration</strong> per configurare le impostazioni di Parcheggio di chiamata. È consigliabile configurare come minimo l'opzione <strong>OnTimeoutURI</strong> per definire la destinazione di fallback da utilizzare quando si verifica il timeout di una chiamata parcheggiata. È inoltre possibile configurare le impostazioni seguenti:</p>
<ul>
<li><p>(Facoltativo) <strong>EnableMusicOnHold</strong> per abilitare o disabilitare la musica di attesa.</p></li>
<li><p>(Facoltativo) <strong>MaxCallPickupAttempts</strong> per determinare il numero di squilli sul telefono di destinazione di una chiamata parcheggiata prima dell'inoltro all'URI (Uniform Resource Identifier) di fallback.</p></li>
<li><p>(Facoltativo) <strong>CallPickupTimeoutThreshold</strong> per determinare quanto tempo deve trascorrere dopo che una chiamata è stata parcheggiata prima che squilli sul telefono da cui è stata effettuata la risposta.</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-call-park-settings.md">Configurare le impostazioni del parcheggio di chiamata in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Se lo si desidera, personalizzare la musica di attesa</p></td>
<td><p>Utilizzare il cmdlet <strong>Set-CsCallParkServiceMusicOnHoldFile</strong> per personalizzare e caricare un file audio, se non si desidera utilizzare la musica di attesa predefinita.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-customize-call-park-music-on-hold.md">Personalizzare la musica di attesa del parcheggio di chiamata in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurare il criterio vocale per abilitare Parcheggio di chiamata per gli utenti</p></td>
<td><p>Utilizzare il cmdlet Pannello di controllo di Lync Server o <strong>Set-CSVoicePolicy</strong> con l'opzione <strong>EnableCallPark</strong> per abilitare Parcheggio di chiamata per gli utenti nel criterio vocale.</p>

> [!NOTE]
> Per impostazione predefinita, l'applicazione Parcheggio di chiamata è disabilitata per tutti gli utenti.


> [!NOTE]
> Se si dispone di più criteri vocali, verificare che la proprietà EnableCallPark sia impostata per ogni criterio vocale e non solo per quello predefinito.


</td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsUserAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-enable-call-park-for-users.md">Abilitare il parcheggio di chiamata per gli utenti in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Verificare le regole di normalizzazione per Parcheggio di chiamata</p></td>
<td><p>I codici orbit di Parcheggio di chiamata non devono essere normalizzati. Verificare che le regole di normalizzazione non includano alcun intervallo dei codici orbit. Se necessario, creare regole di normalizzazione aggiuntive per impedire che vengano normalizzati i codici orbit.</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-verify-normalization-rules-for-call-park.md">Verificare le regole di normalizzazione per il parcheggio di chiamata in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Verificare la distribuzione di Parcheggio di chiamata</p></td>
<td><p>Testare il parcheggio e la ripresa delle chiamate per assicurarsi che la configurazione funzioni come previsto.</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-optional-verify-call-park-deployment.md">(Facoltativo) Verificare la distribuzione del parcheggio di chiamata in Lync Server 2013</a></p></td>
</tr>
</tbody>
</table>

