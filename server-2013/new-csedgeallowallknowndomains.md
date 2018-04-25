---
title: New-CsEdgeAllowAllKnownDomains
TOCTitle: New-CsEdgeAllowAllKnownDomains
ms:assetid: f9416909-c328-41b3-9215-7ebd091b0ca0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994088(v=OCS.15)
ms:contentKeyID: 52062487
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowAllKnownDomains

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita la federazione di Microsoft Lync Online con tutti i domini ad eccezione di quelli inclusi nell'elenco dei domini bloccati.

Questo cmdlet può essere usato solo con Skype for Business online.

## Sintassi

    New-CsEdgeAllowAllKnownDomains [-Verbose]

## Esempi

## Esempio 1

I due comandi illustrati nell'esempio 1 consentono di configurare le impostazioni di federazione per il tenant con Identity "bf19b7db-6960-41e5-a139-2aa373474354" in modo da consentire tutti i domini noti. A tale scopo, il primo comando nell'esempio usa il cmdlet **New-CsEdgeAllowAllKnownDomains** per creare un'istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains. Questa istanza è archiviata in una variabile denominata $x. Nel secondo comando viene chiamato il cmdlet **Set-CsTenantFederationConfiguration** con il parametro AllowedDomains. L'uso di $x come valore di parametro consente di configurare le impostazioni di federazione in modo da consentire tutti i domini noti.

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

## Esempio 2

L'esempio 2 dimostra come è possibile configurare tutti i tenant in modo da consentire le comunicazioni con tutti i domini non inclusi esplicitamente nell'elenco dei domini bloccati. A tale scopo, il primo comando nell'esempio usa il cmdlet **New-CsEdgeAllowAllKnownDomains** per creare un'istanza dell'oggetto AllowAllKnownDomains, un oggetto archiviato in una variabile denominata $x.

Il secondo comando nell'esempio usa quindi il cmdlet **Get-CsTenant** per restituire una raccolta di tutti i tenant disponibili. La raccolta viene poi inviata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet **ForEach-Object**, a sua volta, esegue il cmdlet **Set-CsTenantFederationConfiguration** per ogni tenant nella raccolta, configurando la proprietà AllowedDomains in modo da consentire tutti i domini noti.

    $x = New-CsEdgeAllowAllKnownDomains
    Get-CsTenant | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantID -AllowedDomains $x}

## Descrizione dettagliata

Il servizio di federazione consente agli utenti di scambiarsi informazioni di messaggistica istantanea e sulla presenza con utenti di altri domini. Con Lync Online gli amministratori possono usare le impostazioni di configurazione della federazione per gestire:

  - La possibilità per gli utenti di comunicare con utenti di altri domini ed eventualmente con quali domini possono comunicare.

  - La possibilità per gli utenti di comunicare con altri utenti che dispongono di account presso un servizio di messaggistica istantanea o presso un provider della presenza pubblico come Windows Live, AOL e Yahoo.

La federazione è gestita in parte usando elenchi di domini consentiti e bloccati. L'elenco di domini consentiti specifica i domini con cui gli utenti possono comunicare, mentre l'elenco di domini bloccati include i domini con cui gli utenti non possono comunicare. Per impostazione predefinita, gli utenti possono comunicare con qualsiasi dominio non incluso nell'elenco di domini bloccati. Gli amministratori possono tuttavia modificare l'impostazione predefinita e limitare la comunicazione ai domini inclusi nell'elenco di domini consentiti.

Lync Online non consente di modificare direttamente l'elenco di domini consentiti o bloccati. Non è possibile ad esempio usare un comando simile al seguente che passa all'elenco di domini consentiti un valore stringa che rappresenta un nome di dominio:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

È invece necessario usare il cmdlet **New-CsEdgeAllowAllKnownDomains** o **New-CsEdgeAllowList** per creare un oggetto dominio e passarlo quindi al cmdlet **Set-CsTenantFederationConfiguration**. Il cmdlet **New-CsEdgeAllowAllKnownDomains** viene usato per consentire agli utenti di comunicare con tutti i domini eccetto quelli espressamente specificati nell'elenco di domini bloccati. Il cmdlet **ew-CsEdgeAllowList** viene usato per limitare la comunicazione degli utenti a una raccolta di domini specificata. In questo caso, gli utenti saranno autorizzati a comunicare solo con i domini presenti nell'elenco di domini consentiti.

Per configurare la federazione con tutti i domini noti, usare un set di comandi simile al seguente:

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

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
<td><p>Questo cmdlet fornisce unicamente i parametri comuni di Windows PowerShell.</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsEdgeAllowAllKnownDomains** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsEdgeAllowAllKnownDomains** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains.

## Vedere anche

#### Ulteriori risorse

[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

