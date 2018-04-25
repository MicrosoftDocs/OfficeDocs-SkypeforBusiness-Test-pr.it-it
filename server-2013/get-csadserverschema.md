---
title: Get-CsAdServerSchema
TOCTitle: Get-CsAdServerSchema
ms:assetid: fba777e5-886c-4914-a492-f2237721c57c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413070(v=OCS.15)
ms:contentKeyID: 49302554
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdServerSchema

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano se lo schema di Active Directory è stato configurato correttamente per consentire l'installazione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdServerSchema [-Report <String>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituito lo stato corrente dello schema del server Active Directory. Se lo schema è aggiornato, viene restituito il valore seguente: SCHEMA\_VERSION\_STATE\_CURRENT.

    Get-CsAdServerSchema

## ESEMPIO 2

Nell'esempio 2 viene restituito lo stato corrente dello schema del server Active Directory. Vengono anche fornite informazioni più dettagliate su tale schema in un file denominato C:\\Logs\\Server\_Schema.html. Tali informazioni includono aspetti quali la versione principale e la versione secondaria dello schema.

    Get-CsAdServerSchema -Report C:\Logs\Server_Schema.html

## Descrizione dettagliata

Non è possibile installare Lync Server se lo schema di Active Directory non è stato esteso correttamente, ovvero è necessario che gli oggetti e gli attributi specifici di Lync Server siano stati aggiunti a Servizi di dominio Active Directory prima di eseguire l'installazione. Ad esempio, gli oggetti account utente devono essere modificati per consentire l'utilizzo degli attributi che gestiscono aspetti quali l'indicazione del criterio vocale assegnato a un utente o la segnalazione che un account è stato abilitato o meno per VoIP aziendale.

Il cmdlet **Get-CsAdServerSchema** restituisce un singolo valore che indica se Active Directory è stato esteso e preparato per l'installazione di Lync Server. Se il cmdlet **Get-CsAdServerSchema** restituisce il valore SCHEMA\_VERSION\_STATE\_CURRENT, lo schema è stato esteso. Se invece il cmdlet restituisce qualsiasi altro valore, lo schema non è stato esteso.

Il cmdlet **Get-CsAdServerSchema** in genere viene eseguito come parte dell'installazione guidata. Se durante questa procedura viene rilevato che lo schema non è stato preparato correttamente, verrà visualizzato un messaggio di errore e l'installazione guidata si interromperà. È tuttavia possibile eseguire il cmdlet **Get-CsAdServerSchema** anche in modo indipendente dall'installazione guidata, per avere l'opportunità di verificare lo stato dello schema prima di provare a installare Lync Server.

Il cmdlet **Get-CsAdServerSchema** ha la stessa funzione del comando Microsoft Office Communications Server 2007 R2 seguente: Lcscmd.exe /domain /action:CheckSchemaPrepState.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, chiunque disponga delle autorizzazioni di lettura per Active Directory può eseguire il cmdlet **Get-CsAdServerSchema** in locale. In genere tutti i membri del dominio dispongono di questa autorizzazione.

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
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\SchemaPrep.html&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAdServerSchema** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsAdServerSchema** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deployment.SchemaVersionState.

## Vedere anche

#### Ulteriori risorse

[Install-CsAdServerSchema](install-csadserverschema.md)

