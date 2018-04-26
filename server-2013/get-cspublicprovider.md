---
title: Get-CsPublicProvider
TOCTitle: Get-CsPublicProvider
ms:assetid: c122505d-7209-4dcb-a888-5c73f58fa68a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412945(v=OCS.15)
ms:contentKeyID: 49301853
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui provider pubblici configurati per l'utilizzo nell'organizzazione. Un provider pubblico è un'organizzazione che offre al grande pubblico servizi di messaggistica istantanea, presenza e altri servizi correlati. Lync Server viene fornito con tre provider pubblici configurati, ma non abilitati: Yahoo\!, AIM (AOL) e Messenger (MSN). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPublicProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituita una raccolta di tutti i provider pubblici che sono configurati per l'utilizzo nell'organizzazione. Se si chiama il cmdlet **Get-CsPublicProvider** senza parametri aggiuntivi, verrà restituita sempre la raccolta completa dei provider pubblici.

    Get-CsPublicProvider

## ESEMPIO 2

Nell'esempio 2 vengono restituiti tutti i provider pubblici con valore Identity Messenger. Poiché le identità devono essere univoche tra i provider pubblici e tra quelli di hosting, il comando restituirà al massimo un elemento.

    Get-CsPublicProvider -Identity "Messenger"

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti i provider pubblici con valore Identity che inizia con la lettera W. Questa operazione viene eseguita includendo il parametro Filter e il valore di filtro "W\*".

    Get-CsPublicProvider -Filter W*

## ESEMPIO 4

Con il comando mostrato nell'esempio 4 viene restituita una raccolta di tutti i provider pubblici attualmente disabilitati. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider con proprietà Enabled uguale a False.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False}

## ESEMPIO 5

Nell'esempio 5 vengono restituiti tutti i provider pubblici per cui la proprietà VerificationLevel è impostata su AlwaysUnverifiable o UseSourceVerification (i livelli di verifica possono essere impostati su AlwaysUnverifiable, UseSourceVerification o AlwaysVerifiable). Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che sceglie solo i provider con proprietà VerificationLevel non uguale a AlwaysVerifiable. Il risultato è che verranno selezionati solo i provider per cui la proprietà VerificationLevel è impostata su AlwaysUnverifiable o UseSourceVerification.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"}

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Una volta stabilita una federazione, gli utenti delle due organizzazioni possono scambiarsi messaggi istantanei, sottoscrivere le notifiche di presenza e comunicare tra loro in altri modi utilizzando le applicazioni SIP come Lync 2013. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico, e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

Un provider pubblico è un'organizzazione che fornisce servizi di comunicazione SIP al pubblico. Quando si stabilisce una relazione di federazione con un provider pubblico, in realtà si stabilisce una federazione con qualsiasi utente che disponga di un account ospitato da tale provider. Se ad esempio si stabilisce una federazione con Messenger (MSN), gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di ﻿messaggistica istantanea Messenger.

Per poter stabilire una federazione con un provider pubblico, è necessario crearne e abilitarne uno nuovo, e il provider pubblico dovrà creare una relazione di federazione con l'utente o l'organizzazione. Il cmdlet **Get-CsPublicProvider** consente di restituire informazioni sui provider pubblici che sono stati configurati per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsPublicProvider** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPublicProvider"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare valori con caratteri jolly per restituire uno o più provider pubblici. Per restituire ad esempio una raccolta di tutti i provider pubblici con valore Identity che inizia con la lettera Y, utilizzare la seguente sintassi: -Filter &quot;Y*&quot;. Per restituire una raccolta di tutti i provider pubblici che includono il valore stringa &quot;Windows&quot; in un punto qualsiasi del valore Identity, utilizzare la seguente sintassi: -Filter &quot;*Windows*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il provider pubblico da restituire. L'identità in genere corrisponde al nome del sito Web che fornisce i servizi, ad esempio Yahoo!, AOL, MSN e così via.</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità. Anziché utilizzare caratteri jolly per restituire uno o più provider pubblici, utilizzare il parametro Filter.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi ai provider pubblici dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPublicProvider** non accetta input da pipeline.

## Tipi restituiti

Restituisce le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

