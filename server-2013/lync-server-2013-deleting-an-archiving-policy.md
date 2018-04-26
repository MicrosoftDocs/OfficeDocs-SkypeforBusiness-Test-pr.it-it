---
title: Eliminazione dei criteri di archiviazione
TOCTitle: Eliminazione dei criteri di archiviazione
ms:assetid: 4739a691-41cc-4128-8bb8-6d5a4c02107a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520989(v=OCS.15)
ms:contentKeyID: 49300395
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione dei criteri di archiviazione

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile eliminare un criterio utente o un criterio sito, ma non rimuovere il criterio globale. Se si tenta di eliminare tale criterio, Lync Server 2013 lo reimposta automaticamente sui valori predefiniti.


> [!NOTE]
> Se per la distribuzione viene abilitata l'integrazione di Microsoft Exchange, i criteri di Exchange determinano se l'archiviazione è abilitata per gli utenti ospitati in Exchange 2013 con cassette postali impostate per l'archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.



## Per eliminare un criterio utente o sito per l'archiviazione

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Criteri di archiviazione**.

4.  Nell'elenco dei criteri di archiviazione fare clic sul criterio utente o sito che si desidera eliminare, su **Modifica** e quindi su **Elimina**.

5.  Fare clic su **Commit**.

## Rimozione dei criteri di archiviazione mediante i cmdlet di Lync Server Management Shell

I criteri di archiviazione possono anche essere eliminati utilizzando Windows PowerShell e il cmdlet **Remove-CsArchivingPolicy**. Tale cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Rimozione di un criterio di archiviazione specificato

  - Ad esempio,**Remove-CsArchivingPolicy** elimina il criterio con identità site:Redmond. Si noti che, quando viene eliminato un criterio configurato nell'ambito del sito, gli utenti precedentemente gestiti da quel criterio verranno automaticamente controllati dal criterio di archiviazione globale. Il comando seguente rimuove l'archiviazione applicata al sito Redmond:
    
        Remove-CsArchivingPolicy -Identity site:Redmond

## Rimozione di tutti i criteri di archiviazione applicati all'ambito per utente

  - Questo comando rimuove tutti i criteri di archiviazione applicati all'ambito per utente:
    
        Get-CsArchivingPolicy -Filter "tag:*" | Remove-CsArchivingPolicy

## Rimozione di tutti i criteri di archiviazione che disabilitano l'archiviazione interna

  - Questo comando rimuove tutti i criteri di archiviazione in cui è stata disabilitata l'archiviazione interna:
    
        Get-CsArchivingPolicy | Where-Object {$_.ArchiveInternal -eq $False} | Remove-CsArchivingPolicy

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Remove-CsArchivingPolicy](remove-csarchivingpolicy.md).

## Vedere anche

#### Ulteriori risorse

[Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

