---
title: Get-CsTenantLicensingConfiguration
TOCTitle: Get-CsTenantLicensingConfiguration
ms:assetid: 0df23143-f1aa-4850-b0f7-750422762925
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362770(v=OCS.15)
ms:contentKeyID: 56269882
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantLicensingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Indica se le informazioni sulle licenze per il tenant specificato sono disponibili nell'interfaccia di amministrazione di Lync.

Questo cmdlet può essere usato solo con Lync Online.

## Sintassi

    Get-CsTenantLicensingConfiguration [-Filter] <Object>] [-Identity] <Object>] [-Tenant] <Object>] [-LocalStore]

## Descrizione dettagliata

Il cmdlet Get-CsTenantLicensingConfiguration indica se le informazioni sulle licenze per il tenant specificato sono disponibili nell'interfaccia di amministrazione di Lync. Il cmdlet restituisce informazioni simili alle seguenti:

Identity: Global  
Status: Enabled

Se Status è uguale a Enabled, le informazioni sulle licenze sono disponibili nell'interfaccia di amministrazione di Lync. In caso contrario tali non lo sono.

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
<td><p><strong>Filter</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per ottenere una raccolta di impostazioni di configurazione delle licenze del tenant. Poiché ogni tenant è limitato a una singola raccolta globale di impostazioni di configurazione delle licenze, non è necessario usare il parametro Filter.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Specifica la raccolta di impostazioni di configurazione delle licenze del tenant da restituire. Poiché ogni tenant è limitato a una singola raccolta globale di impostazioni delle licenze, non è necessario includere questo parametro quando si chiama il cmdlet Get-CsTenantLicensingConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalStore</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione delle licenze del tenant dalla replica locale dell'archivio di gestione centrale, anziché l'archivio stesso.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tenant</strong></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di cui vengono restituite le impostazioni delle licenze. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Eseguendo questo comando è possibile ottenere l'ID di ogni tenant:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet Get-CsTenantLicensingConfiguration non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet Get-CsTenantLicensingConfiguration restituisce istanze dell'oggetto Deserialized.Microsoft.Rtc.Management.WritableConfig.Settings.TenantConfiguration.TenantLicensingConfiguration.

## Esempio

Il comando illustrato nell'esempio 1 restituisce informazioni di configurazione delle licenze per il tenant corrente:

    Get-CsTenantLicensingConfiguration

