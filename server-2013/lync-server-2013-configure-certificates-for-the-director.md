---
title: 'Lync Server 2013: Configurare i certificati per il server Director'
TOCTitle: Configurare i certificati per il server Director
ms:assetid: 22988186-15ae-43b1-92f4-0adb3b75a7fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398296(v=OCS.15)
ms:contentKeyID: 49299926
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i certificati per il server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

> [!IMPORTANT]  
> Quando si esegue la Configurazione guidata certificati, verificare di aver effettuato l'accesso con un account membro di un gruppo che dispone delle autorizzazioni appropriate per il tipo di modello di certificato da utilizzare. Per impostazione predefinita, per una richiesta di certificato di Lync Server 2013 viene utilizzato il modello di certificato WebServer. Se per la richiesta di un certificato con questo modello si utilizza un account membro del gruppo RTCUniversalServerAdmins, verificare che al gruppo siano state assegnate le autorizzazioni di registrazione necessarie per l'utilizzo del modello.

Ogni director richiede un certificato predefinito, un certificato Web interno e un certificato Web esterno. Per informazioni dettagliate sui requisiti dei certificati per i director, vedere [Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md) nella documentazione relativa alla pianificazione.

Utilizzare la procedura seguente per configurare i certificati per i Director. Ripetere la procedura per ogni Director. Nei passaggi di questa procedura viene descritto come configurare un certificato da un'autorità di certificazione (CA) radice globale (enterprise) interna distribuita dall'organizzazione e con l'elaborazione delle richieste offline. Per informazioni dettagliate su come ottenere certificati da una CA esterna, rivolgersi al team di supporto.

## Per configurare certificati per il Director o il pool di server Director

1.  Nella Distribuzione guidata di Lync Server, accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** , fare clic su **Esegui** .

2.  Nella pagina **Configurazione guidata certificati** fare clic su **Richiedi** .

3.  Nella pagina **Richiesta di certificato** fare clic su **Avanti** .

4.  Nella pagina **Richiesta posticipata o immediata** accettare l'opzione predefinita **Invia immediatamente la richiesta a un'autorità di certificazione online** e quindi fare clic su **Avanti** .

5.  Nella pagina **Scegli Autorità di certificazione (CA)** fare clic sull'autorità di certificazione di Windows interna che si desidera utilizzare e quindi fare clic su **Avanti** .

6.  Nella pagina **Account autorità di certificazione** specificare credenziali alternative da utilizzare se l'account con cui è stato eseguito l'accesso non dispone dell'autorità sufficiente per richiedere il certificato e quindi fare clic su **Avanti** .

7.  Nella pagina **Specifica modello di certificato alternativo** fare clic su **Avanti** .

8.  Nella pagina **Impostazioni nome e sicurezza** è possibile specificare un nome in **Nome descrittivo** , accettare la lunghezza di chiave di 2048 bit e quindi fare clic su **Avanti** .

9.  Nella pagina **Informazioni sull'organizzazione** specificare facoltativamente le informazioni sull'organizzazione e quindi fare clic su **Avanti** .

10. Nella pagina **Dati geografici** specificare facoltativamente i dati geografici e quindi fare clic su **Avanti** .

11. Nella pagina **Nome soggetto / Nomi soggetto alternativi** fare clic su **Avanti** .
    

    > [!NOTE]
    > Nell'elenco dei nomi alternativi del soggetto dovrebbero essere contenuti il nome del computer in cui si desidera installare il Director (se singolo) o il nome del pool di server Director e i nomi degli URL semplici configurati per l'organizzazione.



12. Nella pagina **Impostazione del dominio SIP su nomi soggetto alternativi (SAN)** selezionare **Domini SIP configurati** per tutti i domini che devono essere gestiti dal Director e quindi fare clic su **Avanti** .

13. Nella pagina **Configura nomi soggetto alternativi aggiuntivi** aggiungere altri eventuali nomi alternativi del soggetto necessari e quindi fare clic su **Avanti** .

14. Nella pagina **Riepilogo richiesta certificato** fare clic su **Avanti** .

15. Nella pagina **Esecuzione comandi in corso** fare clic su **Avanti** al termine dell'esecuzione dei comandi.

16. Nella pagina **Stato richiesta di certificato online** fare clic su **Fine** .

17. Nella pagina **Assegnazione certificato** fare clic su **Avanti** .
    

    > [!NOTE]
    > Se si desidera visualizzare il certificato, fare doppio clic su di esso nell'elenco.



18. Nella pagina **Riepilogo assegnazione certificato** fare clic su **Avanti** .

19. Nella pagina **Esecuzione comandi in corso** fare clic su **Fine** al termine dell'esecuzione dei comandi.

20. Nella pagina **Configurazione guidata certificati** fare clic su **Chiudi** .

