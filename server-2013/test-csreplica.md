---
title: Test-CsReplica
TOCTitle: Test-CsReplica
ms:assetid: cef1fcda-3292-411a-b3dd-7a8ef7935b20
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205289(v=OCS.15)
ms:contentKeyID: 49302009
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsReplica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica lo stato del servizio di replica nel computer locale. Il servizio di replica viene utilizzato per replicare le informazioni tra tutti i computer Lync Server 2013 nella topologia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsReplica [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 testa il servizio di replica di Lync Server 2013 nel computer locale. In questo esempio il parametro Verbose viene utilizzato per assicurarsi che le informazioni sul test, incluso il relativo esito positivo o negativo del test, nonché il percorso del report generato dal test vengano visualizzate sullo schermo.

    Test-CsReplica -Verbose

## Esempio 2

L'esempio 2 è una variazione del comando illustrato nell'esempio 1. In questo caso, tuttavia, il parametro Report viene incluso per specificare un percorso di cartella e un nome per il report generato dal test. Se non si specifica un percorso, al report verrà assegnato un nome generato automaticamente simile al seguente:

C:\\Users\\Administrator.Litwareinc\\AppData\\Local\\Temp\\1\\Test-Cs-Replica-3db40ee0-4b5d-4f58-8d3d-b1e61253129e.html

    Test-CsReplica -Verbose -Report C:\Logs\ReplicaTest.html

## Descrizione dettagliata

Il cmdlet **Test-CsReplica** verifica che il servizio di replica di Lync Server 2013 sia in esecuzione nel computer locale. Il cmdlet **Test-CsReplica** esegue diverse attività. Verifica ad esempio lo stato dei servizi Agente di replica e Agente di registrazione centralizzato, controlla che in Windows Firewall siano state aperte le porte necessarie e verifica che siano presenti i gruppi di sicurezza di Active Directory e del computer locale necessari.

Si noti che questo cmdlet deve essere eseguito localmente, ovvero nello stesso computer in cui viene eseguito il servizio di replica. Non sono disponibili opzioni che consentono di eseguire **Test-CsReplica** in un server remoto.

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsReplica** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo di un server di catalogo globale nel dominio in uso. Questo parametro non è necessario se si esegue il cmdlet <strong>Test-CsReplica</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio nel dominio. Questo parametro non è obbligatorio se il cmdlet <strong>Test-CsReplica</strong> viene eseguito in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio:</p>
<p>-Report &quot;C:\Logs\ReplicaTest.html&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsReplica** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsReplica** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

