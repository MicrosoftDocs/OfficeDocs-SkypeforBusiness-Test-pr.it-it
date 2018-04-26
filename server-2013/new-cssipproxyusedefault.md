---
title: New-CsSipProxyUseDefault
TOCTitle: New-CsSipProxyUseDefault
ms:assetid: 1e8bedca-8bd5-4559-b530-0f18ae23d6d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398274(v=OCS.15)
ms:contentKeyID: 49299883
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyUseDefault

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna l'area di autenticazione predefinita (Servizio di comunicazioni SIP) a una raccolta di impostazioni di configurazione dei server proxy. Le aree di autenticazione, conosciute anche come domini di protezione, vengono utilizzate per autenticare le credenziali utente durante l'accesso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyUseDefault

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di assegnare l'area di autenticazione (Servizio di comunicazioni SIP) a una variabile denominata $x.

    $x = New-CsSipProxyUseDefault

## Descrizione dettagliata

I server proxy consentono agli utenti esterni di accedere alle risorse della rete interna. Ogni server proxy deve essere associato a un'area di autenticazione. Le aree di autenticazione, conosciute anche come domini di protezione, indicano dove devono essere elaborate le credenziali di accesso di un 'utente. Per impostazione predefinita, Lync Server utilizza il Servizio di comunicazioni SIP come area di autenticazione predefinita. È tuttavia possibile modificare l'area di autenticazione utilizzata da un server proxy. Se l'area di autenticazione viene modificata e successivamente si desidera ripristinare l'area predefinita, creare un oggetto SipProxy.UseDefault e quindi assegnarlo alla proprietà Realm del server o dei server proxy appropriati.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsSipProxyUseDefault** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyUseDefault"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce unicamente parametri comuni di Windows PowerShell.</p>
<p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyUseDefault** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipProxyUseDefault** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.UseDefault.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyCustom](new-cssipproxycustom.md)  
[New-CsSipProxyRealm](new-cssipproxyrealm.md)

