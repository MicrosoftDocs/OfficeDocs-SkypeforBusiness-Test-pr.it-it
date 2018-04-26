---
title: Install-CsAdServerSchema
TOCTitle: Install-CsAdServerSchema
ms:assetid: 86e13601-7e80-4276-b176-77d9c6e7d55a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398681(v=OCS.15)
ms:contentKeyID: 49301212
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Install-CsAdServerSchema

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Estende lo schema di Active Directory per consentire l'installazione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Install-CsAdServerSchema [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Ldf <String>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene determinato il percorso del file LDF con una lettura delle informazioni dal Registro di sistema, quindi viene utilizzato tale file per aggiornare lo schema di Active Directory.

    Install-CsAdServerSchema

## ESEMPIO 2

Con l'esempio 2, lo schema di Active Directory viene aggiornato con le informazioni recuperate da un file di aggiornamento dello schema presente nella cartella C:\\Schemas. La posizione della cartella viene specificata dal parametro Ldf.

    Install-CsAdServerSchema -Ldf "C:\Schemas"

## Descrizione dettagliata

Sebbene Lync Server archivi la maggior parte delle relative informazioni di configurazione nel proprio database, il software si avvale anche di Servizi di dominio Active Directory come posizione di archiviazione. Ad esempio, le informazioni relative agli utenti sono archiviate come parte dell'account di Active Directory dell'utente. A tale scopo, Lync Server deve archiviare questi valori in attributi che non fanno parte dell'account utente tipico di Active Directory. È pertanto necessario "estendere" lo schema di Active Directory, modificandolo per aggiungere gli attributi personalizzati (e agli altri elementi) richiesti da Lync Server.

Il modo più facile per estendere lo schema di Active Directory consiste nell'utilizzare il cmdlet **Install-CsAdServerSchema**. Il cmdlet **Install-CsAdServerSchema** viene in genere eseguito durante il processo di installazione di Lync Server ma, se necessario, può essere eseguito in qualsiasi momento dagli amministratori. Al termine dell'esecuzione del cmdlet, è possibile utilizzare il cmdlet **Get-CsAdServerSchema** per verificare che lo schema sia stato aggiornato e che Active Directory sia pronto per il passaggio successivo del processo di installazione.

Si noti che durante l'esecuzione, il cmdlet **Install-CsAdServerSchema** deve avere accesso al master schema, il ruolo master operazioni che gestisce le definizioni di oggetti e attributi di Active Directory. Se si esegue il cmdlet **Install-CsAdServerSchema** in un computer diverso dal master schema, il computer che ospita il master schema deve consentire l'accesso remoto al Registro di sistema. In caso contrario, è necessario eseguire il cmdlet **Install-CsAdServerSchema** nel master schema stesso.

Le funzioni eseguite dal cmdlet **Install-CsAdServerSchema** sono simili a quelle svolte dal comando di Microsoft Office Communications Server 2007 R2 seguente:

Lcscmd.exe /forest /action:SchemaPrep /SchemaType:Server

Utenti che possono eseguire questo cmdlet: il cmdlet **Install-CsAdServerSchema** può essere eseguito in locale solo dagli amministratori dello schema di Active Directory nel dominio radice o dagli amministratori locali del computer master schema.

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo (FQDN) di un server di catalogo globale nel dominio in uso. Questo parametro non è necessario se si esegue il cmdlet <strong>Install-CsAdServerSchema</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Install-CsAdServerSchema</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Ldf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso della cartella contenente il file LDF da importare. Il file LDF (LDAP Data Interchange Format) include gli aggiornamenti necessari per lo schema di Active Directory. Se questo parametro non viene incluso, il cmdlet <strong>Install-CsAdServerSchema</strong> ricercherà il file nel percorso di installazione di Lync Server scritto nel Registro di sistema. Il percorso di installazione è generalmente C:\Programmi\Microsoft Lync Server 2010\Deployment\Setup.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ServerSchema.html&quot;</p></td>
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

Nessuno. Il cmdlet **Install-CsAdServerSchema** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Install-CsAdServerSchema** non restituisce valori o oggetti.

## Vedere anche

#### Ulteriori risorse

[Get-CsAdServerSchema](get-csadserverschema.md)

