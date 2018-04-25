---
title: New-CsHealthMonitoringConfiguration
TOCTitle: New-CsHealthMonitoringConfiguration
ms:assetid: 8ed1da01-f7db-482d-b99a-777f239908e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398718(v=OCS.15)
ms:contentKeyID: 49301290
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsHealthMonitoringConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione del monitoraggio dello stato per l'utilizzo nell'organizzazione. Queste impostazioni consentono agli amministratori di eseguire test di controllo della qualità senza dover fornire nome utente e password per gli account di test necessari. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsHealthMonitoringConfiguration -TargetFqdn <String> <COMMON PARAMETERS>

    New-CsHealthMonitoringConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -FirstTestUserSipUri <String> -SecondTestUserSipUri <String> [-Confirm [<SwitchParameter>]] [-FirstTestSamAccountName <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SecondTestSamAccountName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare una nuova raccolta di impostazioni di configurazione per il monitoraggio dello stato per il pool atl-cs-001.litwareinc.com. Queste nuove impostazioni utilizzeranno sip:davidegarghentini@litwareinc.com e sip:pilar@litwareinc.com come i due account di test preconfigurati.

    New-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -SecondTestUserSipUri "sip:pilar@litwareinc.com"

## ESEMPIO 2

Nell'Esempio 2 viene creata una nuova raccolta di impostazioni di configurazione per il monitoraggio dello stato per tutti i pool di registrazione dell'organizzazione. Per ottenere questo risultato, il primo comando nell'esempio utilizza il cmdlet **Get-Service** e il parametro Registrar per ottenere una raccolta di tutti i pool di registrazione. Questa raccolta viene poi inviata tramite pipe al cmdlet **Select-Object** che seleziona solo la proprietà PoolFqdn. Questa proprietà restituisce il nome completo di dominio (FQDN) di un pool di registrazione. Questi FQDN sono memorizzati in una variabile denominata $x.

Nel secondo comando viene creato un ciclo foreach per eseguire un ciclo tra ogni FQDN dei pool di registrazione. Per ogni FQDN viene chiamato il cmdlet **New-CsHealthMonitoringConfiguration** per creare una nuova raccolta di impostazioni di configurazione, con il valore FQDN archiviato nella variabile $x utilizzato come identità (Identity) per la nuova raccolta. A ogni raccolta vengono assegnati gli stessi due account di test: sip:kenmyer@litwareinc.com e sip:pilar@litwareinc.com.

    $x = Get-CsService -Registrar | Select-Object PoolFqdn
    foreach ($i in $x)
       {New-CsHealthMonitoringConfiguration -Identity $i.PoolFqdn -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -SecondTestUserSipUri "sip:pilar@litwareinc.com"}

## Descrizione dettagliata

Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite "manualmente" da un amministratore oppure possono essere eseguite automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano i cmdlet **CsHealthMonitoringConfiguration** per configurare account di test per ciascun pool di registrazione. Si tratta di una coppia di account utente appositamente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato gli account di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test. Infatti, al momento di eseguire i controlli, la transazione sintetica utilizzerà automaticamente gli account di test predefiniti.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test). Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali, sarà necessario fornire le credenziali di tutti gli utenti coinvolti.

Il cmdlet **New-CsHealthMonitoringConfiguration** offre la possibilità di creare nuove impostazioni di configurazione per il monitoraggio dello stato per un pool. Quando si crea una nuova raccolta di impostazioni di configurazione per il monitoraggio dello stato si deve specificare il nome completo di dominio del pool così come l'indirizzo SIP dei due account che serviranno come account di test per il pool. Non è tuttavia necessario fornire la password di questi account di test. Si noti che ciascun pool può ospitare al massimo una singola raccolta di impostazioni di configurazione per il monitoraggio dello stato. Se si tenta di creare una nuova raccolta per il pool atl-cs-001.litwareinc.com e a questo pool è già stata assegnata una registrazione, il comando avrà esito negativo.

Quando si esegue il cmdlet **New-CsHealthMonitoringConfiguration**, è possibile che si riceva un avviso se sono presenti pool a cui non sono stati assegnati utenti di test, inclusi pool di server Director così e pool di Office Communications Server. Questo avviso può essere ignorato. Se lo si preferisce, è possibile assegnare utenti di test di altri pool ai propri pool di server Director, in modo da consentire l'esecuzione del cmdlet **Test-CsRegistration** per il server Director. Non è possibile tuttavia assegnare utenti di test ai pool di Office Communications Server.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsHealthMonitoringConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsHealthMonitoringConfiguration"}

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
<td><p><em>FirstTestUserSipUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP del primo utente di test da configurare per l'utilizzo in questa raccolta di impostazioni per il monitoraggio dello stato. Si noti che l'indirizzo SIP deve includere il prefisso sip:. Ad esempio: -FirstTestUserSipUri &quot;sip:davidegarghentini@litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome completo di dominio del pool al quale assegnare le impostazioni di configurazione per il monitoraggio dello stato (ad esempio: -Identity atl-cs-001.litwareinc.com). Il comando avrà esito negativo se il pool specificato ospita già una raccolta di impostazioni di configurazione per il monitoraggio dello stato.</p>
<p>Il parametro Identity è equivalente al parametro TargetFqdn. Quando si crea una nuova raccolta di impostazioni, è possibile utilizzare uno dei due parametri. Se si omettono entrambi i parametri, il cmdlet <strong>New-CsHealthMonitoringConfiguration</strong> chiederà di immettere il parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondTestUserSipUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP del secondo utente di test da configurare per l'utilizzo in questa raccolta di impostazioni per il monitoraggio dello stato. Si noti che l'indirizzo SIP deve includere il prefisso sip:. Ad esempio: -SecondTestUserSipUri &quot;sip:pilar@litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome completo di dominio del pool al quale assegnare le impostazioni di configurazione per il monitoraggio dello stato (ad esempio: -TargetFqdn atl-cs-001.litwareinc.com). Il comando avrà esito negativo se il pool specificato ospita già una raccolta di impostazioni di configurazione per il monitoraggio dello stato.</p>
<p>Il parametro TargetFqdn è equivalente al parametro Identity. Quando si crea una nuova raccolta di impostazioni, è possibile utilizzare uno dei due parametri. Se si omettono entrambi i parametri, il cmdlet <strong>New-CsHealthMonitoringConfiguration</strong> chiederà di immettere il parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>FirstTestSamAccountName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>SamAccountName del primo utente di test. FirstTestSamAccountName deve essere immesso utilizzando il formato dominio\nomeutente; ad esempio:</p>
<p>-FirstTestSamAccountName litwareinc\davidegarghentini</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondTestSamAccountName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>SamAccountName del secondo utente di test. SecondTestSamAccountName deve essere immesso utilizzando il formato dominio\nomeutente; ad esempio:</p>
<p>-SecondTestSamAccountName litwareinc\pilar</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsHealthMonitoringConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsHealthMonitoringConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)

