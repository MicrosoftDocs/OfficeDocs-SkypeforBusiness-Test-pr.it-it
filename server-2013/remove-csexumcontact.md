---
title: Remove-CsExUmContact
TOCTitle: Remove-CsExUmContact
ms:assetid: d79f7082-f58b-4cc3-a90d-230111e32850
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398946(v=OCS.15)
ms:contentKeyID: 49302127
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsExUmContact

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un oggetto contatto Operatore automatico o Accesso sottoscrittore per il servizio Messaggistica unificata di Exchange ospitato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsExUmContact -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimosso il contatto Messaggistica unificata di Exchange con indirizzo SIP exumsa1@fabrikam.com.

    Remove-CsExUmContact -Identity sip:exumsa1@fabrikam.com

## ESEMPIO 2

Questo esempio rimuove tutti i contatti Messaggistica unificata di Exchange con i valori LineURI che iniziano con tel:425. La prima parte di questo comando chiama il cmdlet **Get-CsExUmContact** con il parametro Filter utilizzando questa espressione come filtro: LineURI -like "tel:425\*". Il filtro specifica che si desidera recuperare gli oggetti contatto Messaggistica unificata di Exchange che hanno un valore LineURI che corrisponde alla stringa carattere jolly tel:425\*. In altri termini, tutti gli URI linea che iniziano con la stringa tel:425 e finiscono con qualsiasi insieme di caratteri. Dopo aver raccolto questi oggetti, la raccolta viene inviata tramite pipe al cmdlet **Remove-CsExUmContact** che rimuove tutti gli elementi presenti nella raccolta.

    Get-CsExUmContact -Filter {LineURI -like "tel:425*"} | Remove-CsExUmContact

## Descrizione dettagliata

Lync Server collabora con Messaggistica unificata di Exchange per fornire diverse funzionalità vocali, tra cui Operatore automatico e Accesso sottoscrittore. Quando Messaggistica unificata di Exchange viene fornito come servizio ospitato (anziché locale), è necessario creare oggetti contatto mediante Windows PowerShell per applicare le funzionalità Operatore automatico e Accesso sottoscrittore. Tutti gli oggetti creati possono essere rimossi con il cmdlet **Remove-CsExUmContact**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsExUmContact** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsExUmContact"}

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
<td><p>L'identificatore univoco dell'oggetto contatto che si desidera rimuovere. Le identità dei contatti possono essere specificate utilizzando uno dei quattro formati seguenti: 1) L'indirizzo SIP del contatto; 2) il nome dell'entità utente (UPN) del contatto; 3) il nome del dominio del contatto e il nome di accesso nella forma dominio\accesso (ad esempio, litwareinc\exum1); infine, 4) il nome di visualizzazione Active Directory del contatto (ad esempio, Team Auto Attendant).</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Accetta l'input da pipeline di oggetti contatto di Messaggistica unificata di Exchange.

## Tipi restituiti

Questo cmdlet non restituisce un oggetto. Rimuove un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact.

## Vedere anche

#### Ulteriori risorse

[New-CsExUmContact](new-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

