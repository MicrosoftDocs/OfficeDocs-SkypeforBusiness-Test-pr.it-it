---
title: "Lync Server 2013: Installare l'archivio di configurazione locale"
TOCTitle: Installare l'archivio di configurazione locale
ms:assetid: b563030d-d338-411f-9611-28d5eb4b3238
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412874(v=OCS.15)
ms:contentKeyID: 49301732
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare l'archivio di configurazione locale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-27_

Prima di eseguire i passaggi seguenti, assicurarsi di avere eseguito l'accesso al server con un account utente di dominio sia amministratore locale che membro del gruppo RTCUniversalReadOnlyAdmins.

Per poter eseguire qualsiasi operazione con la Distribuzione guidata di Lync Server, è necessario che l'archivio di configurazione locale esista in un server. Tale archivio è una copia di sola lettura dell'archivio di gestione centrale, che viene creato dopo l'installazione locale di SQL Server Express. L'archivio di gestione centrale viene aggiunto al database di SQL Server esistente installato nel server Standard Edition o al database basato su SQL Server Express.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se non è stata eseguita in precedenza l'installazione di Lync Server 2013 in questo server, verrà richiesto di specificare l'unità e il percorso per l'installazione di Lync Server 2013. Ciò consentirà di eseguire l'installazione in un'unità diversa da quella di sistema, se richiesto dell'organizzazione oppure nel caso esistano problemi di spazio. È possibile cambiare semplicemente il percorso di installazione dei file di Lync Server nella finestra di dialogo del programma di installazione, scegliendo una diversa unità disponibile. Se si installano i file di installazione in questo percorso, incluso il file OCSCore.msi, anche la parte restante dei file di Lync Server 2013 verrà distribuita in tale unità.</td>
</tr>
</tbody>
</table>


## Per installare l'archivio di configurazione locale

1.  Dal supporto di installazione passare a \\setup\\amd64\\Setup.exe e quindi fare clic su **OK**.

2.  Se viene richiesto di installare Microsoft Visual C++ 2012 Redistributable, fare clic su **Sì**.

3.  Nella pagina **Percorso di installazione di Lync Server 2013** fare clic su **OK** .

4.  Nella pagina **Contratto di licenza con l'utente finale** esaminare le condizioni di licenza, selezionare **Accetto i termini del Contratto di licenza** e quindi fare clic su **OK** per continuare.

5.  Nella pagina Distribuzione guidata fare clic su **Installa o aggiorna il sistema Lync Server** .

6.  Nella pagina **Lync Server 2013**, accanto a **Passaggio 1: Installazione dell'archivio di configurazione locale**, fare clic su **Esegui**.

7.  Nella pagina **Installazione dell'archivio di configurazione locale** verificare che l'opzione **Recupera direttamente dall'archivio di gestione centrale** sia selezionata e quindi fare clic su **Avanti** .

8.  Al termine dell'installazione con configurazione del server locale, fare clic su **Fine**.

