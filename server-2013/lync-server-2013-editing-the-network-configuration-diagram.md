---
title: Modifica del diagramma di configurazione della rete in Lync Server 2013
TOCTitle: Modifica del diagramma di configurazione della rete in Lync Server 2013
ms:assetid: 47425ab1-5645-4d6f-b202-64bcce43e3ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558643(v=OCS.15)
ms:contentKeyID: 52062143
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica del diagramma di configurazione della rete in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

La maggior parte del lavoro che un progettista deve svolgere in Lync Server 2013, Strumento di pianificazione è rappresentata dalla definizione delle voci relative agli indirizzi IP e ai nomi di dominio completi (FQDN) per le voci nel diagramma di rete. Le informazioni immesse in questa pagina vengono riportate nei rapporti e in altre informazioni contenute nello Strumento di pianificazione.

![Diagramma di rete dello strumento di pianificazione](images/Gg558643.eeabee2d-698c-4b79-baa5-caa4cfb7edb3(OCS.15).jpg "Diagramma di rete dello strumento di pianificazione")

Lo Strumento di pianificazione crea un diagramma di rete con testo predefinito per gli indirizzi IP e gli FQDN.

Per modificare il diagramma di rete e i valori di input:

1.  Scegliere una sezione della rete per iniziare. Ad esempio, fare doppio clic sul testo **access1.contoso.com**. Nella finestra di dialogo aperta digitare il nome di dominio completo effettivo per il server access1.contoso.com e l'indirizzo IP effettivo, sostituendo l'indirizzo 131.107.155.3.

2.  Fare clic su **OK** per salvare le immissioni.

3.  Continuare a modificare gli indirizzi IP e gli FQDN, fornendo indirizzi IP virtuali per i dispositivi di bilanciamento del carico hardware o le voci relative ai server per il bilanciamento del carico DNS (Domain Name System) per i server dei pool.

Nello Strumento di pianificazione è disponibile una funzionalità utile che consente di assegnare in modo incrementale un intervallo di indirizzi IP e nomi host di server anziché richiedere al progettista di modificare ogni server separato di un pool. Ad esempio:

1.  Fare doppio clic sui Front End Server in pool. Quando viene visualizzata la finestra di dialogo, selezionare **Utilizzare questi IP e l'FQDN come punti di partenza per tutti i server equivalenti nel cluster?**.

2.  Ad esempio, il valore di partenza per il primo server è fe0101.contoso.com con indirizzo IP 192.168.21.122.

3.  Digitare **fe0.contoso.com** in **FQDN di Front End Server** e **192.168.21.131** in **Indirizzo IP di Front End Server**, quindi fare clic su **OK**.

4.  La funzionalità di incremento automatico aggiorna tutti i server del pool impostando server compresi tra fe01 e fe06 e tutti gli indirizzi IP impostando indirizzi compresi tra 192.168.21.131 e 136.

Dopo aver completato tutte le modifiche, salvare la topologia eseguendo le operazioni seguenti:

Per salvare la progettazione dello Strumento di pianificazione, scegliere **Salva topologia** o **Salva topologia con nome** dal menu **File**. Se viene visualizzata una finestra di dialogo **Salva file dello Strumento di pianificazione con nome**, digitare un nome per il file in **Nome file** e quindi fare clic su **Salva**.

## Vedere anche

#### Concetti

[Modifica della progettazione in Lync Server 2013](lync-server-2013-editing-the-design.md)

