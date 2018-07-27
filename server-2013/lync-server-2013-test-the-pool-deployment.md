---
title: 'Lync Server 2013: Testare la distribuzione di pool'
TOCTitle: Testare la distribuzione di pool
ms:assetid: ffd80617-155a-4041-bbeb-74503e7938dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413092(v=OCS.15)
ms:contentKeyID: 49302597
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testare la distribuzione di pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-09-25_

Nella procedura seguente viene descritto come testare la distribuzione del pool Front End.

## Per testare la distribuzione di pool

1.  Utilizzare Utenti e computer Active Directory per aggiungere l'oggetto utente di Active Directory del ruolo di amministratore per la distribuzione di Lync Server 2013 (in cui è installato il Pannello di controllo di Lync Server 2013) al gruppo **CSAdministrator** .
    
    > [!IMPORTANT]  
    > Se non si aggiungono gli utenti e i gruppi appropriati al gruppo CsAdministrator, verrà visualizzato un errore all'apertura del Pannello di controllo di Lync Server con il messaggio &quot;Non autorizzato: accesso negato a causa di autorizzazione di controllo di accesso basato su ruoli (RBAC) non riuscita&quot;.

2.  Se l'oggetto utente è connesso, disconnettersi e rieseguire l'accesso per registrare la nuova assegnazione al gruppo.
    

    > [!NOTE]
    > L'account utente non può essere l'amministratore locale di qualsiasi server che esegue Lync Server 2013.



3.  Utilizzare l'account amministrativo per accedere al computer in cui è installato il Pannello di controllo di Lync Server.

4.  Avviare il Pannello di controllo di Lync Server e specificare le credenziali, se richieste. Nel Pannello di controllo di Lync Server verranno visualizzate informazioni sulla distribuzione.

5.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi verificare che lo stato del servizio riporti un'icona di computer con una freccia verde e che sia presente un segno di spunta verde per lo stato di replica accanto a ogni ruolo del server di Lync Server distribuito e portato online.

6.  Sulla barra di spostamento sinistra fare clic su **Utenti** e quindi su **Abilita utenti** .

7.  Nella pagina **Nuovo utente di Lync Server** fare clic su **Aggiungi** .

8.  Per definire i parametri di ricerca per gli oggetti che si desidera trovare, nella pagina **Seleziona da Active Directory** è possibile selezionare **Cerca** e quindi facoltativamente fare clic su **Aggiungi filtro** . È anche possibile selezionare **Ricerca LDAP** e immettere un'espressione LDAP per filtrare o limitare gli oggetti che verranno restituiti. Dopo aver deciso le opzioni di ricerca, fare clic su **Trova** .

9.  Nel riquadro dei risultati di ricerca selezionare tutti gli oggetti per questa sessione di ricerca e quindi fare clic su **OK** .

10. Nella pagina **Nuovo utente di Lync Server** l'oggetto o gli oggetti selezionati si trovano nella visualizzazione **Utenti** . Nell'elenco **Assegna utenti a un pool** selezionare il server in cui verranno ospitati gli oggetti.
    
    Di seguito sono riportate alcune opzioni di configurazione degli oggetti.
    
      - **Genera URI SIP utente**
    
      - **Telefonia**
    
      - **URI linea**
    
      - **Criteri conferenza**
    
      - **Criteri versione client**
    
      - **Criteri PIN**
    
      - **Criteri di accesso esterno**
    
      - **Criteri di archiviazione**
    
      - **Criteri percorso**
    
      - **Criteri client**
    
    Ai fini del test delle funzionalità di base, selezionare l'opzione preferita per l'impostazione **Genera URI SIP utente** (per le altre opzioni nella configurazione verranno utilizzate le impostazioni predefinite) e fare clic su **Abilita** .

11. Verrà visualizzata una pagina di riepilogo con un segno di spunta nella colonna **Abilitato** per indicare che gli oggetti sono pronti per l'uso. La colonna **Indirizzo SIP** visualizza l'indirizzo necessario per la configurazione dell'accesso degli utenti.

12. Connettere un utente a un computer appartenente al dominio e un altro utente a un altro computer nel dominio.

13. Installare Lync 2013 in ognuno dei due computer client e quindi verificare che entrambi gli utenti possano accedere a Lync Server 2013 e scambiarsi messaggi istantanei.

## Vedere anche

#### Concetti

[Distribuzione di client e dispositivi in Lync Server 2013](lync-server-2013-deploying-clients-and-devices.md)

