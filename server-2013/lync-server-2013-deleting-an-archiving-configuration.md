---
title: Eliminazione della configurazione di archiviazione
TOCTitle: Eliminazione della configurazione di archiviazione
ms:assetid: a8744d39-5cf2-474c-9a99-a0f3a37f846f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205167(v=OCS.15)
ms:contentKeyID: 49301588
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione della configurazione di archiviazione

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile eliminare la configurazione di un sito o la configurazione di un pool. La configurazione globale non può essere rimossa. Se si elimina la configurazione globale, viene reimpostata automaticamente sui valori predefiniti. Per informazioni dettagliate sulle modalità di implementazione delle configurazioni di archiviazione, incluse le opzioni che è possibile specificare e la gerarchia di tali configurazioni, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.

## Per eliminare la configurazione di un sito o di un pool per l'archiviazione

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Nell'elenco delle configurazioni di archiviazione fare clic sulla configurazione di sito o di pool che si desidera eliminare, fare clic su **Modifica** e quindi su **Elimina**.

5.  Fare clic su **Commit**.

## Rimozione delle impostazioni della configurazione di archiviazione mediante i cmdlet di Lync Server Management Shell

È possibile eliminare le impostazioni della configurazione di archiviazione anche utilizzando Windows PowerShell e il cmdlet Remove-CsArchivingConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.

## Rimozione di una raccolta specifica di impostazioni della configurazione di archiviazione

  - Il comando seguente rimuove le impostazioni della configurazione di archiviazione applicate al sito Redmond:
    
        Remove-CsArchivingConfiguration -Identity "site:Redmond"

## Rimozione di tutte le impostazioni della configurazione di archiviazione applicate all'ambito del sito

  - Questo comando rimuove tutte le impostazioni della configurazione di archiviazione applicate all'ambito del servizio:
    
        Get-CsArchivingConfiguration -Filter "site:*" | Remove-CsArchivingConfiguration

## Rimozione delle impostazioni della configurazione di archiviazione in base a un valore specifico di una proprietà

  - Questo comando rimuove tutte le impostazioni della configurazione di archiviazione in cui l'archiviazione di Exchange è stata disabilitata:
    
        Get-CsArchivingConfiguration | Where-Object {$_.EnableExchangeArchiving -eq $False} | Remove-CsArchivingConfiguration

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Remove-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsArchivingConfiguration).

## Vedere anche

#### Concetti

[Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md)  

#### Ulteriori risorse

[Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

