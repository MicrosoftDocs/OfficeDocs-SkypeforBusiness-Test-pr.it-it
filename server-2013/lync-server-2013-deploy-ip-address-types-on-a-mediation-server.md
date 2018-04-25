---
title: 'Lync Server 2013: Distribuire i tipi di indirizzi IP in un Mediation Server'
TOCTitle: Distribuire i tipi di indirizzi IP in un Mediation Server
ms:assetid: 689ebed5-96ee-4cd4-b7ae-ee2a86a1d9b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204964(v=OCS.15)
ms:contentKeyID: 49300846
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire i tipi di indirizzi IP in un Mediation Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-24_

Utilizzando Generatore di topologie, eseguire i passaggi della procedura riportata di seguito per distribuire i tipi di indirizzi IP in un Mediation Server.

## Per distribuire i tipi di indirizzi IP in un Mediation Server

  - In Generatore di topologie fare clic con il pulsante destro del mouse sul server in un pool in **Pool Mediation Server** e quindi scegliere **Modifica proprietà**. (In alternativa, selezionare il server e quindi scegliere **Modifica proprietà** dal menu **Azione**.)

  - Nella finestra di dialogo **Modifica proprietà** selezionare il tipo di indirizzo IP che si desidera configurare. Per una configurazione con dual stack, selezionare **Abilita IPv4** e **Abilita IPv6**, come illustrato nella figura seguente.
    
    **Finestra di dialogo Modifica proprietà per il pool Mediation Server**
    
    ![Pagina delle proprietà generali di Lync Server con FQDN](images/JJ204964.4e650aca-dbff-4a86-b10d-f0162c032539(OCS.15).png "Pagina delle proprietà generali di Lync Server con FQDN")
    
      - **Usa tutti gli indirizzi IP configurati**. Selezionare questa opzione se si desidera consentire l'utilizzo di qualsiasi indirizzo IP definito nel computer.
        

        > [!NOTE]
        > Questa è l'opzione consigliata per le configurazioni IP versione 6 (IPv6).

    
      - **Limita utilizzo servizio a indirizzi IP selezionati**. Selezionare questa opzione per specificare un indirizzo specifico da utilizzare nel nuovo server. Se si seleziona questa opzione è necessario immettere un valore per Indirizzo IP primario.
    
      - **Indirizzo IP primario**. Immettere un indirizzo IP che verrà utilizzato dal server per tutte le comunicazioni, tranne quelle su rete PSTN (Public Switched Telephone Network). L'indirizzo IP immesso deve corrispondere al formato del tipo di indirizzo selezionato.
    
      - **Indirizzo IP PSTN**. Definire un indirizzo IP PSTN quando un Mediation Server è collocato nel Front End Server. Questo indirizzo deve corrispondere al formato del tipo di indirizzo selezionato.
        

        > [!NOTE]
        > L'installazione di altre schede di interfaccia di rete per il supporto della configurazione dell'indirizzo IP PSTN per Lync Server 2013 non è supportata. Per ulteriori informazioni sulle configurazioni di schede di interfaccia di rete supportate per Lync Server 2013, vedere <A href="lync-server-2013-server-hardware-platforms.md">Piattaforme hardware server per Lync Server 2013</A>.


