---
title: "Lync Server 2013: Usa funzione Chiama c/ telef. abilitato per Lync e LS 2013"
TOCTitle: "Lync Server 2013: Usa funzione Chiama c/ telef. abilitato per Lync e LS 2013"
ms:assetid: 975a1df8-a159-4aa4-a991-5972a535998e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn383570(v=OCS.15)
ms:contentKeyID: 56558963
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso della funzionalità Chiama con un telefono abilitato per Lync e Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-08-09_

La funzionalità Chiama di Lync consente agli utenti di partecipare alla parte audio di una conferenza usando un telefono cellulare, una linea terrestre o un altro dispositivo connesso alla rete PSTN. Quando si tenta di partecipare a una riunione usando Lync, in genere viene visualizzata la finestra di dialogo **Partecipa all'audio della riunione**:

![Cattura di schermata della finestra per partecipare all'audio della riunione tramite Lync](images/Dn383570.e28f17f0-9f17-44ef-b893-f4ef132f47ac(OCS.15).png "Cattura di schermata della finestra per partecipare all'audio della riunione tramite Lync")

Selezionando **Chiama** sarà possibile scegliere un numero di telefono nell'elenco a discesa. Lync Server 2013 effettuerà una chiamata al numero selezionato e quindi si potrà usare quel telefono per partecipare alla parte audio della conferenza.

L'elenco a discesa contiene i numeri di telefono, relativi a telefono cellulare, telefono di casa o altro telefono, inseriti dall'utente nella scheda **Telefoni** della finestra di dialogo **Lync – Opzioni**:

![Cattura di schermata delle opzioni di configurazione di Lync Phone](images/Dn383570.03d2f25d-49e2-47b4-b1e9-b1614fc0c11c(OCS.15).png "Cattura di schermata delle opzioni di configurazione di Lync Phone")

Se non si è inserito alcun numero di telefono nella scheda **Telefoni**, l'elenco a discesa non conterrà numeri. È comunque sempre possibile fare clic su **Nuovo numero** e fare in modo che Lync Server chiami qualsiasi numero telefonico desiderato:

![Cattura di schermata della finestra Chiama per partecipare all'audio della riunione di Lync](images/Dn383570.27f2ac7a-cc1c-465c-b145-202ad03af4f2(OCS.15).png "Cattura di schermata della finestra Chiama per partecipare all'audio della riunione di Lync")

La funzionalità Chiama funziona al meglio quando viene usata secondo le modalità previste, ovvero facendo in modo che Lync Server chiami un numero di telefono PSTN. L'esperienza può risultare meno che ottimale se si chiede a Lync Server di chiamare un endpoint abilitato per Lync, ad esempio un telefono in una sala conferenze. Di seguito è illustrato il problema che potrebbe verificarsi, con due possibili soluzioni.

Per iniziare, ecco cosa accade quando si inserisce nella funzionalità Chiama il numero di un telefono abilitato per Lync. Si supponga che Ken Myer tenti di partecipare a una riunione facendosi chiamare da Lync Server al numero 1-206-555-1219, che corrisponde a un telefono abilitato per Lync Server. Ken verrà inizialmente connesso alla riunione, ma dopo pochi secondi in Lync verrà visualizzato il messaggio **Chiamata non completata o terminata** e sembrerà che Ken sia stato disconnesso:

![Cattura di schermata della finestra della conferenza telefonica Lync](images/Dn383570.c2a81727-8751-41b5-946a-03a1b75b9d95(OCS.15).png "Cattura di schermata della finestra della conferenza telefonica Lync")

Tenere presente, tuttavia, che esiste una discrepanza all'interno della finestra di conversazione di Lync. Ken Myer è l'unico nome elencato sotto l'intestazione **Partecipanti**, ma se si osserva la barra del titolo della finestra, si vedrà che la conferenza contiene un totale di 4 partecipanti.

Analogamente, se si osserva la finestra di conversazione di qualsiasi altro partecipante alla conferenza, Ken Myer non sarà elencato:

![Cattura di schermata della finestra dell'elenco dei partecipanti di Lync](images/Dn383570.fa5990cf-2694-402c-ac06-946aa66b6837(OCS.15).png "Cattura di schermata della finestra dell'elenco dei partecipanti di Lync")

Malgrado tutto questo, Ken Myer sarà in grado di partecipare alla parte audio della conferenza usando il suo telefono abilitato per Lync. La funzionalità Chiama ha effettivamente funzionato, ma l'esperienza utente non è ottimale.

Il problema può essere risolto in almeno due modi. Se si è già effettuato l'accesso a una conferenza nel modo illustrato nell'esempio, in genere è possibile risolvere il problema partecipando anche con una modalità diversa. Ad esempio, se si invia un messaggio istantaneo, si verrà inclusi tra i partecipanti alla conferenza nella finestra di conversazione:

![Cattura di schermata della conversazione di Lync e dell'elenco dei partecipanti](images/Dn383570.9b5ff6d6-9f73-467c-99a7-ef3aa8bd7e7a(OCS.15).png "Cattura di schermata della conversazione di Lync e dell'elenco dei partecipanti")

A questo punto dovrebbe essere possibile partecipare alla riunione nel modo previsto.

In alternativa, è possibile aggirare completamente il problema partecipando alla riunione in modo diverso. Se è necessario che Lync Server chiami un telefono abilitato per Lync Server, iniziare a partecipare alla riunione senza una connessione audio. A questo scopo, selezionare Non partecipare all'audio quando viene visualizzata la finestra di dialogo Partecipa all'audio della riunione:

![Cattura di schermata della finestra per non partecipare all'audio della riunione di Lync](images/Dn383570.280a148d-cce5-4b02-87f9-9f78f17a81c1(OCS.15).png "Cattura di schermata della finestra per non partecipare all'audio della riunione di Lync")

Dopo aver effettuato correttamente la connessione alla riunione, sarà possibile "invitare" anche il telefono abilitato per Lync Server. A questo scopo, posizionare il puntatore del mouse sull'icona Persone e fare clic su **Invita altre persone**:

![Cattura di schermata della finestra per invitare altri partecipanti di Lync](images/Dn383570.69b81b29-d1d2-4ed3-acb6-e37dd18e3d86(OCS.15).png "Cattura di schermata della finestra per invitare altri partecipanti di Lync")

Verrà visualizzata la finestra di dialogo **Invia messaggio istantaneo**. Non tenere conto del titolo della finestra di dialogo, in quanto non si sta realmente inviando un messaggio istantaneo, e digitare il numero del telefono abilitato per Lync:

![Cattura di schermata della finestra di dialogo Invia un messaggio istantaneo](images/Dn383570.cd67a3f0-06d8-41ba-a808-c067f64bec9f(OCS.15).png "Cattura di schermata della finestra di dialogo Invia un messaggio istantaneo")

Dopo aver fatto clic su **OK**, Lync Server chiamerà il numero immesso nella finestra di dialogo. Una volta effettuata la connessione, si disporrà di funzionalità audio complete tramite il telefono abilitato per Lync e sarà possibile vedere l'intero elenco conferenze e interagire con esso.

