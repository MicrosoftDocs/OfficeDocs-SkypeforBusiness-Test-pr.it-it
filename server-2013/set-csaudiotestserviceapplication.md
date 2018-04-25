---
title: Set-CsAudioTestServiceApplication
TOCTitle: Set-CsAudioTestServiceApplication
ms:assetid: d2c6880b-58df-43d1-9f26-d2b9f54d3f0b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398907(v=OCS.15)
ms:contentKeyID: 49302056
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAudioTestServiceApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare i valori di proprietà per i contatti dell'applicazione di servizio test audio attualmente in uso nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAudioTestServiceApplication -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-Enabled <$true | $false>] [-EnabledForFederation <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrimaryLanguage <String>] [-SecondaryLanguages <MultiValuedProperty>] [-SipAddress <String>] [-Type <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 la lingua principale per il contatto del servizio di test audio sip:RedmondAudioTest@litwareinc.com è impostata sull'inglese americano (en-US).

    Set-CsAudioTestServiceApplication -Identity "sip:RedmondAudioTest@litwareinc.com" -PrimaryLanguage "en-US" 

## ESEMPIO 2

Nell'esempio 2 viene annullato il valore della proprietà PrimaryLanguage per il contatto del servizio di test audio sip:RedmondAudioTest@litwareinc.com. A tale scopo, viene incluso il parametro PrimaryLanguage impostandolo su $Null.

    Set-CsAudioTestServiceApplication -Identity "sip:RedmondAudioTest@litwareinc.com" -PrimaryLanguage $Null 

## ESEMPIO 3

Nell'esempio 3 i contatti del servizio di test audio in uso nell'organizzazione vengono configurati per l'utilizzo dell'inglese americano come lingua principale. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsAudioTestServiceApplication** senza alcun parametro per restituire una raccolta dei contatti del servizio di test audio. La raccolta viene quindi inviata tramite pipe a **Set-CsAudioTestServiceApplication**, che imposta l'inglese americano (en-Us) come proprietà PrimaryLanguage per ogni contatto della raccolta.

    Get-CsAudioTestServiceApplication | Set-CsAudioTestServiceApplication -PrimaryLanguage "en-US"

## Descrizione dettagliata

Il servizio di test audio consente agli utenti di Lync Server di testare le connessioni vocali prima di effettuare una chiamata vocale. A tale scopo, gli utenti fanno clic sul pulsante Controlla qualità chiamata che si trova nella scheda Dispositivo audio della finestra di dialogo Opzioni di Lync. Quando un utente fa clic su questo pulsante, verrà effettuata una chiamata al servizio di test audio automatizzato. Questa chiamata riceve una risposta e, dopo la riproduzione di una registrazione introduttiva, al chiamante viene chiesto di registrare un breve messaggio della durata massima di 10 secondi. Questa registrazione verrà quindi riprodotta, consentendo al chiamante di verificare la qualità audio ottenuta con la connessione corrente.

Il servizio di test audio si basa in parte sugli oggetti contatto di Active Directory. Questi oggetti vengono creati automaticamente con l'installazione di Audio Bot. Non è possibile crearli manualmente. Gli amministratori tuttavia possono utilizzare il cmdlet **Get-CsAudioTestServiceApplication** per recuperare informazioni sui diversi contatti del servizio di test attualmente in uso nell'organizzazione. Gli amministratori possono inoltre utilizzare il cmdlet **Set-CsAudioTestServiceApplication** per modificare le proprietà di questi contatti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsAudioTestServiceApplication** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAudioTestServiceApplication"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indirizzo SIP del contatto del servizio di test audio da modificare.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome visualizzato Active Directory dell'oggetto contatto.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Benché sia una proprietà valida, DisplayNumber non viene effettivamente utilizzata con il servizio di test audio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se l'oggetto contatto è stato abilitato o meno per Lync Server. Se questo valore viene impostato su False ($False), il contatto non potrà più accedere a Lync Server. Se il valore viene impostato su True ($True), i privilegi di accesso del contatto verranno riabilitati.</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledForFederation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se questo contatto è disponibile per gli utenti di un dominio federato. Se impostato su False, solo gli utenti all'interno dell'organizzazione avranno accesso al contatto.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se l'oggetto contatto è stato abilitato per VoIP aziendale, ovvero l'implementazione Microsoft di VoIP (Voice over Internet Protocol). Con VoIP aziendale, gli utenti possono effettuare telefonate via Internet anziché utilizzare la rete telefonica standard.</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica la posizione in cui vengono archiviate le sessioni di messaggistica istantanea del contatto. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Benché sia una proprietà valida, LineUri non viene effettivamente utilizzata con il servizio di test audio.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto utente attraverso la pipeline che rappresenta l'utente a cui viene assegnato il criterio. Per impostazione predefinita, il cmdlet <strong>Set-CsAudioTestServiceApplication</strong> non passa oggetti attraverso la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Lingua principale utilizzata per il servizio di test audio. La lingua deve essere configurata utilizzando uno dei codici lingua consentiti, ad esempio en-US per l'inglese americano, fr-FR per il francese e così via. Per restituire un elenco dei codici lingua disponibili, al prompt di Windows PowerShell digitare il seguente comando:</p>
<p>Get-CsDialInConferencingLanguageList | Select-Object -ExpandProperty Languages.</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Benché sia una proprietà valida, SecondaryLanguages non viene effettivamente utilizzata con il servizio di test audio.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro è attualmente disabilitato. Non è possibile modificare l'indirizzo SIP con Set-CsAudioTestServiceApplication.</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tipo di contatto di test da distribuire. Per impostazione predefinita, i contatti vengono elencati come Automaton, il che significa che possono interagire con i chiamanti.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsAudioTestServiceApplication** accetta le istanze da pipeline dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Tipi restituiti

Il cmdlet **Set-CsAudioTestServiceApplication** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Get-CsAudioTestServiceApplication](get-csaudiotestserviceapplication.md)

