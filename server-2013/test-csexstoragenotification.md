---
title: Test-CsExStorageNotification
TOCTitle: Test-CsExStorageNotification
ms:assetid: d8fe3b22-7a76-4d70-9bc1-b54b37f68449
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205331(v=OCS.15)
ms:contentKeyID: 49302157
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExStorageNotification

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che il servizio di archiviazione di Lync Server eseguito in un Front End Server sia in grado di eseguire la sottoscrizione al servizio di notifica della cassetta postale di Microsoft Exchange Server 2013. A tal fine, il cmdlet esegue la sottoscrizione al servizio, crea un elemento, verifica che venga ricevuta la notifica del nuovo elemento e quindi, facoltativamente, elimina l'elemento e annulla la sottoscrizione al servizio. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsExStorageNotification -SipUri <String> [-Binding <String>] [-DeleteItem <SwitchParameter>] [-Force <SwitchParameter>] [-HostNameStorageService <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 testa se il servizio di archiviazione di Lync Server può connettersi al servizio di notifica della cassetta postale per l'utente sip:kenmyer@litwareinc.com. In questo esempio NetNamedPipe è utilizzato come associazione WCF.

    Test-CsExStorageNotification -SipUri "sip:kenmyer@litwareinc.com" -Binding "NetNamedPipe"

## Descrizione dettagliata

Il cmdlet **Test-CsExStorageNotification** viene utilizzato per verificare che il servizio di notifica di Microsoft Exchange Server 2013 sia in grado di notificare in qualsiasi momento a Lync Server 2013 gli aggiornamenti effettuati nell'elenco contatti di un utente. Questo cmdlet è valido solo se si utilizza l'archivio contatti unificato.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExStorageNotification"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsExStorageNotification** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indirizzo SIP della cassetta postale di Exchange Server in cui deve essere creato l'elemento di test.</p></td>
</tr>
<tr class="even">
<td><p><em>Binding</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Associazione Windows Communication Foundation (WCF). Un'associazione WCF determina i dettagli di trasporto, codifica e protocollo richiesti perché client e servizi comunichino tra loro. I valori validi sono:</p>
<p>* NetNamedPipe</p>
<p>* NetTCP</p></td>
</tr>
<tr class="odd">
<td><p><em>DeleteItem</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, l'elemento di test verrà eliminato dalla cassetta postale di Exchange alla fine del testo.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HostNameStorageService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del server in cui è in esecuzione il servizio di archiviazione di Lync Server. Questo parametro è obbligatorio se Binding è impostato su NetTCP.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsExStorageNotification** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsExStorageNotification** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.Xds.ResourceData.

## Vedere anche

#### Ulteriori risorse

[Test-CsExStorageConnectivity](test-csexstorageconnectivity.md)

