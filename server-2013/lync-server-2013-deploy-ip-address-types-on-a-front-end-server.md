---
title: 'Lync Server 2013: Distribuire i tipi di indirizzi IP in un Front End Server'
TOCTitle: Distribuire i tipi di indirizzi IP in un Front End Server
ms:assetid: b6c8e0f9-ec8e-4a4e-a525-756f9cd6b9d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205191(v=OCS.15)
ms:contentKeyID: 49301747
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire i tipi di indirizzi IP in un Front End Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-14_

Utilizzando Generatore di topologie, eseguire i passaggi della procedura riportata di seguito per distribuire i tipi di indirizzi IP in un Front End Server.

## Per distribuire i tipi di indirizzi IP in un Front End Server

1.  In **Pool Enterprise Edition Front End** fare clic con il pulsante destro del mouse sul server all'interno di un pool e quindi scegliere **Modifica proprietà** . In alternativa, selezionare il server e quindi scegliere **Modifica proprietà** dal menu **Azione** .

2.  Nella finestra di dialogo **Modifica proprietà** selezionare il tipo di indirizzo IP che si desidera configurare. Per una configurazione con dual stack, selezionare **Abilita IPv4** e **Abilita IPv6** , come illustrato nella figura seguente.
    
    **Finestra di dialogo Modifica proprietà per il pool Front End Server**
    
    ![Finestra di dialogo Modifica proprietà del server Front End](images/JJ205191.737a9d71-c0bc-4a54-9608-9e028dacc814(OCS.15).png "Finestra di dialogo Modifica proprietà del server Front End")
    
      - **Usa tutti gli indirizzi IP configurati**. Selezionare questa opzione se si desidera consentire l'utilizzo di qualsiasi indirizzo IP definito nel computer.
        

        > [!NOTE]
        > Questa è l'opzione consigliata per le configurazioni IP versione 6 (IPv6).

    
      - **Limita utilizzo servizio a indirizzi IP selezionati**. Selezionare questa opzione per specificare un determinato indirizzo da utilizzare nel nuovo server. Se si seleziona questa opzione, sarà necessario immettere un valore per **Indirizzo IP primario** .
    
      - **Indirizzo IP primario**. Immettere un indirizzo IP che verrà utilizzato dal server per tutte le comunicazioni, tranne quelle su rete PSTN (Public Switched Telephone Network). L'indirizzo IP immesso deve corrispondere al formato del tipo di indirizzo selezionato.
    
      - **Indirizzo IP PSTN**. Definire un indirizzo IP PSTN quando un Mediation Server è collocato nel Front End Server. Questo indirizzo deve corrispondere al formato del tipo di indirizzo selezionato.

