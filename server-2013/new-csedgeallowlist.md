---
title: New-CsEdgeAllowList
TOCTitle: New-CsEdgeAllowList
ms:assetid: 21a6d546-9e03-485c-b7ec-9deb778f2b01
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994023(v=OCS.15)
ms:contentKeyID: 52062112
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowList

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente agli amministratori di specificare i domini con cui gli utenti saranno autorizzati a comunicare. Il cmdlet **New-CsEdgeAllowList**, che funziona solo con Microsoft Lync Online, deve essere usato insieme ai cmdlet **New-CsEdgeDomainPattern** e **Set-CsTenantFederationConfiguration**.

## Sintassi

    New-CsEdgeAllowList [-AllowedDomain <PSListModifier>] [-Verbose]

## Esempi

## Esempio 1

I comandi illustrati nell'esempio 1 consentono di assegnare il dominio fabrikam.com all'elenco di domini consentiti per il tenant con TenantId "bf19b7db-6960-41e5-a139-2aa373474354". A questo scopo, il primo comando nell'esempio usa il cmdlet **New-CsEdgeDomainPattern** per creare un oggetto dominio per fabrikam.com, che viene archiviato in una variabile denominata $x. Dopo la creazione dell'oggetto dominio, viene usato il cmdlet **New-CsEdgeAllowList** per creare un nuovo elenco di domini consentiti contenente solo il dominio fabrikam.com.

Una volta creato l'elenco di domini consentiti, il comando finale nell'esempio userà il cmdlet **Set-CsTenantFederationConfiguration** per configurare fabrikam.com come unico dominio nell'elenco di domini consentiti per il tenant specificato.

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Si noti che il parametro Tenant è obbligatorio solo in una distribuzione ibrida. Se si è connessi solo a Skype for Business online, questo parametro può essere omesso.

## Esempio 2

L'esempio 2 mostra come aggiungere più domini a un elenco di domini consentiti. A questo scopo, chiamare più volte il cmdlet **New-CsEdgeDomainPattern**, una volta per ogni dominio da aggiungere all'elenco, e archiviare gli oggetti dominio risultanti in variabili separate. Ognuna di queste variabili potrà quindi essere aggiunta all'elenco di domini consentiti creato dal cmdlet **New-CsEdgeAllowList**, usando semplicemente il parametro AllowedDomain e separando i nomi delle variabili con virgole:

$newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y

    $x = New-CsEdgeDomainPattern -Domain "contoso.com"
    $y = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Esempio 3

Nell'esempio 3 vengono rimossi tutti i domini dall'elenco di domini consentiti. A questo scopo, il primo comando nell'esempio usa il cmdlet **New-CsEdgeAllowList** per creare un elenco di domini consentiti vuoto, impostando la proprietà AllowedDomain su un valore Null ($Null). Il riferimento all'oggetto risultante ($newAllowList) viene quindi usato insieme al cmdlet **Set-CsTenantFederationConfiguration** per rimuovere tutti i domini dall'elenco di domini consentiti per il tenant con TenantId "bf19b7db-6960-41e5-a139-2aa373474354".

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $Null
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Descrizione dettagliata

Il servizio di federazione consente agli utenti di scambiarsi informazioni di messaggistica istantanea e sulla presenza con utenti di altri domini. Con Lync Online gli amministratori possono usare le impostazioni di configurazione della federazione per gestire:

  - La possibilità per gli utenti di comunicare o meno con persone di altri domini e, in tal caso, con quali domini possono comunicare.

  - La possibilità per gli utenti di comunicare o meno con persone che dispongono di account di provider di servizi di messaggistica istantanea e presenza pubblici, quali Windows Live, Yahoo\! e AOL.

La federazione è gestita in parte usando elenchi di domini consentiti e bloccati. L'elenco di domini consentiti specifica i domini con cui gli utenti possono comunicare, mentre l'elenco di domini bloccati include i domini con cui gli utenti non possono comunicare. Per impostazione predefinita, gli utenti possono comunicare con qualsiasi dominio non incluso nell'elenco di domini bloccati. Gli amministratori possono tuttavia modificare l'impostazione predefinita e limitare la comunicazione ai domini inclusi nell'elenco di domini consentiti.

Lync Online non consente di modificare direttamente l'elenco di domini consentiti o bloccati. Non è possibile ad esempio usare un comando simile al seguente che passa all'elenco di domini consentiti un valore stringa che rappresenta un nome di dominio:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

È invece necessario usare il cmdlet **New-CsEdgeAllowAllKnownDomains** o **New-CsEdgeAllowList** per creare un oggetto dominio e passarlo quindi al cmdlet **Set-CsTenantFederationConfiguration**. Il cmdlet **New-CsEdgeAllowAllKnownDomains** viene usato per consentire agli utenti di comunicare con tutti i domini eccetto quelli espressamente specificati nell'elenco di domini bloccati. Il cmdlet **New-CsEdgeAllowList** viene usato per limitare la comunicazione degli utenti a una raccolta di domini specificata. In questo caso, gli utenti saranno autorizzati a comunicare solo con i domini presenti nell'elenco di domini consentiti.

Per aggiungere un singolo dominio (fabrikam.com) all'elenco di domini consentiti, è necessario usare un set di comandi simile al seguente:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Al termine dell'esecuzione di questo comando, gli utenti potranno comunicare solo con gli utenti del dominio fabrikam.com.

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
<td><p><em>AllowedDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Riferimento all'oggetto per il nuovo dominio, o set di domini, da aggiungere all'elenco di domini consentiti. È necessario creare riferimenti agli oggetti dominio utilizzando il cmdlet <strong>New-CsEdgeDomainPattern</strong>. È possibile aggiungere più oggetti dominio separando i riferimenti agli oggetti con virgole. Ad esempio:</p>
<p>-AllowedDomain $x,$y</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsEdgeAllowList** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsEdgeAllowList** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowList.

## Vedere anche

#### Ulteriori risorse

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

