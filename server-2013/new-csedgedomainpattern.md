---
title: New-CsEdgeDomainPattern
TOCTitle: New-CsEdgeDomainPattern
ms:assetid: 653bc148-c22b-4ad4-afdd-17aaeaa299d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994040(v=OCS.15)
ms:contentKeyID: 52062176
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeDomainPattern

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Usato per specificare un dominio che verrà aggiunto o rimosso dal set di domini abilitati per la federazione o il set di domini disabilitati per la federazione. È necessario usare il cmdlet **New-CsEdgeDomainPattern** per la modifica degli elenchi di domini consentiti o bloccati. Non è possibile passare direttamente i valori stringa, come "fabrikam.com", ai cmdlet usati per gestire questi elenchi.

Il cmdlet **New-CsEdgeDomainPattern** può essere usato solo con Skype for Business online.

## Sintassi

    New-CsEdgeDomainPattern -Domain <String> [-Verbose]

## Esempi

## Esempio 1

L'esempio 1 illustra come assegnare un singolo dominio all'elenco dei domini bloccati per un tenant specificato. A tale scopo, il primo comando nell'esempio crea un oggetto dominio per il dominio fabrikam.com, chiamando il cmdlet **New-CsEdgeDomainPattern** e salvando l'oggetto dominio risultante in una variabile denominata $x. Il secondo comando usa quindi il cmdlet **Set-CsTenantFederationConfiguration** e il parametro BlockedDomains per configurare fabrikam.com come l'unico dominio bloccato dal tenant con TenantId "bf19b7db-6960-41e5-a139-2aa373474354".

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

## Descrizione dettagliata

Il servizio di federazione consente agli utenti di scambiarsi informazioni di messaggistica istantanea e sulla presenza con utenti di altri domini. Con Skype for Business online gli amministratori possono usare le impostazioni di configurazione della federazione per gestire:

  - La possibilità per gli utenti di comunicare con utenti di altri domini ed eventualmente con quali domini possono comunicare.

  - La possibilità per gli utenti di comunicare con altri utenti che dispongono di account presso un servizio di messaggistica istantanea o presso un provider della presenza pubblico come Windows Live, AOL e Yahoo.

La federazione è gestita in parte usando elenchi di domini consentiti e bloccati. L'elenco di domini consentiti specifica i domini con cui gli utenti possono comunicare, mentre l'elenco di domini bloccati include i domini con cui gli utenti non possono comunicare. Per impostazione predefinita, gli utenti possono comunicare con qualsiasi dominio non incluso nell'elenco di domini bloccati. Gli amministratori possono tuttavia modificare l'impostazione predefinita e limitare la comunicazione ai domini inclusi nell'elenco di domini consentiti.

Skype for Business online non consente di modificare direttamente l'elenco di domini consentiti o bloccati. Non è possibile, ad esempio, usare un comando simile al seguente che passa all'elenco di domini bloccati un valore stringa che rappresenta un nome di dominio:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains "fabrikam.com"

È invece necessario creare un oggetto dominio tramite il cmdlet **New-CsEdgeDomainPattern**, archiviare l'oggetto dominio in una variabile (in questo esempio $x), quindi passare il nome di variabile all'elenco dei domini bloccati:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

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
<td><p><em>Domain</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del dominio da aggiungere all'elenco dei domini consenti. Ad esempio:</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>Si noti che non è possibile usare i caratteri jolly per specificare un nome di dominio.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsEdgeDomainPattern** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsEdgeDomainPattern** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DomainPattern.

## Vedere anche

#### Ulteriori risorse

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

