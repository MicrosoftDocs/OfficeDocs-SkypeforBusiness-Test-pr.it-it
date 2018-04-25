---
title: Get-CsAdForest
TOCTitle: Get-CsAdForest
ms:assetid: f063df2f-fdb2-4599-bfb0-fb4ba3584e3b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412995(v=OCS.15)
ms:contentKeyID: 49302426
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdForest

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano se la foresta di Active Directory è stata configurata correttamente per consentire l'installazione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdForest [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-RootDomainController <Fqdn>] [-SkipPrepareCheck <$true | $false>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni che indicano se la foresta di Active Directory in uso è stata configurata correttamente per consentire l'installazione di Lync Server.

    Get-CsAdForest

## ESEMPIO 2

Nell'esempio 2 vengono restituite le informazioni sullo stato della foresta e sullo schermo viene visualizzata la preparazione della foresta. Inoltre, informazioni dettagliate sulla procedura adottata per determinare lo stato della foresta vengono scritte in un file denominato C:\\Logs\\Forest\_State.html. Il file contiene un elenco dettagliato di tutti i gruppi di Active Directory e i contenitori di Active Directory di cui sono state verificate le autorizzazioni.

    Get-CsAdForest -Report C:\Logs\ForestState.html

## Descrizione dettagliata

Prima di poter installare Lync Server è necessario apportare diverse modifiche a livello di foresta in Servizi di dominio Active Directory. Esse comprendono la creazione di specificatori di visualizzazione e oggetti specifici per Lync Server, nonché la creazione dei gruppi di sicurezza universali necessari per gestire Lync Server e la concessione a questi gruppi di autorizzazioni di accesso alle impostazioni globali. Il cmdlet **Get-CsAdForest** restituisce un valore singolo che indica se Lync Server può essere installato in una foresta. Se il cmdlet **Get-CsAdForest** restituisce il valore LC\_FORESTSETTINGS\_STATE\_READY, è possibile installare Lync Server nella foresta. Se il cmdlet restituisce LC\_FORESTSETTINGS\_STATE\_NOT\_READY, è necessario preparare la foresta nel modo corretto, prima di tentare l'installazione di Lync Server.

Il cmdlet **Get-CsAdForest** viene eseguito come parte dell'installazione guidata. Se l'installazione guidata determina che la foresta non è preparata correttamente, verrà visualizzato un messaggio di errore e l'installazione verrà interrotta. Tuttavia, è possibile eseguire il cmdlet **Get-CsAdForest** indipendentemente dall'installazione guidata per verificare lo stato della foresta prima di ritentare l'installazione di Lync Server.

Il cmdlet **Get-CsAdForest** ha la stessa funzione del comando Microsoft Office Communications Server 2007 R2 seguente:

Lcscmd.exe /forest /action:CheckForestPrepState

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, chiunque disponga delle autorizzazioni di lettura per Active Directory può eseguire il cmdlet **Get-CsAdForest** in locale. In genere tutti i membri del dominio dispongono di questa autorizzazione.

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdForest"}

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
<td><p>Il nome di dominio completo di un server di catalogo globale nel dominio in uso. Se si esegue il cmdlet <strong>Get-CsAdForest</strong> su un computer che dispone di un account nel dominio, questo parametro non è obbligatorio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio in cui sono archiviate le impostazioni globali. Se in Servizi di dominio Active Directory le impostazioni globali sono archiviate nel contenitore di sistema, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, è possibile utilizzare qualsiasi dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ForestPrep.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RootDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del controller di dominio radice utilizzato per creare i percorsi di attendibilità per i client che devono accedere alle risorse in domini diversi dal proprio.</p></td>
</tr>
<tr class="odd">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se il parametro è impostato su True ($True), Get-CsAdForest viene eseguito senza svolgere i controlli di preparazione iniziali.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsAdForest** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deployment.LcForestSettingsState.

