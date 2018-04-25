---
title: Test-CsCertificateConfiguration
TOCTitle: Test-CsCertificateConfiguration
ms:assetid: 8086bdf7-d283-4666-9f6c-0d5a3a31b3a6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398647(v=OCS.15)
ms:contentKeyID: 49301141
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsCertificateConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui certificati di Lync Server in uso nel computer locale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsCertificateConfiguration [-Report <String>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce informazioni sui certificati attualmente utilizzati (nel computer locale) da Lync Server.

    Test-CsCertificateConfiguration

## ESEMPIO 2

Il comando mostrato nell'esempio 2 è una variante del comando mostrato nell'esempio 1. In questo caso però viene utilizzato il parametro Report per specificare un percorso (C:\\Logs\\Certificates.xml) per il file di output generato durante l'esecuzione del cmdlet **Test-CsCertificateConfiguration**.

    Test-CsCertificateConfiguration -Report "C:\Logs\Certificates.xml"

## Descrizione dettagliata

Il cmdlet **Test-CsCertificateConfiguration** è un esempio di "transazione sintetica". Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Il cmdlet **Test-CsCertificateConfiguration** restituisce informazioni sui certificati utilizzati da Lync Server. Il cmdlet **Test-CsCertificateConfiguration** è destinato principalmente all'utilizzo da parte della Configurazione guidata certificati. È consigliabile che gli amministratori utilizzino il cmdlet **Get-CsCertificate** per recuperare le informazioni sui certificati.

Utenti che possono eseguire questo cmdlet: Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsCertificateConfiguration"}

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
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Certificates.html&quot;. Se il file esiste, viene sovrascritto durante l'esecuzione del cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsCertificateConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsCertificateConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deployment.CertificateExists.

## Vedere anche

#### Ulteriori risorse

[Get-CsCertificate](get-cscertificate.md)

