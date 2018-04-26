---
title: Set-CsSite
TOCTitle: Set-CsSite
ms:assetid: f4165fdb-5828-4e81-b489-7e263b27e36b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413023(v=OCS.15)
ms:contentKeyID: 49302454
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSite

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le proprietà di un sito di Lync Server. I siti rappresentano una raccolta di pool di Lync Server e generalmente sono dislocati in diverse aree geografiche. Lync Server include due tipi di siti: siti data center e siti remoti (succursale). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsSite [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-DefaultPersistentChatPool <String>] [-Description <String>] [-DisplayName <String>] [-FederationRoute <String>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]] [-XmppFederationRoute <String>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 si modifica la proprietà Description per il sito di Redmond (-Identity Redmond).

    Set-CsSite -Identity Redmond -Description "Full-time employees in Redmond, WA."

## ESEMPIO 2

Nell'esempio 2 viene modificato il nome visualizzato per il sito di Redmond in "US Headquarters".

    Set-CsSite -Identity Redmond -DisplayName "US Headquarters"

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 vengono individuati tutti i siti che non dispongono di una proprietà Description, quindi si assegna a ognuno di tali siti una descrizione generica "Litwareinc.com". Per questo scopo, viene chiamato prima il cmdlet **Get-CsSite** senza parametri per restituire una raccolta di tutti i siti Lync Server. La raccolta restituita viene quindi inviata tramite pipe al cmdlet **Where-Object**, che preleva solo i siti con proprietà Description uguale a (-eq) un valore Null ($Null). Tali siti vengono quindi inviati tramite pipe al cmdlet **ForEach-Object**. Questo cmdlet sceglie ogni elemento della raccolta e utilizza il cmdlet **Set-CsSite** per modificare il valore della proprietà Description.

    Get-CsSite | Where-Object {$_.Description -eq $Null} | ForEach-Object {Set-CsSite $_.Identity -Description "Litwareinc.com"}

## Descrizione dettagliata

Lync Server 2010 ha introdotto un nuovo concetto nella topologia di Lync Server: i siti. I siti, da non confondere con i siti Active Directory o Microsoft Exchange Server) sono una raccolta di pool e server Lync Server generalmente organizzati in base all'area geografica e alla larghezza di banda della rete. Ad esempio, se tutti i computer di Redmond sono collocati nella stessa rete LAN con connessioni a bassa latenza ed elevata velocità, è possibile designare un sito di Redmond che includa quei computer. Se i computer di Dublino sono collocati in una specifica rete LAN e condividono connessioni a bassa latenza ed elevata velocità, è possibile anche un sito di Dublino separato. I siti svolgono inoltre un ruolo fondamentale nella gestione di Lync Server, poiché molti criteri e impostazioni possono essere configurati nell'ambito del sito, semplificando operazioni quali l'applicazione di un set di dial plan agli utenti di Redmond e di un set diverso di dial plan agli utenti di Dublino.

I siti vengono creati utilizzando lo Generatore di topologie ed eventuali modifiche all'infrastruttura del sito, come l'aggiunta di nuovi pool, devono essere apportate mediante questo strumento. È tuttavia possibile utilizzare il cmdlet **Set-CsSite** per modificare il nome visualizzato, la descrizione e la route di federazione di qualsiasi sito dell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsSite** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSite"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultPersistentChatPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente predefinito del sito.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di aggiungere ulteriori informazioni in un oggetto del sito. Ad esempio, Description può includere informazioni di contatto per il sito.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo del sito. Ad esempio: -DisplayName &quot;Nord America e Sud America&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>FederationRoute</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del server perimetrale utilizzata per fornire un collegamento tra la rete interna e Internet. Ad esempio: -FederationRoute &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome del sito da modificare, ad esempio: -Identity &quot;Redmond&quot;. Non utilizzare il formato &quot;site:Redmond&quot; per specificare l'identità.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppFederationRoute</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità del servizio di Edge Server utilizzato per la federazione XMPP (Extensible Messaging and Presence Protocol). Ad esempio:</p>
<p>-XmppFederationRoute EdgeServer:atl-xmpp-001.litwareinc.com</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsSite** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsSite** non restituisce oggetti o valori. Modifica le istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.Site+CentralSite.

## Vedere anche

#### Ulteriori risorse

[Get-CsSite](get-cssite.md)

