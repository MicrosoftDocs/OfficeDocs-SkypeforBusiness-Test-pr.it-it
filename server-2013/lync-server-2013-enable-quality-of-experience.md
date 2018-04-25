---
title: Abilitare la qualità percepita dagli utenti (QoE)
TOCTitle: Abilitare la qualità percepita dagli utenti (QoE)
ms:assetid: c8bb3c67-b324-4d94-8158-00c792c7ac42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182583(v=OCS.15)
ms:contentKeyID: 49301966
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare la qualità percepita dagli utenti (QoE)

 

_**Ultima modifica dell'argomento:** 2013-02-23_

La qualità percepita dagli utenti (QoE, Quality of Experience) registra dati numerici che indicano la qualità multimediale e le informazioni sui partecipanti, i nomi di dispositivi, i driver, gli indirizzi IP e i tipi di endpoint coinvolti nelle chiamate e nelle sessioni. Per informazioni dettagliate, vedere [Pianificazione del monitoraggio in Lync Server 2013](lync-server-2013-planning-for-monitoring.md) nella documentazione relativa alla pianificazione.

Utilizzare la procedura che segue per abilitare QoE per l'intera organizzazione o per ogni suo sito.


> [!NOTE]
> Per abilitare QoE, è innanzitutto necessario configurare il monitoraggio e un database back-end Monitoring Server. Per informazioni dettagliate, vedere <A href="lync-server-2013-deploying-monitoring.md">Distribuzione del monitoraggio in Lync Server 2013</A>.



## Per abilitare QoE tramite il Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Monitoraggio e archiviazione** e quindi su **Dati QoE**.

4.  Nella pagina **Dati QoE** fare clic sulla raccolta appropriata nella tabella, su **Azione** e quindi su **Abilita QoE**.

## Abilitazione di QoE tramite i cmdlet di Windows PowerShell

È possibile abilitare QoE utilizzando Windows PowerShell e il cmdlet **Set-CsQoEConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare QoE per una singola posizione

  - Per abilitare QoE, impostare il parametro EnableQoE su True ($True).
    
        Set-CsQoEConfiguration -Identity "site:Redmond" -EnableQoE $True

## Per disabilitare QoE per una singola posizione

  - Per disabilitare QoE, impostare il parametro EnableQoE su False ($False). Questa operazione non comporta la disinstallazione del monitoraggio. Determina solo la sospensione della raccolta e dell'archiviazione di dati QoE.
    
        Set-CsQoEConfiguration -Identity "site:Redmond" -EnableQoE $False

## Per utilizzare un singolo comando per abilitare QoE in più posizioni

  - Il comando seguente abilita QoE per tutte le impostazioni di configurazione QoE attualmente in uso nell'organizzazione.
    
        Get-CsQoEConfiguration | Set-CsQoEConfiguration "site:Redmond" -EnableQoE $True

Per informazioni dettagliate, vedere [Set-CsQoEConfiguration](set-csqoeconfiguration.md).

## Vedere anche

#### Ulteriori risorse

[Pianificazione del monitoraggio in Lync Server 2013](lync-server-2013-planning-for-monitoring.md)  
[Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md)

