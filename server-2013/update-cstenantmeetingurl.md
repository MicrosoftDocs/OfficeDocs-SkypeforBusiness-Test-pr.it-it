---
title: Update-CsTenantMeetingUrl
TOCTitle: Update-CsTenantMeetingUrl
ms:assetid: 9aed3ede-bbd3-405a-997f-f7553e66aecd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn424754(v=OCS.15)
ms:contentKeyID: 59602742
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsTenantMeetingUrl

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiorna l'URL riunione del tenant di Skype for Business online specificato. L'URL aggiornato usa un formato più semplice e standardizzato che semplifica ai client l'individuazione e la connessione alle riunioni.

Questo cmdlet può essere usato solo con Skype for Business online.

## Sintassi

    Update-CsTenantMeetingUrl [-Tenant] <guid> [-Force] [-WhatIf] [-Confirm]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 aggiorna l'URL riunione del tenant con ID 38aad667-af54-4397-aaa7-e94c79ec2308. L'ID tenant deve essere specificato per poter completare il comando. Dopo aver premuto INVIO per eseguire il comando, viene chiesto di confermare che si vuole aggiornare l'URL riunione. Se si sceglie Sì, Update-CsTenantMeetingUrl viene avviato e inizia ad apportare le modifiche necessarie alle impostazioni di configurazione di Skype for Business online.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308"

## Esempio 2

Anche l'esempio 2 aggiorna l'URL riunione del tenant con ID 38aad667-af54-4397-aaa7-e94c79ec2308, ma in questo caso viene incluso il parametro Force, che disabilita la richiesta di conferma che viene in genere visualizzata quando si esegue Update-CsTenantMeetingUrl. In questo caso, appena si preme INVIO il comando viene eseguito e le impostazioni di configurazione di Skype for Business online vengono modificate.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -Force

## Descrizione dettagliata

Il cmdlet Update-CsTenantMeetingUrl aggiorna l'URL riunione di Skype for Business online in un formato più semplice e standardizzato, eliminando problemi che a volte si verificano con l'URL riunione originale. Supponiamo ad esempio che un'organizzazione configuri un dominio di Office 365 denominato contoso.onmicrosoft.com. Le riunioni avranno quindi URL simili al seguente:

https://meet.lync.com/onmicrosoft/contoso/user1/45GZFH99

Supponiamo ora che, in seguito ad alcuni cambiamenti, l'organizzazione decida di usare l'URL litwareinc.com invece di onmicrosoft.com. Gli indirizzi di posta elettronica degli utenti vengono quindi modificati in modo che usino il dominio litwareinc.com. Tuttavia, gli URL riunione continueranno a usare il vecchio nome di dominio:

https://meet.lync.com/contoso/user1/45GZFH99

Per risolvere il problema, gli amministratori devono eseguire il cmdlet Update-CsTenantMeetingUrl, che sostituisce l'URL riunione precedente con un nuovo URL che contiene il dominio litwareinc.com:

https://meet.lync.com/litwareinc.com/user1/37JYLP71

L'esecuzione del cmdlet Update-CsTenantMeetingUrl è l'unico modo per apportare questa modifica.

Quando si esegue Update-CsTenantMeetingUrl, il tenant di Skype for Business online passa al nuovo URL dopo una breve sincronizzazione. Questo non crea alcun problema per le nuove riunioni pianificate dagli utenti, che vengono pianificate automaticamente con il nuovo URL. Le riunioni pianificate in precedenza riscontreranno invece dei problemi, poiché sono state pianificate con il vecchio URL riunione, non più valido. L'unico modo per risolvere il problema è chiedere agli utenti di ripianificare queste riunioni.

Per evitare di creare problemi, in particolare nelle organizzazioni in cui è già stato pianificato un numero elevato di riunioni, per impostazione predefinita Update-CsTenantMeetingUrl chiede conferma prima di aggiornare l'URL riunione:

AVVISO: Si tratta di una modifica significativa per gli utenti del tenant. La configurazione dell'URL riunione verrà aggiornata. Gli URL riunione precedenti non funzioneranno più. La modifica non può essere annullata.  
Continuare?  
\[Y\] Sì \[A\] Sì a tutti \[N\] No \[L\] No a tutti \[S\] Sospendi \[?\] Guida (l'impostazione predefinita è “Y”):

È necessario rispondere “Sì” o “Sì a tutti” per eseguire effettivamente il comando. Se si risponde “No”, il comando viene annullato e l'URL riunione non viene aggiornato. Tenere presente che, una volta modificato l'URL riunione, non è più possibile ripristinare l'URL originale. Con l'esecuzione del comando l'URL viene modificato e tutte le riunioni pianificate in precedenza devono essere pianificate di nuovo. Questo significa anche che è necessario eseguire il comando una sola volta per tenant. Non c'è bisogno di eseguire periodicamente il comando per riaggiornare l'URL riunione.

Se si preferisce eseguire il comando senza dover rispondere alla richiesta di conferma, è possibile includere il parametro Force. In questo modo Update-CsTenantMeetingUrl viene eseguito senza visualizzare la richiesta di conferma:

AVVISO: Si tratta di una modifica significativa per gli utenti del tenant. La configurazione dell'URL riunione verrà aggiornata.

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
<td><p><strong>Tenant</strong></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di cui vengono restituite le impostazioni di federazione. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Eseguendo questo comando è possibile ottenere l'ID di ogni tenant:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se non si include il parametro Tenant, Update-CsMeetingUrl chiede di inserirlo prima di continuare.</p></td>
</tr>
<tr class="even">
<td><p><strong>Confirm</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p>
<p>Per impostazione predefinita, Update-CsMeetingUrl visualizza la richiesta di conferma prima di eseguire qualsiasi modifica. Questo significa che, se si vuole visualizzare la richiesta di conferma, non è necessario includere il parametro Confirm.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Force</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione della richiesta di conferma, che altrimenti verrebbe visualizzata prima che Update-CsMeetingUrl apporti qualsiasi modifica.</p></td>
</tr>
<tr class="even">
<td><p><strong>WhatIf</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Update-CsMeetingUrl non accetta input da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

