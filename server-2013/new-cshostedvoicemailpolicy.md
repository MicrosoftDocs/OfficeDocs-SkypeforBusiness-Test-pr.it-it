---
title: New-CsHostedVoicemailPolicy
TOCTitle: New-CsHostedVoicemailPolicy
ms:assetid: 81e1ec62-45c4-49ad-8e2b-3568c092b6c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398653(v=OCS.15)
ms:contentKeyID: 49301154
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsHostedVoicemailPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio di segreteria telefonica ospitata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsHostedVoicemailPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Destination <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Organization <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando crea un nuovo criterio di segreteria telefonica ospitata denominato ExRedmond. L'assenza dell'ambito indica che il criterio può essere assegnato a singoli utenti o contatti. Questo criterio definisce come destinazione della Messaggistica unificata di Exchange il nome di dominio completo ExUM.fabrikam.com. Gli utenti di Lync Server del criterio possono inoltre essere suddivisi nelle organizzazioni corp1 e corp2 di litwareinc. Il valore del parametro Description di questo criterio è "Hosted voice mail property for Redmond users".

    New-CsHostedVoicemailPolicy -Identity ExRedmond -Destination ExUM.fabrikam.com -Description "Hosted voicemail policy for Redmond users." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"

## Esempio 2

I comandi mostrati nell'esempio 2 sono una variante del comando mostrato nell'esempio 1. In questo caso, tuttavia, i nuovi criteri segreteria telefonica ospitata sono assegnati al tenant Lync Online con ID tenant 73d355dd-ce5d-4ab9-bf49-7b822c18dd98. Per creare un nuovo criterio per un tenant Lync Online, è necessario includere il parametro InMemory e archiviare il criterio risultante in una variabile. Questo è quanto accade nel primo comando, con il nuovo criterio archiviato in una variabile denominata $x. Si noti inoltre che è necessario impostare l'identità su Global e il parametro Tenant sull'ID tenant appropriato.

Per creare il nuovo criterio, il secondo comando chiama quindi il cmdlet **Set-CsHostedVoiceMailPolicy** insieme al parametro Instance e al parametro Tenant.

    $x = New-CsHostedVoiceMailPolicy -Identity global -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98" -Destination ExUM.fabrikam.com -Description "Hosted voicemail policy for Redmond users." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"
    Set-CsHostedVoiceMailPolicy -Instance $x -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98"

## Descrizione dettagliata

Questo cmdlet crea un criterio che configura un account utente abilitato per Lync Server o Office Communications Server all'utilizzo di un servizio di segreteria telefonica ospitato della Messaggistica unificata di Exchange. Il criterio specifica come instradare le chiamate senza risposta di un utente a un servizio di Messaggistica unificata di Exchange ospitato.

Affinché il criterio abbia effetto deve esistere un utente abilitato per la segreteria telefonica ospitata di Messaggistica unificata di Exchange. È possibile chiamare il cmdlet **Get-CsUser** e controllare la proprietà HostedVoiceMail per determinare se esiste un utente abilitato per la segreteria telefonica ospitata. Il valore True indica che l'utente è abilitato.

I criteri creati nell'ambito del sito vengono automaticamente assegnati agli utenti residenti in questi siti. I criteri creati con ambito per utente devono essere assegnati agli utenti o agli oggetti contatto utilizzando il cmdlet **Grant-CsHostedVoicemailPolicy**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsHostedVoicemailPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsHostedVoicemailPolicy"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco per il criterio, che include l'ambito e il sito (per un criterio di sito, come site:Redmond) oppure il nome del criterio (nel caso di un criterio per utente, come RenoHostedVoicemail). Un criterio globale sarà sempre esistente e non potrà essere rimosso, pertanto non è possibile creare un criterio globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione di facile comprensione del criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Destination</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il valore assegnato a questo parametro è il nome di dominio completo (FQDN) del servizio di Messaggistica unificata di Exchange ospitato. La destinazione scelta deve essere attendibile per il routing.</p>
<p>Questo parametro è facoltativo, ma se si tenta di abilitare un utente per la segreteria telefonica ospitata e il criterio assegnato all'utente non dispone di un valore Destination, l'abilitazione avrà esito negativo.</p>
<p>Questo valore deve contenere al massimo 255 caratteri e deve avere la forma di un nome di dominio completo (FQDN), ad esempio server.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di eliminare qualsiasi richiesta di conferma altrimenti visualizzata prima di apportare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Organization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro include un elenco separato da virgole dei tenant Exchange che contengono gli utenti di Lync Server. Ogni tenant deve essere specificato come nome di dominio completo del tenant nel servizio Exchange ospitato.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per cui vengono creati i nuovi criteri segreteria telefonica ospitata, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID tenant per ciascun tenant eseguendo questo comando:</p>
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

Nessuno.

## Tipi restituiti

Questo cmdlet consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy.

## Vedere anche

#### Ulteriori risorse

[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

