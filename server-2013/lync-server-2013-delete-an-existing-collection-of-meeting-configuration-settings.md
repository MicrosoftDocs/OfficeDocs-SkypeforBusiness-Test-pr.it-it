---
title: Eliminare una raccolta esistente di impostazioni di configurazione delle riunioni
TOCTitle: Eliminare una raccolta esistente di impostazioni di configurazione delle riunioni
ms:assetid: 92ff8a91-05c5-4047-a533-5dff12f22299
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688136(v=OCS.15)
ms:contentKeyID: 49887658
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta esistente di impostazioni di configurazione delle riunioni

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile eliminare una configurazione utente o sito. La configurazione globale non può essere rimossa. Se si elimina la configurazione globale, essa viene automaticamente reimpostata sui valori predefiniti.

## Per eliminare una configurazione utente o sito per le riunioni

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Configurazione riunione** .

4.  Nell'elenco delle configurazioni delle riunioni, fare clic sulla configurazione di sito o pool da eliminare, fare clic su Modifica e quindi su Elimina.

## Rimozione delle impostazioni di configurazione delle riunioni mediante i cmdlet di PowerShell per Lync Server

Le impostazioni delle riunioni possono anche essere eliminate mediante Windows PowerShell e il cmdlet Remove-CsMeetingConfiguration. Questo cmdlet può essere eseguito dalla Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Rimozione di una raccolta specificata di impostazioni di configurazione delle riunioni

  - Questo comando rimuove le impostazioni di configurazione delle riunioni applicati al sito Redmond:
    
        Remove-CsMeetingConfiguration -Identity "site:Redmond"

## Rimozione di tutte le impostazioni di configurazione delle riunioni applicate all'ambito del sito

  - Questo comando rimuove tutte le impostazioni di configurazione delle riunioni applicate all'ambito del sito:
    
        Get-CsMeetingConfiguration -Filter "site:*" | Remove-CsMeetingConfiguration

## Rimozione di tutte le impostazioni di configurazione delle riunioni che ammettono utenti anonimi per impostazione predefinita

  - Questo rimuove tutte le impostazioni che consentono agli utenti anonimi di essere ammessi per impostazione predefinita:
    
        Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $True} | Remove-CsMeetingConfiguration

Per ulteriori informazioni, vedere l'argomento della Guida relativa al cmdlet [Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md).

