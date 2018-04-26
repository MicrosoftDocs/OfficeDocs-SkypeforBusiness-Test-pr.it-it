---
title: Disable-CsComputer
TOCTitle: Disable-CsComputer
ms:assetid: e64128f1-2b53-4569-bf37-90cbbba01b36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399023(v=OCS.15)
ms:contentKeyID: 49302307
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Disabilita un servizio o un ruolo del server rimosso da un computer in cui è in esecuzione Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Disable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Scorch <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 disabilita il computer locale.

    Disable-CsComputer 

## ESEMPIO 2

Anche il comando mostrato nell'esempio 2 disabilita il computer locale. In aggiunta, le informazioni relative all'avvenuta o alla mancata esecuzione di questa attività vengono registrate nel file C:\\Logs\\Disable.html. Tale file di log viene generato aggiungendo il parametro Report seguito dal percorso del file in cui si desidera vengano registrate le informazioni.

    Disable-CsComputer -Report C:\Logs\Disable.html

## Descrizione dettagliata

Rimuovendo un servizio o un ruolo del server da un computer, non viene automaticamente aggiornata la topologia di Lync Server. È anzi necessario disabilitare tale servizio o ruolo prima che le modifiche vengano interamente aggiornate nella topologia. Il cmdlet **Disable-CsComputer** consente agli amministratori di disabilitare i servizi o i ruoli del server rimossi dal computer locale.

A meno che non venga utilizzato il parametro Scorch, con il cmdlet **Disable-CsComputer** il software Lync Server non viene disinstallato. Semplicemente il computer non opererà più nel ruolo assegnatogli in precedenza.

Utenti autorizzati a eseguire il cmdlet: per poter eseguire localmente il cmdlet **Disable-CsComputer**, è necessario essere amministratori locali e membri del dominio.

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
<td><p>Il nome di dominio completo (FQDN) di un server di catalogo globale nel dominio in uso. Questo parametro non è necessario se si esegue il cmdlet <strong>Disable-CsComputer</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro dovrà puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, sarà possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\DisableComputer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scorch</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Disinstalla tutti i servizi e i ruoli del server di Lync Server per il computer locale.</p></td>
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

Nessuno. Il cmdlet **Disable-CsComputer** non accetta input inviato tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Disable-CsComputer** disabilita piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.Machine.

## Vedere anche

#### Ulteriori risorse

[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

