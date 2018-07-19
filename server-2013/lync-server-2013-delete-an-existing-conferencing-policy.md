---
title: Eliminare i criteri per le conferenze esistenti
TOCTitle: Eliminare i criteri per le conferenze esistenti
ms:assetid: 709ed771-790f-4bf1-a4de-b37ca5168688
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688089(v=OCS.15)
ms:contentKeyID: 49887603
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare i criteri per le conferenze esistenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Eseguire questa procedura per eliminare un criterio di conferenza a livello di utente o di sito.


> [!NOTE]
> Non è possibile eliminare il criterio di conferenza globale.



## Per eliminare un criterio di conferenza a livello di utente o di sito

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Criteri conferenza**.

4.  Nell'elenco dei criteri relativi alle conferenze, fare clic sul criterio utente o sito che si desidera eliminare, su Modifica e quindi su Elimina.

## Rimozione di criteri di conferenza attraverso i cmdlet di Lync Server Management Shell

È inoltre possibile eliminare impostazioni di configurazione del trunk utilizzando i cmdlet Lync Server Management Shell e **Remove-CsConferencingPolicy**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere un criterio di conferenza specifico.

  - Il comando seguente rimuove il criterio di conferenza con identità (Identity) RedmondConferencingPolicy.
    
        Remove-CsConferencingPolicy -Identity "RedmondConferencingPolicy"

## Per rimuovere tutti i criteri di conferenza applicati all'ambito "per utente"

  - Questo comando rimuove tutti i criteri di conferenza configurati nell'ambito "per utente":
    
        Get-CsConferencingPolicy -Filter "tag:*" | Remove-CsConferencingPolicy

## Per rimuovere tutti i criteri di conferenza che consentono la registrazione da parte degli utenti esterni

  - Questo comando rimuove tutti i criteri di conferenza configurati che consentono la registrazione da parte degli utenti esterni:
    
        Get-CsConferencingPolicy | Where-Object {$_.AllowExternalUsersToRecordMeetings -eq $True} | Remove-CsConferencingPolicy

Per informazioni dettagliate, vedere [Remove-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsConferencingPolicy).

