---
title: Test-CsExStorageConnectivity
TOCTitle: Test-CsExStorageConnectivity
ms:assetid: 20fda110-5e09-4453-bb7b-a062abaab87f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204740(v=OCS.15)
ms:contentKeyID: 49299910
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExStorageConnectivity

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che il servizio di archiviazione di Lync Server funzioni in un Front End Server. A tale scopo, viene creato un messaggio di posta elettronica di prova nella cassetta postale di Exchange specificata e alla fine del test viene facoltativamente eliminato il messaggio. **Test-CsExStorageConnectivity** verifica inoltre che l'archiviazione di Exchange funzioni come previsto. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsExStorageConnectivity -SipUri <String> [-Binding <String>] [-DeleteItem <SwitchParameter>] [-Folder <ConversationHistory | Inbox | Dumpster>] [-Force <SwitchParameter>] [-HostNameStorageService <String>] [-UseCache <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica che il servizio di archiviazione di Lync Server sia in grado di connettersi alla cassetta postale di Exchange dell'utente sip:kenmyer@litwareinc.com. In questo esempio viene utilizzato NetNamedPipe come binding WCF.

    Test-CsExStorageConnectivity -SipUri "sip:kenmyer@litwareinc.com" -Binding "NetNamedPipe"

## Esempio 2

Nell'esempio 2 viene verificato che il servizio di archiviazione di Lync Server sia in grado di connettersi all'archivio in Exchange 2013. Si noti che questo comando avrà esito negativo se l'utente specificato non è stato abilitato per l'archiviazione Exchange. In questo esempio viene creata una connessione alla cartella Dumpster, ovvero la cartella di eliminazione Elementi ripristinabili che archivia gli elementi eliminati e non è visibile per gli utenti finali.

    Test-CsExStorageConnectivity -SipUri "sip:kenmyer@litwareinc.com" -Binding "NetNamedPipe" -Folder Dumpster

## Descrizione dettagliata

Il cmdlet **Test-CsExStorageConnectivity** viene utilizzato per verificare il corretto funzionamento dell'autenticazione da server a server tra Lync Server 2013 ed Exchange 2013. A tale scopo, il cmdlet esegue l'accesso a Exchange 2013, scrive un elemento nella cartella Cronologia conversazioni della cassetta postale specificata e quindi elimina l'elemento.

È inoltre possibile utilizzare il cmdlet **Test-CsExStorageConnectivity** per verificare che sia possibile connettersi all'archivio di archiviazione in Exchange 2013.

Se si riceve un messaggio di errore di accesso negato quando si esegue questo cmdlet, in genere significa che non si è membri del gruppo locale Amministratori utenti locali RTC. È possibile essere aggiunti a tale gruppo o al gruppo di Active Directory RTCUniversalUserAdmins (che è membro del gruppo Amministratori utenti locali RTC) per ottenere le autorizzazioni necessarie per eseguire il cmdlet **Test-CsExStorageConnectivity**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExStorageConnectivity"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsExStorageConnectivity** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>SipUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP della cassetta postale di Exchange 2013 in cui deve essere creato l'elemento di prova.</p></td>
</tr>
<tr class="even">
<td><p><em>Binding</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Binding Windows Communication Foundation (WCF). Un binding WCF determina i dettagli relativi al trasporto, alla codifica e ai protocolli necessari affinché i client e i servizi possano comunicare tra loro. I valori validi sono:</p>
<p>* NetNamedPipe</p>
<p>* NetTCP</p></td>
</tr>
<tr class="odd">
<td><p><em>DeleteItem</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, l'elemento di prova verrà eliminato dalla cassetta postale di Exchange 2013 alla fine del test.</p></td>
</tr>
<tr class="even">
<td><p><em>Folder</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Lyss.Cmdlets.ExchFolder</p></td>
<td><p>Specifica la cartella di archiviazione di Exchange 2013 a cui deve connettersi il cmdlet. I valori consentiti sono:</p>
<p>* ConversationHistory</p>
<p>* Inbox</p>
<p>* Dumpster</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>HostNameStorageService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del server in cui è in esecuzione il servizio di archiviazione di Lync Server. Questo parametro è obbligatorio se Binding è impostato su NetTCP.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCache</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato, questo parametro indica al cmdlet di utilizzare i risultati di individuazione automatica memorizzati nella cache quando tenta di connettersi a Exchange.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet Test-CsExStorageConnectivity non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsExStorageConnectivity** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ResourceData.

## Vedere anche

#### Ulteriori risorse

[Test-CsExStorageNotification](test-csexstoragenotification.md)

