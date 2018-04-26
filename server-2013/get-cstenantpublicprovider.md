---
title: Get-CsTenantPublicProvider
TOCTitle: Get-CsTenantPublicProvider
ms:assetid: 0d949ec2-206d-4979-a3be-a5578ae93ed3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994016(v=OCS.15)
ms:contentKeyID: 52062094
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano se gli utenti di Microsoft Lync Online sono autorizzati a comunicare con altri utenti che dispongono di account presso provider di servizi di messaggistica istantanea e di presenza di terze parti, come Windows Live, AOL e Yahoo.

Questo cmdlet può essere usato solo con Skype for Business online.

## Sintassi

    Get-CsTenantPublicProvider -Tenant <String> [-Verbose]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 restituisce informazioni sui provider pubblici per il tenant con ID "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Si noti che il parametro Tenant è facoltativo. È possibile chiamare Get-CsTenantPublicProvider anche con questa sintassi:

    Get-CsTenantPublicProvider

## Esempio 2

Il comando precedente restituisce informazioni dettagliate sullo stato di tutti i provider pubblici assegnati al tenant bf19b7db-6960-41e5-a139-2aa373474354. A tale scopo, il comando usa prima di tutto il cmdlet **Get-CsTenantPublicProvider** per restituire informazioni sui provider pubblici per il tenant specificato. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che usa il parametro ExpandProperty per "espandere" il valore della proprietà DomainPICStatus. L'espansione di una proprietà significa semplicemente visualizzare tutti i valori archiviati in quella proprietà in un formato di facile lettura.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Un comando come questo verrebbe usato in una distribuzione ibrida di Lync Server 2013.

## Esempio 3

Il comando riportato nell'esempio 3 è una variante di quello mostrato nell'esempio 2. Nell'esempio 3, tuttavia, le informazioni sui provider pubblici restituite tramite l'espansione del valore della proprietà DomainPICStatus vengono a loro volta inviate tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** seleziona quindi solo i provider con la proprietà Status impostata su Enabled. Il risultato finale è la visualizzazione dei soli provider pubblici abilitati per l'uso.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus | Where-Object {$_.Status -eq "Enabled"}

## Descrizione dettagliata

I provider pubblici sono organizzazioni che forniscono servizi di comunicazione SIP al pubblico. Quando si configura una relazione di federazione con un provider pubblico, la federazione viene in realtà estesa a chiunque disponga di un account ospitato da tale provider. Se ad esempio si abilita la federazione con Windows Live, gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di messaggistica istantanea di Windows Live.

Lync Online offre agli amministratori la possibilità di configurare la federazione con uno o più dei provider di servizi di messaggistica istantanea o di presenza pubblici seguenti:

  - Windows Live

  - AOL

  - Yahoo\!

Gli amministratori possono usare il cmdlet **Get-CsTenantPublicProvider** per stabilire quali di tali provider sono stati eventualmente abilitati per la federazione. Con la chiamata del cmdlet **Get-CsTenantPublicProvider** si ottengono informazioni simili alle seguenti:

    PublicProviderSet     DomainPicStatus
    ------------------    ------------------------
    True                  {Microsoft.Rtc.Management.Hosted.DomainPICStatus}

La proprietà PublicProviderSet indica se la federazione è stata o meno abilitata per uno o più provider pubblici. Se la proprietà PublicProviderSet è impostata su True, la federazione è abilitata con almeno un provider. Se la proprietà PublicProviderSet è False, la federazione è disabilitata per tutti e tre i provider pubblici (Windows Live, AOL e Yahoo). Per stabilire lo stato effettivo di ogni provider, usare questo comando:

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Si noti che la semplice abilitazione dello stato di un provider pubblico non significa che gli utenti siano in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che hanno account con tale provider. Oltre ad abilitare la federazione con il provider in questione, gli amministratori devono anche impostare su True la proprietà AllowPublicUsers delle impostazioni di configurazione della federazione. Se la proprietà è impostata su False, le comunicazioni non saranno consentite con alcun provider pubblico, indipendentemente dalle impostazioni di configurazione del provider pubblico.

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet **Set-CsTenantFederationConfiguration**.

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
<td><p><em>Tenant</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di cui vengono restituite le impostazioni dei provider pubblici. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTenantPublicProvider** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsTenantPublicProvider** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Vedere anche

#### Ulteriori risorse

[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md)

