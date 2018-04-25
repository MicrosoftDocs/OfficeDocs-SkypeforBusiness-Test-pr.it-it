---
title: Get-CsPinPolicy
TOCTitle: Get-CsPinPolicy
ms:assetid: 1d627ba5-6333-466c-82a1-859deaf8d690
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398262(v=OCS.15)
ms:contentKeyID: 49299869
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPinPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui criteri PIN client configurati per l'utilizzo nell'organizzazione. L'autenticazione tramite PIN consente agli utenti di accedere a Lync Server immettendo il proprio PIN anziché il nome utente e la password. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsPinPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPinPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce una raccolta di tutti i criteri PIN configurati per l'utilizzo nell'organizzazione. Se si chiama il cmdlet **Get-CsPinPolicy** senza alcun parametro, verrà sempre restituita la serie completa di criteri PIN.

    Get-CsPinPolicy

## ESEMPIO 2

L'Esempio 2 restituisce un singolo criterio dei PIN: il criterio con Identity site:Redmond.

    Get-CsPinPolicy -Identity "site:Redmond"

## ESEMPIO 3

Il comando riportato nell'esempio 3 utilizza il parametro Filter per restituire tutti i criteri che sono stati configurati nell'ambito per utente. A tale scopo, viene utilizzato il valore di filtro "tag:\*". Questo valore indica al cmdlet **Get-CsPinPolicy** di restituire solo i criteri la cui identità inizia con la stringa "tag:".

    Get-CsPinPolicy -Filter "tag:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti i criteri PIN in cui la proprietà AllowCommonPatterns è impostata su True. In questo esempio viene innanzitutto chiamato il cmdlet **Get-CsPinPolicy** senza parametri aggiuntivi. Viene così restituita una raccolta di tutti i criteri PIN configurati per l'utilizzo nell'organizzazione. La raccolta così ottenuta viene quindi passata al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà AllowCommonPatterns è uguale a True.

    Get-CsPinPolicy | Where-Object {$_.AllowCommonPatterns -eq $True}

## ESEMPIO 5

Come nell'esempio 4, il comando riportato nell'esempio 5 utilizza il cmdlet **Where-Object** per restituire un sottoinsieme dei criteri PIN esistenti. In questo caso, il cmdlet **Where-Object** recupera solo i criteri per i quali la proprietà PinLifetime è maggiore di 30. Ciò significa che verranno restituiti soli i criteri PIN con scadenza superiore ai 30 giorni.

    Get-CsPinPolicy | Where-Object {$_.PinLifetime -gt 30}

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. In genere, l'accesso al sistema o la partecipazione a una conferenza richiedono l'immissione del nome utente e della password. Tale operazione può rappresentare un problema se si utilizza un telefono privo di tastierino alfanumerico. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché il nome utente e la password.

In Lync Server vengono utilizzati i criteri per il PIN per gestire le proprietà di autenticazione tramite PIN. È ad esempio possibile specificare una lunghezza minima per un codice PIN e stabilire se sono accettabili i PIN che utilizzano "formati comuni", come cifre consecutive (ad esempio, il PIN 123456). È possibile utilizzare il cmdlet **Get-CsPinPolicy** per recuperare le informazioni sui criteri per il PIN attualmente configurati per l'utilizzo nella propria organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsPinPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPinPolicy"}

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
<td><p>Consente di utilizzare i caratteri jolly per ricercare i criteri dei PIN. Ad esempio, per trovare tutti i criteri configurati nell'ambito del sito, utilizzare il seguente valore per Filter: site:*. Per trovare i criteri nell'abito dei siti Seattle, Seville e Saskatoon (tutti nomi che iniziano con la lettera &quot;S&quot;), utilizzare il seguente filtro: site:S*. Si noti che questo parametro può filtrare solo i valori della proprietà Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca assegnata al criterio al momento della creazione. È possibile assegnare i criteri relativi ai PIN in ambito globale, del sito o per utente. Per fare riferimento all'istanza globale, utilizzare la seguente sintassi: -Identity global. Per fare riferimento a un criterio nell'ambito del sito, utilizzare la seguente sintassi: -Identity site:Redmond. Per fare riferimento a un criterio nell'ambito per utente, utilizzare una sintassi simile alla seguente: -Identity RedmondPolicy.</p>
<p>Non è possibile utilizzare i caratteri jolly, come l'asterisco (*), con il parametro Identity. Per cercare i criteri utilizzando i caratteri jolly, utilizzare il parametro Filter.</p>
<p>Se non si specifica né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPinPolicy</strong> restituirà le informazioni su tutti i criteri PIN configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei criteri per il PIN dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPinPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsPinPolicy** restituisce una o più istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPinPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

