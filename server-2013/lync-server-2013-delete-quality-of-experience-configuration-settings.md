---
title: Eliminare le impostazioni di configurazione per la qualità percepita dagli utenti
TOCTitle: Eliminare le impostazioni di configurazione per la qualità percepita dagli utenti
ms:assetid: fd0c4c2f-3bfb-42cb-9b6a-f0f8d5aa9e81
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182613(v=OCS.15)
ms:contentKeyID: 49302570
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare le impostazioni di configurazione per la qualità percepita dagli utenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le metriche QoE (qualità percepita dagli utenti) registrano la qualità delle chiamate audio e video effettuate nell'organizzazione, includendo informazioni quali il numero di pacchetti di rete persi, i rumori di fondo e la quantità di "instabilità" (differenze nel ritardo dei pacchetti). Queste metriche vengono archiviate in un database separatamente rispetto ad altri dati, ad esempio la registrazione dettagli chiamata, in modo che sia possibile abilitare e disabilitare il servizio QoE in maniera indipendente rispetto ad altre registrazioni di dati.

Quando si installa Microsoft Lync Server 2013, viene creata automaticamente un'unica raccolta globale di impostazioni di configurazione QoE. Gli amministratori hanno inoltre la possibilità di creare raccolte di impostazioni personalizzate da applicare ai siti individuali. Per impostazione predefinita, le impostazioni configurate in ambito sito hanno la precedenza sulle impostazioni configurate in ambito globale. Se si eliminano le impostazioni in ambito sito, le metriche QoE verranno gestite nel sito utilizzando le impostazioni globali.

Si noti che è inoltre possibile "eliminare" le impostazioni globali. Tuttavia, le impostazioni non verranno realmente rimosse: per tutte le proprietà della raccolta verranno ripristinati i valori predefiniti. Ad esempio, per impostazione predefinita, l'eliminazione è abilitata in una raccolta di impostazioni di configurazione QoE. Si supponga di modificare la raccolta globale e disabilitare l'eliminazione. Se successivamente si eliminano le impostazioni globali, per tutte le proprietà verranno ripristinati i valori predefiniti. In tal caso, l'eliminazione verrà di nuovo abilitata.

È possibile rimuovere le impostazioni di configurazione QoE utilizzando il Pannello di controllo di Lync Server o il cmdlet [Remove-CsQoEConfiguration](remove-csqoeconfiguration.md).

## Per eliminare le impostazioni di configurazione QoE utilizzando il Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Monitoraggio e archiviazione** e quindi su **Dati QoE**.

4.  Nella pagina **Dati QoE** fare clic sul criterio desiderato, selezionare **Modifica** e quindi fare clic su **Elimina**.

5.  Fare clic su **OK**.

## Per rimuovere le impostazioni di configurazione QoE utilizzando i cmdlet Lync Server Management Shell

È inoltre possibile eliminare le impostazioni di configurazione QoE utilizzando Lync Server Management Shell e il cmdlet **Remove-CsQoEConfiguration**. È possibile eseguire il cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere una raccolta specificata di impostazioni di configurazione QoE

  - Questo comando rimuove le impostazioni di configurazione QoE applicate al sito Redmond.
    
        Remove-CsQoEConfiguration -Identity "site:Redmond"

## Per rimuovere tutte le impostazioni di configurazione QoE applicate all'ambito sito

  - Questo comando rimuove tutte le impostazioni di configurazione QoE applicate all'ambito sito.
    
        Get-CsQoEConfiguration -Filter "site:*" | Remove-CsQoEConfiguration

## Per rimuovere tutte le impostazioni di configurazione QoE dove il monitoraggio QoE è disabilitato

  - Questo comando rimuove tutte le impostazioni di configurazione QoE dove il monitoraggio QoE è stato disabilitato
    
        Get-CsQoEConfiguration | Where-Object {$_.EnableQoE -eq $False} | Remove-CsQoEConfiguration

Per informazioni dettagliate, vedere [Remove-CsQoEConfiguration](remove-csqoeconfiguration.md).

