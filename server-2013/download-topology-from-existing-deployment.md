---
title: Scarica topologia dalla distribuzione esistente
TOCTitle: Scarica topologia dalla distribuzione esistente
ms:assetid: e39065a2-d4b0-4f27-8c49-f56be78fa55b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721913(v=OCS.15)
ms:contentKeyID: 49887790
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scarica topologia dalla distribuzione esistente

 

_**Ultima modifica dell'argomento:** 2012-09-29_

Per la creazione di un pool Lync Server 2013 si utilizzerà l'Archivio di gestione centrale associato a Lync Server 2010. All'avvio di Generatore di topologie per il primo utilizzo e le sessioni di modifica successive viene richiesto di specificare la posizione in cui deve essere caricato il documento della configurazione corrente. Dato che è già stata definita una topologia di Lync Server 2010 ed è stato stabilito l'Archivio di gestione centrale, è consigliabile scegliere di scaricare una topologia da una distribuzione esistente. Generatore di topologie leggerà il database e recupererà la definizione corrente.

**Per scaricare una topologia da una distribuzione esistente**

1.  Aprire la **Distribuzione guidata di Lync Server** .

2.  Nella pagina **Lync Server 2013 – Distribuzione guidata** fare clic su **Installa Strumenti di amministrazione**.

3.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

4.  Selezionare **Scarica topologia dalla distribuzione esistente**.
    
    ![Impostazioni del Generatore di topologie per la Distribuzione guidata](images/JJ721913.d5b39fd9-3c13-422e-a06c-25d2568fe781(OCS.15).jpg "Impostazioni del Generatore di topologie per la Distribuzione guidata")

5.  Scegliere un nome di file e salvare la topologia con il tipo di file predefinito con estensione tbxml.

6.  Espandere il nodo Lync Server, come illustrato, per visualizzare i vari ruoli server nella distribuzione.
    
    ![Proprietà generali del ruolo server del Generatore di topologie](images/JJ721913.af99ead3-676b-47fd-8369-5a5f9717383f(OCS.15).jpg "Proprietà generali del ruolo server del Generatore di topologie")

