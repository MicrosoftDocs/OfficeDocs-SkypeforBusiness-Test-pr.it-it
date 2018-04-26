---
title: Set-CsHostedVoicemailPolicy
TOCTitle: Set-CsHostedVoicemailPolicy
ms:assetid: 9c47d2a5-356c-4bab-9cef-8346c4b5d99c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412722(v=OCS.15)
ms:contentKeyID: 49301473
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsHostedVoicemailPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio di segreteria telefonica ospitata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsHostedVoicemailPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsHostedVoicemailPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Destination <String>] [-Force <SwitchParameter>] [-Organization <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando consente di modificare la proprietà Destination di un criterio di segreteria telefonica ospitata denominato ExRedmond. Consente di impostare la destinazione Messaggistica unificata di Exchange per questo criterio sul nome di dominio completo ExUM.contoso.com.

    Set-CsHostedVoicemailPolicy -Identity ExRedmond -Destination ExUM.contoso.com

## ESEMPIO 2

Con questo comando viene aggiunto un tenant di Exchange all'elenco con valori separati da virgole di tenant (organizzazioni) per il criterio ExRedmond. Nella prima riga viene utilizzato il cmdlet **Get-CsHostedVoicemailPolicy** per recuperare il criterio con identità (Identity) ExRedmond. La chiamata al cmdlet è inclusa tra parentesi, poiché è necessario innanzitutto recuperare questo criterio. Viene quindi utilizzata la "notazione del punto" per recuperare la proprietà Organization del criterio. La stringa restituita viene salvata nella variabile $a. Nella riga successiva viene utilizzato l'operatore += per aggiungere la stringa assegnata (,corp3.litwareinc.com) alla fine della stringa archiviata nella variabile $a. Si noti la virgola nella stringa assegnata. Poiché Organization è un elenco con valori separati da virgole, se è già presente un valore nell'elenco è necessario che eventuali valori aggiuntivi siano preceduti da una virgola. Infine, nell'ultima riga viene chiamato il cmdlet **Set-CsHostedVoicemailPolicy** e viene assegnata la nuova stringa Organization passando la variabile $a al parametro Organization.

    $a = (Get-CsHostedVoicemailPolicy -Identity ExRedmond).Organization
    $a += ",corp3.litwareinc.com"
    Set-CsHostedVoicemailPolicy -Identity ExRedmond -Organization $a

## Esempio 3

Il comando mostrato nell'esempio 3 modifica la proprietà Destination dei criteri segreteria telefonica ospitata assegnati al tenant Lync Online con l'ID tenant 73d355dd-ce5d-4ab9-bf49-7b822c18dd98.

    Set-CsHostedVoicemailPolicy -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98" -Destination "ExUM.contoso.com"

## Descrizione dettagliata

Questo cmdlet modifica un criterio che configura un account utente abilitato per Lync Server o Microsoft Office Communications Server in modo che possa utilizzare un servizio di segreteria telefonica ospitata della Messaggistica unificata di Exchange. Il criterio specifica come instradare le chiamate senza risposta di un utente a un servizio di Messaggistica unificata di Exchange ospitata.

Affinché il criterio abbia effetto deve esistere un utente abilitato per la segreteria telefonica ospitata di Messaggistica unificata di Exchange. È possibile utilizzare il cmdlet **Get-CsUser** e controllare la proprietà HostedVoiceMail per stabilire se esiste un utente abilitato per la segreteria telefonica ospitata. Il valore True indica che l'utente è abilitato.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsHostedVoicemailPolicy** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsHostedVoicemailPolicy"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione di facile comprensione del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Destination</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il valore assegnato a questo parametro è il nome di dominio completo (FQDN) del servizio di Messaggistica unificata di Exchange ospitata. La destinazione scelta deve essere attendibile per il routing.</p>
<p>Se si tenta di abilitare un utente per la segreteria telefonica ospitata e il criterio assegnato all'utente non ha un valore di Destination, l'abilitazione non andrà a buon fine.</p>
<p>Questo valore deve avere una lunghezza massima di 255 caratteri e deve essere in un formato corrispondente all'espressione regolare ^[a-zA-Z0-9\-_]+(\.[a-zA-Z0-9\-_]+){0,}$. In pratica, deve avere la forma di un nome di dominio completo (FQDN), ad esempio server.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco per il criterio di segreteria telefonica ospitata che si desidera modificare. Questo identificatore include l'ambito (nel caso di un ambito globale), l'ambito e il sito (per un criterio di sito, come. ad esempio, site:Redmond) oppure il nome del criterio (nel caso di un criterio per utente, come, ad esempio, HVUserPolicy).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>HostedVoicemailPolicy</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Questo oggetto deve essere di tipo HostedVoicemailPolicy e può essere recuperato utilizzando il cmdlet <strong>Get-CsHostedVoicemailPolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Organization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro include un elenco separato da virgole dei tenant di Exchange che contengono gli utenti di Lync Server. Ogni tenant deve essere specificato come nome di dominio completo del tenant nel servizio Exchange ospitato.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per il quale viene modificato il criterio di segreteria telefonica ospitata, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy. Accetta input tramite pipeline da oggetti criteri di segreteria telefonica ospitati.

## Tipi restituiti

Questo cmdlet consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

