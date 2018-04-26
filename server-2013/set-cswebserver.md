---
title: Set-CsWebServer
TOCTitle: Set-CsWebServer
ms:assetid: 95a7be5b-9e53-40b9-b7b8-3a4bae9c946c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398759(v=OCS.15)
ms:contentKeyID: 49301391
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWebServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica uno o più servizi Server Web utilizzati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsWebServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-Confirm [<SwitchParameter>]] [-ExternalFqdn <Fqdn>] [-ExternalHttpPort <UInt16>] [-ExternalHttpsPort <UInt16>] [-Force <SwitchParameter>] [-InternalFqdn <Fqdn>] [-McxSipExternalListeningPort <UInt16>] [-McxSipPrimaryListeningPort <UInt16>] [-MeetingRoomAdminPortalExternalListeningPort <UInt16>] [-MeetingRoomAdminPortalInternalListeningPort <UInt16>] [-PrimaryHttpPort <UInt16>] [-PrimaryHttpsPort <UInt16>] [-PublishedExternalHttpPort <UInt16>] [-PublishedExternalHttpsPort <UInt16>] [-PublishedPrimaryHttpPort <UInt16>] [-PublishedPrimaryHttpsPort <UInt16>] [-ReachExternalPsomServerPort <UInt16>] [-ReachPrimaryPsomServerPort <UInt16>] [-RmWebSipExternalListeningPort <UInt16>] [-RmWebSipPrimaryListeningPort <UInt16>] [-SupportConferenceConsoleSipExternalListeningPort <UInt16>] [-SupportConferenceConsoleSipPrimaryListeningPort <UInt16>] [-UcwaSipExternalListeningPort <UInt16>] [-UcwaSipPrimaryListeningPort <UInt16>] [-UserServer <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene modificato PrimaryHttpPort per un singolo pool di servizi Web, quello con identità WebServer:atl-cs-001.litwareinc.com. In questo esempio la porta viene impostata su 89.

    Set-CsWebServer -Identity "WebServer:atl-cs-001.litwareinc.com" -PrimaryHttpPort 89

## ESEMPIO 2

Il comando mostrato nell'esempio 2 è una variante del comando mostrato nell'esempio 1. Questa volta la proprietà PrimaryHttpPort viene modificata per tutti i pool di servizi Web dell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsService** e il parametro WebServer per restituire una raccolta di tutti i pool di servizi Web attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che seleziona ogni pool della raccolta e imposta PrimaryHttpPort sulla porta 89. I dati devono essere inviati tramite pipe al cmdlet **ForEach-Object** in quanto il cmdlet **Set-CsWebServer** non può accettare dati inviati tramite pipeline.

    Get-CsService -WebServer | ForEach-Object {Set-CsWebServer -Identity $_.Identity -PrimaryHttpPort 89}

## Descrizione dettagliata

Lync Server fa ampio uso dei server Web e dei servizi Web. Ad esempio, le query sulla rubrica possono essere eseguite utilizzando i servizi Web (nello specifico, il servizio Web di query sulla Rubrica). Lync Server ospita inoltre le pagine Web che consentono agli utenti di eseguire operazioni come configurare i PIN per le conferenze telefoniche con accesso esterno. Considerando l'importante ruolo svolto da server Web e servizi Web, è fondamentale che gli amministratori sappiano come sono configurati tali server e servizi. Queste informazioni possono essere restituite utilizzando il comando seguente:

Get-CsService -WebServer

Altre volte è fondamentale che gli amministratori siano in grado di cambiare la configurazione dei server Web. Ad esempio, potrebbe essere necessario modificare la porta utilizzata per le connessioni HTTP o HTTPS esterne. Le modifiche alle porte come queste (ma anche altre modifiche) possono essere apportate con il cmdlet **Set-CsWebServer**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsWebServer** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsWebServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero totale di porte allocate per la condivisione delle applicazioni. Le porte effettive da aprire iniziano dalla porta con il valore configurato per AppSharingPortStart e proseguono per il numero di porte specificato in AppSharingPortCount. Ad esempio, se AppSharingPortStart è impostato su 60000 e AppSharingPortCount è impostato su 100, per la condivisione delle applicazioni saranno utilizzate le porte da 60000 a 60099. Il valore predefinito è 16383.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Prima porta nell'intervallo di porte allocato per la condivisione delle applicazioni. Il valore predefinito è 49152.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo utilizzato per le persone che si connettono al pool di servizi Web dall'esterno della rete interna. Ad esempio: -ExternalFqdn &quot;www.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalHttpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta per le connessioni Web esterne effettuate con il protocollo HTTP. Il valore predefinito per la porta è 8080.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalHttpsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta per le connessioni Web esterne effettuate con il protocollo HTTPS. Il valore predefinito per la porta è 4443.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il pool di servizi Web. Ad esempio: -Identity &quot;WebServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>È possibile tralasciare il prefisso &quot;WebServer:&quot; quando si specifica un server Web. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo dei servizi per dispositivi mobili. Il parametro InternalFqdn deve essere accessibile solo dall'interno del firewall dell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>McxSipExternalListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa esterna per il servizio per dispositivi mobili.</p></td>
</tr>
<tr class="odd">
<td><p><em>McxSipPrimaryListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa interna per il servizio per dispositivi mobili.</p></td>
</tr>
<tr class="even">
<td><p><em>MeetingRoomAdminPortalExternalListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa esterna per il portale di amministrazione delle sale riunioni di Lync. Il portale di amministrazione è una utilità basata su Web che consente agli amministratori di gestire facilmente le sale riunioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingRoomAdminPortalInternalListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa interna per il portale di amministrazione delle sale riunioni di Lync. Il portale di amministrazione è una utilità basata su Web che consente agli amministratori di gestire facilmente le sale riunioni.</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryHttpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta per le connessioni Web interne effettuate con il protocollo HTTP. Il valore predefinito per la porta è 80.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryHttpsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta per le connessioni Web interne effettuate con il protocollo HTTPS. Il valore predefinito per la porta è 443.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishedExternalHttpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero della porta HTTP esterna pubblicata.</p></td>
</tr>
<tr class="odd">
<td><p><em>PublishedExternalHttpsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta esterna per il servizio per dispositivi mobili.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishedPrimaryHttpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero della porta HTTP primaria pubblicata.</p></td>
</tr>
<tr class="odd">
<td><p><em>PublishedPrimaryHttpsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta interna per il servizio per dispositivi mobili.</p></td>
</tr>
<tr class="even">
<td><p><em>ReachExternalPsomServerPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero della porta esterna per il protocollo PSOM (Persistent Shared Object Model), un protocollo di Microsoft utilizzato per le conferenze. Il numero di porta predefinito è 8061.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReachPrimaryPsomServerPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero della porta primaria per il protocollo PSOM (Persistent Shared Object Model), un protocollo di Microsoft utilizzato per le conferenze. Il numero di porta predefinito è 8060.</p></td>
</tr>
<tr class="even">
<td><p><em>RmWebSipExternalListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa esterna per app Web di gestione della chat room di Chat persistente. Questa applicazione è disponibile solo se è stata installata e configurata Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>RmWebSipPrimaryListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa primaria per app Web di gestione della chat room di Chat persistente. Questa applicazione è disponibile solo se è stata installata e configurata Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>SupportConferenceConsoleSipExternalListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa per la console per conferenze del supporto. Il valore predefinito è 6007.</p></td>
</tr>
<tr class="odd">
<td><p><em>SupportConferenceConsoleSipPrimaryListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata dalla console per conferenze del supporto di Office 365. Questa console viene utilizzata dal personale addetto all'assistenza tecnica per risolvere i problemi relativi alle conferenze e alle riunioni online.</p></td>
</tr>
<tr class="even">
<td><p><em>UcwaSipExternalListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa SIP esterna per l'API UCWA (Unified Communications Web API). Il valore predefinito è 5088.</p></td>
</tr>
<tr class="odd">
<td><p><em>UcwaSipPrimaryListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa SIP interna per l'API UCWA (Unified Communications Web API). Il valore predefinito è 5089.</p></td>
</tr>
<tr class="even">
<td><p><em>UserServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>ID di servizio per il pool di servizi utente associato al pool di servizi Web. Ad esempio: -UserServer &quot;UserServer:atl-cs-001.litwareinc.com&quot;.</p></td>
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

Nessuno. Il cmdlet **Set-CsWebServer** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsWebServer** modifica invece le istanze dell'oggetto Microsoft.Rtc.Management.Xds.DisplayWebServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

