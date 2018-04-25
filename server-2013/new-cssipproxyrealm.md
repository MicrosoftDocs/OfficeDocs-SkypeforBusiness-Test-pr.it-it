---
title: New-CsSipProxyRealm
TOCTitle: New-CsSipProxyRealm
ms:assetid: fedf9c71-5a23-4818-9f98-db5008a2ba74
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413084(v=OCS.15)
ms:contentKeyID: 49302583
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyRealm

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna l'area di autenticazione predefinita (Servizio di comunicazioni SIP) a una raccolta di impostazioni di configurazione dei server proxy. Le aree di autenticazione, conosciute anche come domini di protezione, vengono utilizzate per autenticare le credenziali utente durante l'accesso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipProxyRealm -RealmChoice <IRealmChoice>

## Esempi

## ESEMPIO 1

Con i comandi mostrati nell'esempio 1 viene assegnata l'area di autenticazione predefinita (Servizio di comunicazioni SIP) a una variabile denominata $y. Per questo scopo, il primo comando chiama il cmdlet **New-CsSipProxyUseDefault** per creare un oggetto SipProxy.UseDefault, che viene memorizzato in una variabile denominata $x.

Nel secondo comando, la variabile $x viene utilizzata come valore per il parametro del cmdlet **New-CsSipProxyRealm** e il parametro RealmChoice. In questo modo viene creato un nuovo oggetto area di autenticazione del proxy che viene memorizzato in una variabile denominata $y.

    $x = New-CsSipProxyUseDefault
    $y = New-CsSipProxyRealm -RealmChoice $x

## ESEMPIO 2

Con i comandi mostrati nell'esempio 2 viene assegnata l'area di autenticazione personalizzata (Servizio di comunicazioni Litwareinc) a una variabile denominata $y. Per questo scopo, il primo comando chiama il cmdlet **New-CsSipProxyCustom** per creare un oggetto SipProxy.Custom (che utilizza il Servizio di comunicazioni CustomValue Litwareinc), che viene memorizzato in una variabile denominata $x.

Nel secondo comando viene utilizzata la variabile $x insieme al cmdlet **New-CsSipProxyRealm** e al parametro RealmChoice per creare un nuovo oggetto area di autenticazione personalizzata.

    $x = New-CsSipProxyCustom -CustomValue "Litwareinc Communications Service"
    $y = New-CsSipProxyRealm -RealmChoice $x

## Descrizione dettagliata

I server proxy consentono agli utenti che si trovano al di fuori della rete interna di accedere alle risorse disponibili nella rete interna. Ogni server proxy deve essere associato a un'area di autenticazione, anche nota come dominio di protezione, che indica quando elaborare le credenziali di accesso di un utente. Per impostazione predefinita, in Lync Server viene utilizzato il Servizio di comunicazioni SIP quale area di autenticazione predefinita. Tuttavia, è possibile modificare l'area di autenticazione utilizzata da un server proxy. Il cmdlet **New-CsSipProxyUseDefault** e il cmdlet **New-CsSipProxyCustom** consentono di modificare l'area di autenticazione utilizzata da un server proxy. Queste modifiche possono anche essere eseguite utilizzando il cmdlet **New-CsSipProxyRealm**. Tuttavia, poiché questo cmdlet richiede un passaggio aggiuntivo, può essere consigliabile utilizzare gli altri due cmdlet ogni volta che è necessario modificare l'area di autenticazione utilizzata da un server proxy.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsSipProxyRealm** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyRealm"}

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
<td><p><em>RealmChoice</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.IRealmChoice</p></td>
<td><p>Oggetto che rappresenta l'area di autenticazione che deve essere utilizzata da un server proxy. È necessario creare RealmChoice utilizzando il cmdlet <strong>New-CsSipProxyUseDefault</strong> o il cmdlet <strong>New-CsSipProxyCustom</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSipProxyRealm** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsSipProxyRealm** consente di creare nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Realm.

## Vedere anche

#### Ulteriori risorse

[New-CsSipProxyCustom](new-cssipproxycustom.md)  
[New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

