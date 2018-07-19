---
title: Definire gli insiemi di festività dei Response Group (facoltativo)
TOCTitle: Definire gli insiemi di festività dei Response Group (facoltativo)
ms:assetid: 56c37b3b-6517-49b9-86b7-ae48cc349119
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688063(v=OCS.15)
ms:contentKeyID: 49887570
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire gli insiemi di festività dei Response Group (facoltativo)

 

_**Ultima modifica dell'argomento:** 2014-02-07_

Le impostazioni delle festività consentono di definire i giorni in cui il Response Group non è operativo e di specificare l'azione da effettuare in questi giorni. Un set di festività è la raccolta delle festività che si applicano a un Response Group.


> [!NOTE]
> Se un flusso di lavoro è definito come flusso di lavoro gestito, tutti gli utenti con il ruolo CsResponseGroupManager possono impostare e modificare le festività per i flussi di lavoro che gestiscono.



## Per creare un set di festività

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per ogni festività che si vuole definire, eseguire:
    
        $x = New-CsRgsHoliday [-Name <holiday name>] -StartDate <starting date of holiday> -EndDate <ending date of holiday>
    
    Per creare il set di festività che contiene le festività definite, eseguire:
    
        New-CsRgsHolidaySet -Parent <service where the workflow is hosted> -Name <unique name for holiday set> -HolidayList <one or more holidays to be included in the holiday set>
    
    Nell'esempio seguente viene illustrato un set di festività che include due festività:
    
        $a = New-CsRgsHoliday -Name "New Year's Day" -StartDate "1/1/2013 12:00 AM" -EndDate "1/1/2013 12:00 AM" 
        $b = New-CsRgsHoliday -Name "Independence Day" -StartDate "7/4/2013 12:00 AM" -EndDate "7/5/2013 12:00 AM" 
        New-CsRgsHolidaySet -Parent "ApplicationServer:Redmond.contoso.com -Name "2013 Holidays" -HolidayList ($a, $b)

## Vedere anche

#### Concetti

[Creare o modificare un flusso di lavoro di un gruppo di risposta in Lync Server 2013](lync-server-2013-create-or-modify-a-hunt-group-workflow.md)  
[Creare o modificare un flusso di lavoro interattivo in Lync Server 2013](lync-server-2013-create-or-modify-an-interactive-workflow.md)  

#### Ulteriori risorse

[New-CsRgsHoliday](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsHoliday)  
[New-CsRgsHolidaySet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsHolidaySet)

