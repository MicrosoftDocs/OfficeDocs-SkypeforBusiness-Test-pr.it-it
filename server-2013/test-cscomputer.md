---
title: Test-CsComputer
TOCTitle: Test-CsComputer
ms:assetid: 0b33d951-510d-445c-9b01-c6431fda6d47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398162(v=OCS.15)
ms:contentKeyID: 49299641
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Test-CsComputer** verifica lo stato dei servizi di Lync Server in esecuzione nel computer locale. Questo cmdlet verifica inoltre che siano stati aggiunti i gruppi di Active Directory per Lync Server appropriati nei corrispondenti gruppi locali nel computer e che siano state aperte le porte firewall del computer necessarie. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsComputer [-Report <String>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di verificare lo stato di attivazione del servizio per il computer locale. Nel comando è incluso il parametro Verbose per fare in modo che l'esecuzione positiva o negativa del comando venga interamente visualizzata sullo schermo.

    Test-CsComputer -Verbose

## ESEMPIO 2

Nell'esempio 2 viene anche verificato lo stato di attivazione del servizio nel computer locale. Questo comando inoltre scrive informazioni dettagliate sullo stato di attivazione nel file C:\\Logs\\Computer.html. Questo file di log viene generato includendo il parametro Report seguito dal percorso completo del file di log in cui devono essere scritte le informazioni.

    Test-CsComputer -Verbose -Report C:\Logs\Computer.html

## Descrizione dettagliata

Il cmdlet **Test-CsComputer** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, ad esempio l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono sulla rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Il cmdlet **Test-CsComputer**, che può essere eseguito solo nel computer locale, verifica lo stato di tutti i servizi di Lync Server nel computer. Controlla inoltre che nel computer siano state aperte le porte firewall appropriate e stabilisce se i gruppi di Active Directory creati al momento dell'installazione di Lync Server sono stati aggiunti ai corrispondenti gruppi locali. Il cmdlet **Test-CsComputer** ad esempio verifica che il gruppo di Active Directory RTCUniversalUserAdmins sia stato aggiunto al gruppo Administrators locale.

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
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Computer.html&quot;. Se questo file esiste, viene sovrascritto quando viene eseguito il cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsComputer** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsComputer** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)

