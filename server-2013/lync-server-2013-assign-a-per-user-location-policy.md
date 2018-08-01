---
title: Assegnare criteri percorso per utente
TOCTitle: Assegnare criteri percorso per utente
ms:assetid: 343f2de3-a0ae-4403-8456-6e520b579d32
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520974(v=OCS.15)
ms:contentKeyID: 49300137
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri percorso per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Il criterio percorso è una delle singole impostazioni di un account utente che è possibile configurare nel Pannello di controllo di Lync Server.

La distribuzione di uno o più criteri percorso per utente è facoltativa. È inoltre possibile distribuire un solo criterio percorso a livello globale o a livello di subnet. Se si distribuiscono criteri per utente, è necessario assegnarli in modo esplicito agli utenti, ai gruppi o agli oggetti contatto. Se non sono assegnati criteri specifici a livello di subnet o per utente, per impostazione predefinita in Enhanced 9-1-1 (E9-1-1) vengono utilizzate automaticamente le impostazioni definite nel criterio a livello globale.

Dopo aver creato almeno un criterio percorso per utente, utilizzare le procedure descritte in questo argomento per assegnare il criterio che specifica le impostazioni che devono essere applicate dal server per le chiamate di emergenza effettuate da un utente specifico.

Per un elenco di tutte le impostazioni dei criteri percorso disponibili, vedere [Definizione di criteri percorso per Lync Server 2013](lync-server-2013-defining-the-location-policy.md).

Per informazioni dettagliate sulla creazione di criteri percorso, vedere [Creare criteri percorso in Lync Server 2013](lync-server-2013-create-location-policies.md).

## Per assegnare un criterio percorso per utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Ricerca utenti** digitare interamente o parzialmente il nome visualizzato, il nome, il cognome, il nome account del sistema degli account di sicurezza (SAM), l'indirizzo SIP o l'URI (Uniform Resource Identifier) linea dell'account utente e quindi fare clic su **Trova**.
    
      - Se si dispone di una query salvata, fare clic sull'icona **Apri query**, utilizzare la finestra di dialogo **Apri** per recuperare la query (file con estensione usf) e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare ulteriori criteri di ricerca per circoscrivere i risultati:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Digitare la proprietà utente oppure selezionarla facendo clic sulla freccia nell'elenco a discesa.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore, ad esempio **Uguale a** o **Diverso da**.
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri che si desidera utilizzare per filtrare i risultati della ricerca digitandoli oppure facendo clic sulla freccia nell'elenco a discesa.
        
        > [!TIP]  
        > Per aggiungere ulteriori clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong>.    
    5.  Fare clic su **Trova**.

6.  Fare clic su un utente nei risultati della ricerca, su **Azione** e quindi su **Assegna criteri**.
    
    > [!TIP]  
    > Se si desidera applicare lo stesso criterio percorso per utente a più utenti, selezionare più utenti nei risultati della ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.

7.  In **Criteri percorso** in **Assegna criteri** eseguire una delle operazioni seguenti:
    

    > [!NOTE]
    > Poiché è possibile configurare più criteri tramite la finestra di dialogo <STRONG>Assegna criteri</STRONG>, per ogni criterio nella finestra di dialogo è selezionato per impostazione predefinita <STRONG>&lt;Mantieni invariati&gt;</STRONG>. Si continua a utilizzare il criterio precedentemente assegnato all'utente se non si modifica questa impostazione.

    
      - Consentire a Lync Server 2013 di scegliere automaticamente il criterio a livello globale oppure, se definito, il criterio a livello di subnet.
    
      - Fare clic sul nome di un criterio percorso per utente precedentemente definito eseguendo il cmdlet **New-CsLocationPolicy**.
        
        > [!TIP]  
        > Per scegliere il criterio da assegnare, dopo aver fatto clic sul nome, fare clic su <strong>Visualizza</strong> per visualizzare le autorizzazioni e i diritti utente definiti nel criterio.

8.  Al termine, fare clic su **OK**.

## Per assegnare un criterio percorso per utente usando il Lync Server Management Shell

È possibile assegnare criteri percorso per utente utilizzando il cmdlet Grant-CsLocationPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per assegnare un criterio percorso per utente a un utente singolo

  - Il comando seguente consente di assegnare i criteri percorso per utente denominati RedmondLocationPolicy all'utente Ken Myer.
    
        Grant-CsLocationPolicy -Identity "Ken Myer" -PolicyName "RedmondLocationPolicy"

## Per assegnare un criterio percorso per utente a più utenti

  - Questo comando assegna il criterio percorso per utente AccountingDepartmentLocationPolicy a tutti gli utenti che lavorano per il reparto Contabilità. Per ulteriori informazioni sul parametro LdapFilter utilizzato in questo comando, vedere la documentazione relativa al cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -LdapFilter "Department=Accounting" | Grant-CsLocationPolicy -PolicyName "AccountingDepartmentLocationPolicy"

## Per annullare l'assegnazione di un criterio percorso per utente

  - Il comando seguente annulla l'assegnazione dei criteri percorso per utente precedentemente assegnati all'utente Ken Myer. Dopo l'annullamento dell'assegnazione dei criteri per utente, Ken Myer verrà gestito automaticamente tramite i criteri globali oppure i criteri di sito locale, se esistenti. I criteri di sito sono prioritari rispetto ai criteri globali.
    
        Grant-CsLocationPolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Grant-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsLocationPolicy).

