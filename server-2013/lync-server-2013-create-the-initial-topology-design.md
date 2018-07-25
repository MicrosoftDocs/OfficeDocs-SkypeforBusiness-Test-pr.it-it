---
title: 'Lync Server 2013: Creare la progettazione della topologia iniziale'
TOCTitle: Creare la progettazione della topologia iniziale
ms:assetid: f3131153-de14-41be-b1e6-7d4bb0191af1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615047(v=OCS.15)
ms:contentKeyID: 52062473
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare la progettazione della topologia iniziale per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Dopo aver completato l'installazione di Lync Server 2013, Strumento di pianificazione, è possibile avviare lo Strumento di pianificazione e iniziare la progettazione dell'infrastruttura di Lync Server 2013 proposta.


> [!NOTE]
> Lo Strumento di pianificazione è una procedura guidata destinata a fornire le informazioni dettagliate necessarie per il processo decisionale per la progettazione di siti e topologia. Questo argomento è una guida completa, ma semplicemente una guida introduttiva per l'utilizzo dello Strumento di pianificazione nelle sessioni di progettazione.



## Per iniziare a utilizzare lo strumento di pianificazione e creare un progetto iniziale

1.  Avviare lo Strumento di pianificazione di Lync Server 2013: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Strumento di pianificazione**.

2.  Dopo l'avvio dello Strumento di pianificazione, viene visualizzata la pagina iniziale dello strumento di pianificazione per Microsoft Lync Server 2013 . Scegliere una delle opzioni seguenti per iniziare la progettazione:
    
      - **Opzione 1: Per iniziare**   Fare clic su **Per iniziare** per visualizzare una serie specifica di domande di questionario con selezioni appropriate per definire i criteri. Dopo aver completato la sezione iniziale del questionario di **Per iniziare** , passare alla sezione **Progetta siti** per definire l'architettura dei siti. Per completare questa opzione, procedere al passaggio 3.
    
      - **Opzione 2: Progetta siti**   Fare clic su **Progetta siti** per ignorare le domande di questionario presentate nella sezione **Per iniziare** . Le informazioni che sarebbero state raccolte rispondendo alle domande della sezione **Per iniziare** vengono impostate sui valori predefiniti. Facendo clic su **Progetta siti** , i progettisti esperti possono ignorare il questionario iniziale e modificare i valori predefiniti secondo necessità nella pagina iniziale **Siti centrali** . Per completare questa opzione, ignorare i passaggi da 3 a 5 e iniziare dal passaggio 6.
    
      - **Opzione 3: Visualizza la topologia salvata**   Se è già stata completata e salvata una topologia utilizzando lo Strumento di pianificazione in precedenza, è possibile ignorare la maggior parte di questi passaggi e iniziare aprendo la topologia. È inoltre possibile apportare modifiche e aggiornamenti alla topologia, risalvarla e quindi esportarla in Microsoft Excel o Microsoft Visio. Per completare questa opzione, ignorare i passaggi da 3 a 12 e iniziare dal passaggio 13.

3.  Fare clic su **Per iniziare** per iniziare a progettare la topologia di Lync Server 2013.

4.  Rispondere alle domande di ogni sezione selezionando i criteri appropriati per il progetto e quindi fare clic su **Avanti** per passare alla pagina successiva della procedura guidata. Fare clic su **Indietro** per modificare le pagine precedenti.
    
    > [!tip]  
    > Ogni pagina contiene una descrizione dei criteri di selezione e alcuni consigli in base alle procedure preferite e alla pianificazione della capacità. Se sono necessari ulteriori dettagli, fare clic su <strong>Ulteriori informazioni</strong> per leggere altre informazioni nella documentazione relativa alla pianificazione di Lync Server 2013 sul sito Web Microsoft TechNet. Per accedere a questo sito Web, è necessario disporre di connettività Internet.

5.  Selezionare le opzioni appropriate per la progettazione. Dopo la definizione dei criteri iniziali, verrà visualizzata la conferma del completamento della panoramica iniziale.

6.  Fare clic su **Progetta siti** per definire il sito centrale.
    

    > [!NOTE]
    > Ogni topologia di Lync Server 2013 conterrà almeno un sito centrale. È possibile progettare un singolo sito centrale, un sito centrale con diversi siti di succursale, diversi siti centrali o diversi siti centrali con siti di succursale associati a ogni sito centrale.



7.  In **Nome sito** digitare il nome che identificherà questo sito centrale.

8.  In **Utenti ospitati nel sito** digitare il numero previsto di utenti simultanei locali che verranno ospitati in questo sito centrale.

9.  In **Utenti ospitati nel cloud** digitare il numero previsto di utenti simultanei online che verranno ospitati in questo sito centrale.

10. Modificare le selezioni per la collaborazione online, gli utenti, le funzionalità voce, altre opzioni di distribuzione o applicazioni server, se necessario.
    
    > [!important]  
    > In questa fase della progettazione, è possibile selezionare o deselezionare solo queste opzioni per la distribuzione. È tuttavia possibile configurare altre opzioni in una fase successiva dello Strumento di pianificazione. Alcune opzioni non sono disponibili e non possono essere deselezionate. Inoltre, può essere necessario deselezionare un'opzione per deselezionarne un'altra. Se ad esempio si seleziona l'opzione <strong>VoIP aziendale</strong> in Voce, verranno deselezionate anche le opzioni <strong>Response Group</strong> , <strong>Annunci</strong> e <strong>Parcheggio di chiamata</strong> in Applicazioni server (tutte funzionalità di VoIP aziendale).

11. Dopo aver definito il nome del sito e il numero di utenti, fare clic su **Avanti** .

12. Nelle pagine seguenti vengono richieste informazioni su domini SIP, impostazioni di conferenza, impostazioni e infrastruttura voce, Messaggistica unificata di Exchange, accesso di utenti esterni, impostazioni di Chat persistente, impostazioni client, opzioni di collocazione e siti di succursale. Rispondere a queste domande nel modo appropriato.

13. Nella domanda finale viene chiesto se si desidera creare un altro sito centrale. Se si seleziona **Sì** , si ritorna nella pagina Siti centrali dello Strumento di pianificazione. Se si seleziona **No** , fare clic su **Avanti** , quindi su **Disegna** per visualizzare la vista Topologia globale di livello superiore.

14. Per visualizzare una topologia esistente, fare clic su **Visualizza** .

15. Fare clic sul file XML che corrisponde alla topologia salvata in precedenza e quindi su **Apri** .

16. Nello Strumento di pianificazione verrà visualizzata la pagina Topologia globale. È ora possibile iniziare a modificare, aggiornare o cambiare la topologia con gli strumenti disponibili nello Strumento di pianificazione.

## Vedere anche

#### Concetti

[Modifica della progettazione in Lync Server 2013](lync-server-2013-editing-the-design.md)

