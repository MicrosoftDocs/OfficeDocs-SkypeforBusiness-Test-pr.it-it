---
title: Set-CsUserServer
TOCTitle: Set-CsUserServer
ms:assetid: f4dd845a-5c78-4455-93eb-722b603ff154
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413026(v=OCS.15)
ms:contentKeyID: 49302488
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare un pool di servizi utente esistente. Tra le altre cose, tale pool fornisce informazioni sulla presenza e facilita la gestione delle conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUserServer [-Identity <XdsGlobalRelativeIdentity>] [-ConfDirManagementWcfTcpPort <UInt16>] [-ConferenceServer <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-McuFactorySipPort <UInt16>] [-UserDatabase <String>] [-UserPinManagementWcfHttpPort <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando indicato nell'esempio 1 consente di modificare la porta McuFactorySipPort per un singolo pool di servizi utente: ovvero, il pool con il parametro Identity UserServer:atl-cs-001.litwareinc.com. In questo esempio la porta viene impostata su 445.

    Set-CsUserServer -Identity "UserServer:atl-cs-001.litwareinc.com" -McuFactorySipPort 445

## ESEMPIO 2

Il comando mostrato nell'esempio 2 è una variante del comando dell'esempio 1. In questo caso, la porta McuFactorySipPort viene però modificata per tutti i pool di servizi utente nell'organizzazione. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsService** e il parametro UserServer per restituire una raccolta di tutti i pool di servizi utente attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che individua ciascun pool della raccolta e imposta McuFactorySipPort su 445. I dati devono essere inviati tramite pipe al cmdlet **ForEach-Object**, in quanto il cmdlet **Set-CsUserServer** non può accettare direttamente i dati da pipeline.

    Get-CsService -UserServer | ForEach-Object {Set-CsUserServer -Identity $_.Identity -McuFactorySipPort 445}

## Descrizione dettagliata

I servizi utente sono un componente completo per l'esecuzione di diversi ruoli chiave di Lync Server. Ad esempio, forniscono informazioni sulla presenza, consentono di gestire le conferenze mediante Focus e Focus Factory, gestiscono l'autorizzazione degli utenti e il routing a livello utente e fungono da interfaccia principale per il database di back-end. I servizi utente consentono inoltre di eseguire il provisioning degli account utente.

Per questo motivo, è importante per gli amministratori sapere esattamente come sono stati configurati i pool di servizi utente e, se necessario, modificare tali configurazioni. È possibile recuperare le informazioni sui pool di servizi utente utilizzando questo comando:

Get-CsService -UserServer

Analogamente, è possibile utilizzare il cmdlet **Set-CsUserServer** per apportare modifiche a questi pool. Il cmdlet **Set-CsUserServer** consente agli amministratori di cambiare il database degli utenti e/o il server per conferenze associato a un pool. Questo cmdlet consente inoltre di modificare la porta utilizzata per le connessioni a Focus Factory.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsUserServer** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserServer"}

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
<td><p><em>ConfDirManagementWcfTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta Windows Communication Foundation (WCF) utilizzata per la gestione delle directory conferenze. Il valore predefinito è 9001.</p></td>
</tr>
<tr class="even">
<td><p><em>ConferenceServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'ID servizio del server per conferenze associato al pool di servizi utente. Ad esempio: -ConferenceServer &quot;ConferenceServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco per il pool di servizi utente da modificare. Ad esempio: -Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>È possibile omettere il prefisso &quot;UserServer:&quot; quando si specifica un server utente. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>McuFactorySipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per la connessione a Focus Factory (McuFactory). Focus Factory alloca unità MCU (Media Control Unit) per aggiungere tipi di elementi multimediali specifici, come l'audio, alle conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'ID di servizio per il database degli utenti associato al pool di servizi utente. Ad esempio: -UserDatabase &quot;UserDatabase:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>UserPinManagementWcfHttpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata da Windows Communication Foundation (WCF) per la gestione di PIN utente. Il valore predefinito è 443.</p></td>
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

Nessuno. Il cmdlet **Set-CsUserServer** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsUserServer** non restituisce alcun oggetto o valore. In realtà il cmdlet modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayUserServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

