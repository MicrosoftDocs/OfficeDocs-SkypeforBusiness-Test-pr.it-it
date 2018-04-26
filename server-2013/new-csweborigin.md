---
title: New-CsWebOrigin
TOCTitle: New-CsWebOrigin
ms:assetid: 16053a99-b5ff-45e1-be95-b04e3f2fe528
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ950236(v=OCS.15)
ms:contentKeyID: 52062099
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebOrigin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo oggetto dominio che può essere aggiunto alla raccolta di domini a cui è consentito inviare richieste di script tra domini alla distribuzione di Lync Server 2013.

Questo cmdlet è stato introdotto negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.

## Sintassi

    New-CsWebOrigin -Url <String>

## Esempi

## Esempio 1

I comandi illustrati nell'esempio 1 consentono di aggiungere il dominio http://fabrikam.com a una nuova raccolta di impostazioni di configurazione del servizio Web creata per il sito Redmond. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsWebOrigin** per creare un oggetto dominio per fabrikam.com. L'oggetto dominio risultante viene archiviato in una variabile denominata $x.

Il secondo comando nell'esempio utilizza il cmdlet **New-CsWebServiceConfiguration** per creare le impostazioni di configurazione del servizio Web per il sito Redmond. La sintassi "-CrossDomainAuthorizationList $x" aggiunge http://fabrikam.com alla raccolta di domini autorizzati per l'esecuzione di script tra domini.

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    New-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $x

## Esempio 2

I comandi illustrati nell'esempio 2 consentono di aggiungere il dominio http://fabrikam.com a una raccolta esistente di impostazioni di configurazione del servizio Web. Per eseguire questa attività, il primo comando nell'esempio utilizza il cmdlet **New-CsWebOrigin** per creare un oggetto dominio per fabrikam.com. L'oggetto dominio risultante viene archiviato in una variabile denominata $x.

Il secondo comando nell'esempio utilizza il cmdlet **Set-CsWebServiceConfiguration** per aggiungere http://fabrikam.com alle impostazioni di configurazione del servizio Web applicate al sito Redmond. La sintassi @{Add=$x} aggiunge il dominio ai domini già presenti nella raccolta di domini autorizzati per l'esecuzione di script tra domini. Per sostituire la raccolta esistente con http://fabrikam.com, utilizzare la sintassi @{Replace=$x}.

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    Set-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList @{Add=$x}

## Descrizione dettagliata

Il cmdlet New-CsWebOrigin consente di specificare domini autorizzati ad ospitare applicazioni Web che a loro volto possono inviare richieste di script tra domini alla distribuzione di Lync Server 2013. Questo cmdlet viene utilizzato principalmente per le applicazioni create sulla base dell'API Web Unified Communications.

Per aggiungere un dominio a una raccolta di impostazioni di configurazione del servizio Web, creare innanzitutto un oggetto dominio utilizzando il cmdlet New-CsWebOrigin. Questo oggetto dominio, che esiste solo in memoria, deve essere archiviato in una variabile. Dopo che è stato creato, l'oggetto può essere aggiunto a una raccolta di impostazioni di configurazione del servizio Web utilizzando il cmdlet New-CsWebServiceConfiguration o Set-CsWebServiceConfiguration.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets -match "New-CsWebOrigin"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsWebOrigin** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Url</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URL del dominio autorizzato a inviare richieste di script tra domini. Gli URL devono essere preceduti dal prefisso http: o https:. Ad esempio:</p>
<p>-Url &quot;http://contoso.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsWebOrigin** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsWebOrigin** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.Origin.

## Vedere anche

#### Ulteriori risorse

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

