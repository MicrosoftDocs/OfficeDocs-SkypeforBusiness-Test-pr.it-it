---
title: "Sposta server Mediation Server in server Mediation Server autonomo (facolt.)"
TOCTitle: "Sposta server Mediation Server in server Mediation Server autonomo (facolt.)"
ms:assetid: 7c3c2fb4-4ff2-47b1-aab3-0aa91472eadb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205026(v=OCS.15)
ms:contentKeyID: 49301086
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Effettuare la transizione di un server Mediation Server collocato in un server Mediation Server autonomo (facoltativo)

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Eseguire la procedura seguente per la transizione del Mediation Server, collocato nel server Standard Edition o nel pool Front End, in un Mediation Server autonomo per una distribuzione a sito singolo.

## Per effettuare la transizione di un Mediation Server collocato in un server Mediation Server autonomo (facoltativo)

1.  Apertura di una topologia esistente da Generatore di topologie

2.  Nel riquadro sinistro passare a **Pool Mediation Server** .

3.  Fare clic con il pulsante destro del mouse su **Pool Mediation Server** e quindi scegliere **Nuovo Mediation Server** .

4.  Nella pagina **Definisci nuovo pool Mediation Server** immettere il nome di dominio completo del nuovo pool Mediation Server, specificare se sarà un pool a server singolo o a più server e quindi fare clic su **Avanti** .

5.  Selezionare il pool dell'hop Front End server successivo al quale il nuovo Mediation Server instraderà le chiamate in arrivo e quindi fare clic su **Avanti** .

6.  Selezionare il pool di server perimetrali che deve essere utilizzato dal Mediation Server e quindi fare clic su **Avanti** .

7.  Nella pagina **Specificare i gateway PSTN** associare il gateway PSTN precedente al Mediation Server. Selezionare il gateway e quindi fare clic su **Aggiungi** .

8.  Fare clic su **Fine** per chiudere la procedura guidata **Definisci nuovo pool Mediation Server** .

9.  In **Generatore di topologie** , selezionare il nodo di primo livello **Lync Server 2013**.

10. Nel riquadro **Azioni** selezionare **Pubblica topologia** e quindi completare la procedura guidata.

11. Eseguire la procedura in [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md) nella documentazione relativa alla distribuzione per installare i file nel nuovo Mediation Server, configurare i certificati e avviare i servizi.

12. Dopo l'installazione dei file nel Mediation Server, tornare al Generatore di topologie e nel riquadro sinistro passare al pool.

13. Fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

14. In **Mediation Server** deselezionare la casella di controllo **Mediation Server nella stessa posizione abilitato** e quindi fare clic su **OK** .

15. In **Generatore di topologie** , selezionare il nodo di primo livello **Lync Server 2013**.

16. Scegliere **Pubblica topologia** dal menu **Azione** e quindi completare la procedura guidata.

