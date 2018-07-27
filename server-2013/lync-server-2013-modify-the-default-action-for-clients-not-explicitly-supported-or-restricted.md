---
title: Modificare l'azione predefinita per i client non supportati in modo esplicito o con restrizioni
TOCTitle: Modificare l'azione predefinita per i client non supportati in modo esplicito o con restrizioni
ms:assetid: 548dd0f5-62fe-4c3f-8952-2b9fd4c5fff3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520994(v=OCS.15)
ms:contentKeyID: 49300541
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare l'azione predefinita per i client non supportati in modo esplicito o con restrizioni

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Oltre a specificare la versione dei client che si desidera supportare nell'ambiente Lync Server 2013, è possibile specificare un'azione predefinita per i client per i quali non è già stato definito un criterio di versione. In tal modo è possibile limitare le versioni client utilizzate nell'ambiente Lync Server e questo può contribuire a tenere sotto controllo i costi associati al supporto di più versioni client.

## Per modificare l'azione predefinita per i client non supportati in modo esplicito o con restrizioni

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra spostamento sinistra fare clic su **Client** e quindi su **Configurazione versione client**.

4.  Nella pagina **Configurazione versione client** fare doppio clic sulla configurazione **Globale** nell'elenco.

5.  Nella finestra di dialogo **Modifica Configurazione versione client** verificare che la casella di controllo **Abilita controllo versione** sia selezionata e quindi selezionare una delle opzioni seguenti in **Azione predefinita**:
    
      - **Consenti**   Consente al client di eseguire l'accesso se la versione del client non corrisponde ad alcun filtro nell'elenco **Criteri versione client**.
    
      - **Blocca**   Impedisce al client di eseguire l'accesso se la versione del client non corrisponde ad alcun filtro nell'elenco **Criteri versione client**.
    
      - **Blocca con URL**   Impedisce al client di eseguire l'accesso se la versione del client non corrisponde ad alcun filtro nell'elenco **Criteri versione client** e include un messaggio di errore contenente l'URL della posizione da cui è possibile scaricare un client più recente.
    
      - **Consenti con URL**   Consente al client di eseguire l'accesso se la versione del client non corrisponde ad alcun filtro nell'elenco **Criteri versione client** e include un messaggio di errore contenente l'URL della posizione da cui è possibile scaricare un client più recente.

6.  Se si seleziona **Blocca con URL**, digitare l'URL per il download del client da includere nel messaggio di errore nella casella **URL**.

7.  Fare clic su **Commit**.

## Per disabilitare il controllo delle versioni client

  - Per disabilitare il controllo delle versioni in modo da consentire l'accesso a tutti i client indipendentemente dalla versione del client, deselezionare la casella di controllo **Abilita controllo versione** e quindi fare clic su **Commit**.

## Modifica dell'azione predefinita mediante i cmdlet di PowerShell per Lync Server

È possibile gestire l'azione predefinita da eseguire quando gli utenti provano ad accedere usando un client non esplicitamente supportato o limitato dai criteri relativi alla versione del client anche mediante interfaccia della riga di comando Windows PowerShell e il cmdlet **Set-CsClientVersionPolicy**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Configurazione dell'azione predefinita per il blocco dell'accesso

  - Il comando seguente imposta l'azione predefinita per il blocco del sito Redmond. La registrazione è bloccata per i client per i quali non esiste una regola di configurazione della versione.
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -DefaultAction Block

## Configurazione dell'azione predefinita per consentire l'accesso

  - In questo esempio l'azione predefinita per il blocco del sito Redmond è Allow. La registrazione è consentita per i client per i quali non esiste una regola di configurazione della versione.
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -DefaultAction Allow

Per informazioni dettagliate, vedere l'argomento della guida relativo al cmdlet [Set-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionPolicy).

## Vedere anche

#### Ulteriori risorse

[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

