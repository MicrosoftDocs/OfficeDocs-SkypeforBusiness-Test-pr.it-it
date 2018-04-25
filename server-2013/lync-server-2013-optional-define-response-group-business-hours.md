---
title: "Lync Server 2013: Definire l'orario di ufficio dei Response Group (facoltativo)"
TOCTitle: Definire l'orario di ufficio dei Response Group (facoltativo)
ms:assetid: d62551b2-1847-4e1b-abe8-683b72aa94d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205291(v=OCS.15)
ms:contentKeyID: 49302102
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire l'orario di ufficio dei Response Group (facoltativo) in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

## Definizione dell'orario di ufficio

Le impostazioni relative all'orario di ufficio consentono di definire quando è disponibile il flusso di lavoro per rispondere alle chiamate e di specificare le azioni da eseguire per le chiamate ricevute al di fuori dell'orario di ufficio. Gli amministratori di Response Group possono utilizzare il cmdlet **New-CsRgsHoursOfBusiness** per creare pianificazioni predefinite da utilizzare per qualsiasi numero di Response Group.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Quando si crea o si modifica un flusso di lavoro, è possibile specificare una pianificazione personalizzata da applicare solo a tale flusso di lavoro. Per informazioni dettagliate, vedere <a href="lync-server-2013-create-or-modify-a-hunt-group-workflow.md">Creare o modificare un flusso di lavoro di un gruppo di risposta in Lync Server 2013</a> o <a href="lync-server-2013-create-or-modify-an-interactive-workflow.md">Creare o modificare un flusso di lavoro interattivo in Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se un flusso di lavoro viene definito come flusso di lavoro gestito, gli utenti a cui è stato assegnato il ruolo CsResponseGroupManager possono impostare e modificare un orario di ufficio personalizzato per i flussi di lavoro gestiti.



<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Utilizzare il formato 24 ore per i parametri dei cmdlet seguenti, ad esempio 20:00 = 8:00 di sera.</td>
</tr>
</tbody>
</table>


## Per creare una raccolta di orari di ufficio predefinita

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per ogni intervallo univoco di ore che si desidera definire, eseguire:
    
        $x = New-CsRgsTimeRange [-Name <name of time range>] -OpenTime <time when business hours begin> -CloseTime <time when business hours end>
    
    Per creare la raccolta di orari di ufficio che utilizza gli intervalli definiti, eseguire:
    
        New-CsRgsHoursOfBusiness -Parent <service where the workflow is hosted> -Name <unique name for collection> [-MondayHours1 <first set of opening and closing times for Monday>] [-MondayHours2 <second set of opening and closing times for Monday>] [-TuesdayHours1 <first set of opening and closing times for Tuesday>] [-TuesdayHours2 <second set of opening and closing times for Tuesday>] [-WednesdayHours1 <first set of opening and closing times for Wednesday>] [-WednesdayHours2 <second set of opening and closing times for Wednesday>] [-ThursdayHours1 <first set of opening and closing times for Thursday>] [-ThursdayHours2 <second set of opening and closing times for Thursday>] [-FridayHours1 <first set of opening and closing times for Friday>] [-FridayHours2 <second set of opening and closing times for Friday>] [-SaturdayHours1 <first set of opening and closing times for Saturday>] [-SaturdayHours2 <second set of opening and closing times for Saturday>] [-SundayHours1 <first set of opening and closing times for Sunday>] [-SundayHours2 <second set of opening and closing times for Sunday>]
    
    Nell'esempio seguente viene specificato un orario di ufficio dalle 9.00 alle 17.00 per i giorni feriali e dalle 8.00 alle 10.00 e di nuovo dalle 14.00 alle 18.00 per il sabato, senza nessun orario di ufficio per la domenica:
    
        $a = NewRgsTimeRange -Name "Weekday Hours" -OpenTime "9:00" -CloseTime "17:00"
        $b = NewRgsTimeRange -Name "Saturday Morning Hours" -OpenTime "8:00" -CloseTime "10:00" 
        $c = NewRgsTimeRange -Name "Saturday Afternoon Hours" -OpenTime "14:00" -CloseTime "18:00" 
        New-CsRgsHoursOfBusiness -Parent "ApplicationServer:Redmond.contoso.com" -Name "Help Desk Business Hours" -MondayHours1 $a -TuesdayHours1 $a -WednesdayHours1 $a -ThursdayHours1 $a -FridayHours1 $a -SaturdayHours1 $b -SaturdayHours2 $c

## Vedere anche

#### Concetti

[Creare o modificare un flusso di lavoro di un gruppo di risposta in Lync Server 2013](lync-server-2013-create-or-modify-a-hunt-group-workflow.md)  
[Creare o modificare un flusso di lavoro interattivo in Lync Server 2013](lync-server-2013-create-or-modify-an-interactive-workflow.md)  

#### Ulteriori risorse

[New-CsRgsTimeRange](new-csrgstimerange.md)  
[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)

