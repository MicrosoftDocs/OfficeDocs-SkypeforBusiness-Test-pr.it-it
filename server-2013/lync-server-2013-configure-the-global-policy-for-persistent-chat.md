---
title: 'Lync Server 2013: Configurare i criteri globali per Chat persistente'
TOCTitle: Configurare i criteri globali per Chat persistente
ms:assetid: 6176eb5c-19de-4c07-bcc0-2e38f8965966
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204951(v=OCS.15)
ms:contentKeyID: 49300749
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i criteri globali per Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

È possibile utilizzare i criteri globali predefiniti da soli per abilitare le impostazioni di Chat persistente per tutti gli utenti della distribuzione. È inoltre possibile specificare ulteriori criteri per i siti e gli utenti per stabilire se Chat persistente deve essere abilitato o disabilitato per utenti e siti specifici.

Non è possibile eliminare i criteri globali. Se si tenta l'eliminazione, la configurazione viene reimpostata sui valori predefiniti.


> [!NOTE]
> Per configurare e utilizzare il server Chat persistente, è innanzitutto necessario utilizzare Generatore di topologie per aggiungere il supporto del server Chat persistente alla topologia e quindi pubblicare la topologia. Per informazioni dettagliate, vedere <A href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.<BR>Per configurare le impostazioni di configurazione del server Chat persistente, vedere <A href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Per configurare i criteri globali per Chat persistente

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator, CsAdministrator o CsUserAdministrator , eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Dal menu **Start** selezionare il Pannello di controllo di Lync Server oppure aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi utilizzabili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md) nella documentazione relativa alle operazioni.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>È inoltre possibile utilizzare i cmdlet di Windows PowerShell. Per informazioni dettagliate, vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.</td>
    </tr>
    </tbody>
    </table>


3.  In Pannello di controllo di Lync Server fare clic su **Chat persistente** e quindi su **Criteri Chat persistente**.

4.  Fare clic su **Globale** nell'elenco dei criteri, fare clic su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica criteri Chat persistente - Globale** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nuovo nome per i criteri globali, se non si desidera utilizzare il nome predefinito Globale.
    
      - In **Descrizione** immettere informazioni dettagliate sugli scopi dei criteri utente, ad esempio "Criteri globali per *NomeSitoCentrale* ".
    
      - Per controllare Chat persistente per tutti i siti e gli utenti non controllati in modo specifico tramite criteri utente o di sito, selezionare o deselezionare la casella di controllo **Abilita Chat persistente**.

6.  Fare clic su **Commit** .

