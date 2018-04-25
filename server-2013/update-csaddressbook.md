---
title: Update-CsAddressBook
TOCTitle: Update-CsAddressBook
ms:assetid: 109c5fe7-0154-4161-b19f-01bab024bb3d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398194(v=OCS.15)
ms:contentKeyID: 49299718
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsAddressBook

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Forza la sincronizzazione del contenuto dei server della Rubrica specifici con il database degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Update-CsAddressBook [-Force <SwitchParameter>] [-Fqdn <Fqdn>]

## Esempi

## ESEMPIO 1

In questo esempio viene chiamato il cmdlet **Update-CsAddressBook** senza alcun parametro. In questo modo vengono sincronizzati tutti i server della Rubrica nell'organizzazione.

    Update-CsAddressBook

## ESEMPIO 2

Con l'esempio 2 viene sincronizzato un singolo server della Rubrica, vale a dire il server con il nome di dominio completo atl-abs-001.litwareinc.com.

    Update-CsAddressBook -Fqdn atl-abs-001.litwareinc.com

## Descrizione dettagliata

I server della Rubrica sono intermediari tra Active Directory e Lync Server. Il server della Rubrica garantisce che le informazioni utente archiviate in Lync Server siano sincronizzate con le informazioni utente archiviate in Active Directory. A tale scopo, i file della Rubrica vengono periodicamente sincronizzati con le informazioni archiviate nel database degli utenti. Per impostazione predefinita, la sincronizzazione viene eseguita ogni cinque minuti. È tuttavia possibile modificare questo intervallo di tempo utilizzando il cmdlet **Set-CsAddressBookConfiguration**.

Se non è possibile attendere la sincronizzazione o se, per qualche motivo, sembra che la sincronizzazione non avvenga, è possibile utilizzare il cmdlet **Update-CsAddressBook** per forzare la sincronizzazione immediata di un server della Rubrica con le informazioni utente archiviate nel database degli utenti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Update-CsAddressBook** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsAddressBook"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Fqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare una singola rubrica da aggiornare. Se questo parametro non è presente, tutti i server della Rubrica saranno sincronizzati con il database degli utenti. I singoli server della Rubrica dovrebbero essere referenziati con il loro nome di dominio completo (FQDN), ad esempio atl-abs-001.litwareinc.com.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Update-CsAddressBook** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Update-CsAddressBook** invece aggiorna le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

