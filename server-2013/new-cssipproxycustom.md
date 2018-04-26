---
title: New-CsSipProxyCustom
TOCTitle: New-CsSipProxyCustom
ms:assetid: 3dc75cb0-c3d2-48bd-af32-2b2034b655dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425904(v=OCS.15)
ms:contentKeyID: 49300295
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyCustom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un'area di autenticazione personalizzata (Servizio di comunicazioni SIP) a una raccolta di impostazioni di configurazione dei server proxy. Le aree di autenticazione, conosciute anche come domini di protezione, vengono utilizzate per autenticare le credenziali utente durante l'accesso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyCustom -CustomValue <String>

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di assegnare un'area di autenticazione (Servizio di comunicazioni Litwareinc) a una variabile denominata $x.

    $x = New-CsSipProxyCustom -CustomValue "Litwareinc Communications Service"

## Descrizione dettagliata

Ogni server proxy deve essere associato a un'area di autenticazione. Le aree di autenticazione (note anche come domini di protezione) indicano dove devono essere elaborate le credenziali di accesso dell'utente. Per impostazione predefinita, Lync Server utilizza il Servizio di comunicazioni SIP come area di autenticazione predefinita. È tuttavia possibile modificare l'area di autenticazione utilizzata da un server proxy. Per ottenere questo risultato, viene creato un oggetto SipProxy.Custom che viene quindi assegnato alla proprietà Realm del server o dei server proxy appropriati. È possibile creare un'area di autenticazione personalizzata utilizzando il cmdlet **New-CsSipProxyCustom**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsSipProxyCustom** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyCustom"}

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
<td><p><em>CustomValue</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'area di autenticazione da utilizzare per le procedure di autenticazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyCustom** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipProxyCustom** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Custom.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyRealm](new-cssipproxyrealm.md)  
[New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

