---
title: "Lync Server 2013: Elimina impostazioni di configurazione di trunk SIP"
TOCTitle: "Lync Server 2013: Elimina impostazioni di configurazione di trunk SIP"
ms:assetid: 3b25f14d-884b-42dd-a866-460d276d3e43
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688024(v=OCS.15)
ms:contentKeyID: 49887522
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta esistente di impostazioni di configurazione di trunk SIP

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Le impostazioni di configurazione del trunk SIP definiscono la relazione e le funzionalità tra un Mediation Server e il gateway PSTN (Public Switched Telephone Network), un IP-PBX (IP-Public Branch Exchange), o un SBC (Session Border Controller) nel provider di servizi. Queste impostazioni consentono di specificare:

  - Se si deve abilitare il bypass multimediale sui trunk.

  - Le condizioni che devono essere soddisfatte per l'invio di pacchetti RTPC (Real-Time Transport Control Protocol).

  - Se è richiesta la crittografia SRTP (Secure Real-Time Protocol) per ciascun trunk.

Quando si installa Microsoft Lync Server 2013, viene creata automaticamente una raccolta globale di impostazioni di configurazione dei trunk SIP. Questa raccolta non può essere eliminata, tuttavia è possibile utilizzare il Pannello di controllo di Lync Server o il cmdlet [Remove-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsTrunkConfiguration) per ripristinare i valori predefiniti delle proprietà della raccolta globale. Se ad esempio la proprietà Enable3pccRefer è stata impostata su True, quando si ripristinano i valori predefiniti, la proprietà Enable3pccRefer viene reimpostata su False.

Gli amministratori possono inoltre creare impostazioni di configurazione personalizzate per i trunk con ambito sito o servizio (per un gateway PSTN singolo) che possono essere rimosse. Quando si rimuovono le impostazioni personalizzate, tenere presente che:

  - Se si rimuovono le impostazioni con ambito servizio, il trunk SIP gestito da tali impostazioni verrà gestito dalle impostazioni applicate al rispettivo sito, se esistenti. In caso contrario, i trunk verranno gestiti dalla raccolta globale di impostazioni di configurazione dei trunk.

  - Se si rimuovono le impostazioni con ambito sito, i trunk SIP gestiti da tali impostazioni verranno gestiti dalla raccolta globale di impostazioni di configurazione dei trunk.

## Rimozione delle impostazioni di configurazione dei trunk mediante il Pannello di controllo di Lync Server

1.  Nel Pannello di controllo di Lync Server fare clic su **Routing vocale**, quindi su **Configurazione trunk**.

2.  Nella scheda **Configurazione trunk** selezionare la raccolta di impostazioni di configurazione dei trunk SIP da eliminare, fare clic su **Modifica**, quindi su **Elimina**. Per eliminare più raccolte con una sola operazione, fare clic sulla prima raccolta da eliminare, quindi sulle altre raccolte tenendo premuto il tasto CTRL.

3.  La proprietà **Stato** per la raccolta verrà aggiornata a **Commit non eseguito**. Per eseguire il commit delle modifiche e per eliminare la raccolta, fare clic su **Commit**, quindi su **Salva tutto**.

4.  Nella finestra di dialogo **Impostazioni di configurazione vocale di cui non è stato eseguito il commit** fare clic su **OK**.

5.  Nella finestra di dialogo **Pannello di controllo di Microsoft Lync Server 2013** fare clic su **OK**.

6.  Se si decide di non eliminare più la raccolta, fare clic su **Commit**, quindi su **Annulla tutte le modifiche di cui non è stato eseguito il commit**. Quando viene visualizzata la finestra di dialogo **Pannello di controllo di Microsoft Lync Server 2013**, fare clic su **OK**.

## Rimozione delle impostazioni di configurazione dei trunk mediante i cmdlet Lync Server PowerShell

È possibile eliminare le impostazioni di configurazione dei trunk anche usando Windows PowerShell e il cmdlet Remove-CsTrunkConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Rimozione di una raccolta di impostazioni specifica

  - Il comando seguente rimuove le impostazioni di configurazione dei trunk applicate al sito di Redmond:
    
        Remove-CsTrunkConfiguration -Identity site:Redmond

## Rimozione di tutte le raccolte applicate all'ambito sito

  - Questo comando rimuove tutte le impostazioni di configurazione dei trunk applicate all'ambito servizio:
    
        Get-CsTrunkConfiguration -Filter "service:*" | Remove-CsTrunkConfiguration

## Rimozione di tutte le raccolte in cui è abilitato il bypass multimediale

  - Il comando seguente rimuove tutte le impostazioni di configurazione dei trunk in cui è stato abilitato il bypass multimediale:
    
        Get-CsTrunkConfiguration | Where-Object {$_.EnableBypass -eq $True} | Remove-CsTrunkConfiguration

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Remove-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsTrunkConfiguration).

