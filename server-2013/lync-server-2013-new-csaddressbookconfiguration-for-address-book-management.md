---
title: new-csaddressbookconfiguration per la gestione della rubrica
TOCTitle: new-csaddressbookconfiguration per la gestione della rubrica
ms:assetid: a58ddc8c-ae04-4141-b69e-e45374a67d72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429718(v=OCS.15)
ms:contentKeyID: 49301563
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# new-csaddressbookconfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet new-csaddressbookconfiguration: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "new-csaddressbookconfiguration"}

Il cmdlet new-csaddressbookconfiguration crea una nuova configurazione per la gestione del comportamento della Rubrica. Il cmdlet, in particolare, è in grado di definire se la Rubrica può creare i file di download del client, come e se utilizzare regole di normalizzazione, per quanto tempo conservare i file delta e delta compatti, nonché di definire la dimensione del file delta prima di incorporare una nuova creazione di file completa, l'ora di creazione della Rubrica del file completo e l'intervallo di sincronizzazione delle informazioni nel database degli utenti.

Ad esempio:

    new-csaddressbookconfiguration -Identity site:Redmond -KeepDuration 15 -SynchronizePollingInterval 00:10:00

Per una descrizione dettagliata del comando completo, fare riferimento all'argomento seguente nella documentazione di riferimento principale per i cmdlet RTC di Windows PowerShell per Lync Server.

## Vedere anche

#### Ulteriori risorse

[new-csaddressbookconfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAddressBookConfiguration)

