---
title: Configurazione dell'archivio dei contatti personali
TOCTitle: Configurazione dell'archivio dei contatti personali
ms:assetid: ec69a6cb-07f2-4057-9544-55035f83eeae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721922(v=OCS.15)
ms:contentKeyID: 49887809
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'archivio dei contatti personali

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Se si integra Microsoft Lync Server 2013 e Microsoft Exchange Server 2013, è consigliabile configurare l'archivio contatti personale in tutti i computer client in cui è in esecuzione Microsoft Lync 2010. In particolare è necessario configurare Lync in modo che utilizzi Exchange come archivio contatti personale e, allo stesso tempo, verificare che gli utenti non possano ignorare tale decisione. A tale scopo è possibile creare e configurare un valore del Registro di sistema in ogni computer client.

Si noti che questa operazione non è necessaria nei computer che eseguono Lync 2013.

Per configurare questo valore in un singolo computer, eseguire la procedura seguente:

1.  Nel computer client fare clic sul pulsante **Start** e quindi su **Esegui**.

2.  Nella finestra di dialogo **Esegui** digitare regedit e quindi premere INVIO.

3.  In Editor del Registro di sistema espandere **HKEY\_LOCAL\_MACHINE**, **Software**, **Policies**, **Microsoft** e quindi **Communicator**.

4.  Fare clic con il pulsante destro del mouse su **Communicator**, scegliere **Nuovo** e quindi fare clic su **Valore DWORD (32 bit)**.

5.  Dopo aver creato il nuovo valore, digitare **PersonalContactStoreOverride** e quindi premere INVIO per rinominare il valore.

6.  Verificare che il valore di PersonalContactStoreOverride sia impostato su 0 e quindi chiudere Editor del Registro di sistema.

Se si desidera eseguire le stesse modifiche in più computer è possibile creare un oggetto Criteri di gruppo personalizzato. Per informazioni dettagliate, vedere la documentazione relativa ai Criteri di gruppo all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268543\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268543%26clcid=0x410).

