---
title: 'Lync Server 2013: Riattivare il server dopo la chiusura delle porte in IIS da parte della Configurazione guidata impostazioni di sicurezza'
TOCTitle: Riattivare il server dopo la chiusura delle porte in IIS da parte della Configurazione guidata impostazioni di sicurezza
ms:assetid: cb8e17cf-f8c1-4099-b63b-c242d656c26a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398851(v=OCS.15)
ms:contentKeyID: 49301977
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riattivare il server dopo la chiusura delle porte in IIS da parte della Configurazione guidata impostazioni di sicurezza

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Alcuni ruoli di Lync Server 2013 eseguono i servizi Web sulla porta 4443 di Internet Information Services (IIS). L'esecuzione della Distribuzione guidata di Lync Server, di Bootstrapper.exe o del cmdlet **Enable-CsComputer** consente di creare un'eccezione nel firewall e di aprire la porta. Se successivamente si esegue la Configurazione guidata impostazioni di sicurezza di Windows Server 2008 R2 o altri script di protezione avanzata, la porta 4443 verrà bloccata e i client esterni non saranno in grado di contattare i servizi Web. Per riaprire la porta, è possibile modificare l'eccezione del firewall direttamente oppure riattivare il server.

## Per riattivare il server mediante la Distribuzione guidata

1.  Nella pagina Distribuzione guidata di Lync Server fare clic su **Esegui** accanto a **Passaggio 2: Installazione o rimozione componenti di Lync Server** .

2.  Nella pagina **Installazione componenti di Lync Server** fare clic su **Avanti** .

3.  Nella pagina **Esecuzione comandi in corso** , quando lo stato dell'attività risulta completato, fare clic su **Fine** .
    

    > [!NOTE]
    > È anche possibile utilizzare bootstrapper.exe o <STRONG>Enable-CsComputer</STRONG> per riattivare il server.


