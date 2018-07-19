---
title: Esportazione dei dati archiviati da Lync Server 2013
TOCTitle: Esportazione dei dati archiviati da Lync Server 2013
ms:assetid: 09450d54-769b-4741-924b-e390664d506f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204657(v=OCS.15)
ms:contentKeyID: 49299614
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esportazione dei dati archiviati da Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

I dati archiviati nei database di archiviazione non sono in un formato leggibile o disponibile per la ricerca, ma è possibile utilizzare il cmdlet Export-CsArchivingData per estrarre record dal database e salvarli come file EML (Electronic Mail) di Outlook. Per informazioni dettagliate sull'esportazione di dati archiviati, vedere [Export-CsArchivingData](https://docs.microsoft.com/en-us/powershell/module/skype/Export-CsArchivingData) nella documentazione relativa alle operazioni.

Se si abilita l'integrazione Microsoft Exchange, i dati vengono archiviati negli archivi di Exchange 2013. I dati archiviati in Exchange 2013 sono individuabili e disponibili per la ricerca. Per informazioni dettagliate sul supporto delle comunicazioni integrate per Exchange 2013 e Lync Server 2013, vedere [Supporto per l'integrazione di Exchange Server e SharePoint in Lync Server 2013](lync-server-2013-exchange-and-sharepoint-integration-support.md) nella documentazione relativa alla supportabilità. Per informazioni dettagliate sull'accesso ai dati archiviati in Exchange, vedere la documentazione di Exchange 2013.

## Esportazione dei dati di archiviazione mediante cmdlet di Lync Server Management Shell

I dati di archiviazione possono essere esportati utilizzando il cmdlet Export-CSArchivingData, che può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

**Esportazione dei dati di archiviazione**

  - Questo comando consente di esportare tutti i dati di archiviazione scritti nel database archiviazione atl-sql-001.litwareinc.com dal 1 giugno 2012. Il file di output risultante verrà archiviato nella cartella C:\\ArchivingExports.
    
        Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports"

**Esportazione dei dati di archiviazione per un singolo utente**

  - Il comando seguente consente di esportare tutti i dati di archiviazione per un singolo utente, in questo caso kenmyer@litwareinc.com. L'operazione si esegue includendo il parametro UserUri seguito dall'indirizzo SIP dell'utente. Ad esempio:
    
        Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports" -UserUri "sip:kenmyer@litwareinc.com"

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Export-CsArchivingData](https://docs.microsoft.com/en-us/powershell/module/skype/Export-CsArchivingData).

## Vedere anche

#### Concetti

[Supporto per l'integrazione di Exchange Server e SharePoint in Lync Server 2013](lync-server-2013-exchange-and-sharepoint-integration-support.md)  

#### Ulteriori risorse

[Export-CsArchivingData](https://docs.microsoft.com/en-us/powershell/module/skype/Export-CsArchivingData)  
[Gestione dell'archiviazione in Lync Server 2013](lync-server-2013-managing-archiving.md)

