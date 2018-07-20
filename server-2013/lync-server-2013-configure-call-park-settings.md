---
title: Configurare le impostazioni del parcheggio di chiamata in Lync Server 2013
TOCTitle: Configurare le impostazioni del parcheggio di chiamata in Lync Server 2013
ms:assetid: 3bed9d09-8363-4fff-a220-f0f6d3a81241
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425886(v=OCS.15)
ms:contentKeyID: 49300268
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le impostazioni del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile personalizzare le impostazioni predefinite di Parcheggio di chiamata. Quando si installa applicazione Parcheggio di chiamata, le impostazioni globali sono configurate per impostazione predefinita. È possibile modificarle, nonché specificare impostazioni specifiche del sito. Usare il cmdlet **New-CsCpsConfiguration** per creare nuove impostazioni specifiche del sito. Usare il cmdlet **Set-CsCpsConfiguration** per modificare le impostazioni esistenti.


> [!NOTE]
> È consigliabile configurare come minimo l'opzione <STRONG>OnTimeoutURI</STRONG> per la destinazione di fallback da utilizzare quando si verifica il timeout di una chiamata parcheggiata e la richiamata ha esito negativo.



Usare il cmdlet **New-CsCpsConfiguration** o il cmdlet **Set-CsCpsConfiguration** per configurare una delle impostazioni seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Opzione:</th>
<th>Descrizione:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CallPickupTimeoutThreshold</strong></p></td>
<td><p>Specifica quanto tempo deve trascorrere dopo che una chiamata è stata parcheggiata prima che squilli sul telefono da cui è stata effettuata la risposta.</p>
<p>Il valore deve essere immesso nel formato hh:mm:ss per specificare le ore, i minuti e i secondi. Il valore minimo è 10 secondi e il valore massimo è 10 minuti. Il valore predefinito è 00:01:30.</p></td>
</tr>
<tr class="even">
<td><p><strong>EnableMusicOnHold</strong></p></td>
<td><p>Specifica se viene riprodotto un brano musicale per il chiamante mentre una chiamata è parcheggiata.</p>
<p>I valori consentiti sono True o False. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCallPickupAttempts</strong></p></td>
<td><p>Specifica per una chiamata parcheggiata il numero di squilli sul telefono da cui è stata effettuata la risposta prima che la chiamata venga inoltrata all'URI (Uniform Resource Identifier) di fallback indicato per <strong>OnTimeoutURI</strong>. Il valore predefinito è 1.</p></td>
</tr>
<tr class="even">
<td><p><strong>OnTimeoutURI</strong></p></td>
<td><p>Specifica l'indirizzo SIP dell'utente o del Response Group a cui viene instradata una chiamata parcheggiata senza risposta quando viene superato il valore specificato per <strong>MaxCallPickupAttempts</strong>.</p>
<p>Il valore deve essere un URI SIP che inizia con la stringa sip:, ad esempio sip:bob@contoso.com. Per impostazione predefinita, non viene specificato un indirizzo di inoltro.</p></td>
</tr>
</tbody>
</table>


## Per configurare le impostazioni di Parcheggio di chiamata

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente:
    
        New-CsCpsConfiguration -Identity site:<sitename to apply settings> [-CallPickupTimeoutThreshold <hh:mm:ss>] -[EnableMusicOnHold <$true | $false>] [-MaxCallPickupAttempts <number of rings>] [-OnTimeoutURI sip:<sip URI for routing unanswered call>]
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Utilizzare il cmdlet <strong>Get-CsSite</strong> per identificare il sito. Per informazioni dettagliate, vedere la documentazione relativa a Lync Server Management Shell.</td>
    </tr>
    </tbody>
    </table>
    
    Ad esempio:
    
        New-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:01:00 -EnableMusicOnHold $false -MaxCallPickupAttempts 2 -OnTimeoutURI sip:bob@contoso.com

## Vedere anche

#### Attività

[Personalizzare la musica di attesa del parcheggio di chiamata in Lync Server 2013](lync-server-2013-customize-call-park-music-on-hold.md)  

#### Ulteriori risorse

[New-CsCpsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCpsConfiguration)  
[Set-CsCpsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCpsConfiguration)  
[Get-CsSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsSite)

