---
title: Eliminare una raccolta esistente di impostazioni di configurazione di Lync Phone Edition
TOCTitle: Eliminare una raccolta esistente di impostazioni di configurazione di Lync Phone Edition
ms:assetid: 1bfc427d-4dcd-4199-b25f-8d5cfec2164f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687984(v=OCS.15)
ms:contentKeyID: 49887464
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta esistente di impostazioni di configurazione di Lync Phone Edition

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Se non si desidera più utilizzare una raccolta di impostazioni per i dispositivi che eseguono Lync Phone Edition, eliminarla. Se si elimina una raccolta per un sito, le impostazioni globali saranno applicabili ai telefoni in quel sito. Non è possibile eliminare la raccolta globale.


> [!NOTE]
> Invece di eliminare una raccolta, è possibile modificare alcune delle impostazioni. Per informazioni dettagliate su come procedere, vedere <A href="lync-server-2013-create-or-modify-a-collection-of-lync-phone-edition-configuration-settings.md">Creare o modificare una raccolta di impostazioni di configurazione di Lync Phone Edition</A>.



## Per eliminare una raccolta di impostazioni di configurazione di Lync Phone Edition

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Client**, quindi fare clic sul pulsante di navigazione **Configurazione dispositivo**.

4.  Nella pagina **Configurazione dispositivo** fare clic sulla raccolta che si desidera eliminare, quindi scegliere il menu **Modifica** e quindi **Elimina**.
    

    > [!NOTE]
    > Se si elimina la raccolta globale, vengono ripristinate le impostazioni predefinite. La raccolta viene mantenuta.



5.  Nella finestra di conferma fare clic su **OK**.

## Per rimuovere le impostazioni di configurazione di Lync Phone Edition utilizzando i cmdlet della Lync Server Management Shell

È possibile eliminare le impostazioni di configurazione di Lync Phone Edition utilizzando l'Windows PowerShell e il cmdlet **Remove-CsUCConfiguration**. È possibile eseguire questo cmdlet dalla Lync Server 2013 Management Shell o da una sessione remota dell'Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere una raccolta specificata di impostazioni di configurazione di Lync Phone Edition

  - Questo comando elimina le impostazioni di configurazione dei telefoni UC applicate al sito di Redmond:
    
        Remove-CsUCPhoneConfiguration -Identity "site:Redmond"

## Per rimuovere tutte le impostazioni di configurazione di Lync Phone Edition applicate all'ambito del sito

  - Questo comando rimuove tutte le impostazioni di configurazione dei telefoni UC applicate all'ambito del servizio:
    
        Get-CsUCPhoneConfiguration -Filter "site:*" | Remove-CsUCPhoneConfiguration

## Per rimuovere tutte le impostazioni di configurazione di Lync Phone Edition in cui il blocco del telefono è disabilitato

  - Questo comando elimina le raccolte di impostazioni di configurazione dei telefoni UC in cui il blocco del telefono è stato disabilitato:
    
        Get-CsUCPhoneConfiguration | Where-Object {$_.EnforcePhoneLock -eq $False} | Remove-CsUCPhoneConfiguration

Per informazioni dettagliate, vedere [Remove-CsUCPhoneConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsUCPhoneConfiguration).

