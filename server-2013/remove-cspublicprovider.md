---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412906(v=OCS.15)
ms:contentKeyID: 49301789
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un provider pubblico configurato per l'utilizzo nell'organizzazione. Un provider pubblico è un'organizzazione che offre al grande pubblico servizi di messaggistica istantanea, presenza e altri servizi correlati. Lync Server viene fornito con tre provider pubblici configurati, ma non abilitati: Yahoo\!, AIM (AOL) e Messenger (MSN). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene eliminato il provider pubblico con l'identità Messenger. Al completamento del comando, Messenger non sarà più visualizzato nell'elenco dei provider pubblici configurati. A quel punto, l'unico modo per ristabilire la federazione con Messenger è ricreare il provider.

    Remove-CsPublicProvider -Identity "Messenger"

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i provider pubblici configurati per l'utilizzo nell'organizzazione. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici attualmente configurati per l'utilizzo. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPublicProvider**, che a sua volta elimina ogni provider contenuto nella raccolta.

    Get-CsPublicProvider | Remove-CsPublicProvider

## ESEMPIO 3

Nell'esempio 3 tutti i provider pubblici attualmente disabilitati vengono rimossi dall'insieme dei provider pubblici configurati. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici attualmente configurati per l'utilizzo. La raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider con proprietà Enabled uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsPublicProvider**, che elimina tutti gli elementi della raccolta.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

## Descrizione dettagliata

La federazione è un mezzo attraverso il quale due organizzazioni possono stabilire una relazione di trust per agevolare la comunicazione tra i due gruppi. Quando viene stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere le notifiche di presenza e comunicare tra loro in altri modi utilizzando le applicazioni SIP, ad esempio Lync 2013. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni, 2) federazione tra un'organizzazione e un provider pubblico e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

Un provider pubblico è un'organizzazione che fornisce servizi di comunicazione SIP al grande pubblico. Quando si stabilisce una relazione di federazione con un provider pubblico, in realtà si stabilisce una federazione con qualsiasi utente che disponga di un account ospitato da tale provider. Ad esempio, se si stabilisce una federazione con Messenger (MSN), gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di messaggistica istantanea di Messenger.

Per poter stabilire una federazione con un provider pubblico, è necessario crearne e abilitarne uno nuovo. Il provider pubblico inoltre dovrà creare una relazione di federazione con l'utente o l'organizzazione. Se si decide in seguito di interrompere la relazione, è possibile utilizzare il cmdlet **Remove-CsPublicProvider** per eliminare il provider pubblico. Quando si elimina un provider pubblico, quest'ultimo viene rimosso dall'elenco dei partner federati. A quel punto, l'unico modo per ristabilire la relazione consiste nel ricreare il provider. Se si desidera sospendere temporaneamente una relazione, utilizzare invece il cmdlet **Disable-CsPublicProvider**. Quando un provider pubblico è disabilitato, non viene eliminato dall'elenco dei partner federati. Viene semplicemente contrassegnato come disabilitato e le comunicazioni tra la propria organizzazione e il provider vengono sospese. Per ristabilire la relazione, è possibile utilizzare il cmdlet **Enable-CsPublicProvider** per riabilitare il provider.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsPublicProvider** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il provider pubblico da eliminare. Il valore di questo parametro in genere corrisponde al nome del sito Web che fornisce i servizi, ad esempio Yahoo!, AOL, MSN e così via.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. Il cmdlet **Remove-CsPublicProvider** accetta istanze dell'oggetto provider pubblico inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet piuttosto elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

