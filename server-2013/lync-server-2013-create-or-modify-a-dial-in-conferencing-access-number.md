---
title: 'Lync Server 2013: Creare o modificare un numero di accesso per una conferenza telefonica con accesso esterno'
TOCTitle: Creare o modificare un numero di accesso per una conferenza telefonica con accesso esterno
ms:assetid: 06f55c28-57f8-4d4e-8313-9740846796d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398126(v=OCS.15)
ms:contentKeyID: 49299571
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un numero di accesso per una conferenza telefonica con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Eseguire questa procedura se si desidera creare o modificare un numero di accesso per partecipare a una conferenza telefonica con accesso esterno.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima di creare un nuovo numero di accesso esterno, è necessario impostare per tale numero un'area di conferenza telefonica con accesso esterno associata al dial plan. Più dial plan possono utilizzare la stessa area.</td>
</tr>
</tbody>
</table>


## Per creare o modificare un numero di accesso esterno

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Servizi di conferenza** e quindi fare clic su **Numero di accesso esterno** .

4.  Nella pagina **Numero di accesso esterno** eseguire una delle operazioni seguenti:
    
      - Fare clic su **Nuovo** per aprire **Nuovo numero di accesso esterno** .
    
      - Fare clic su uno dei numeri di accesso esterno nell'elenco, fare clic su **Modifica** e quindi su **Mostra dettagli** .
        

        > [!NOTE]
        > Se si utilizza il campo di ricerca per cercare il contenuto di una colonna nell'elenco dei numeri di accesso esterno, i risultati ottenuti potrebbero non essere quelli previsti. Ordinare invece l'elenco in base alla colonna a cui si è interessati per identificare il numero di accesso esterno da visualizzare o modificare.



5.  In **Numero visualizzato** digitare il numero di telefono che gli utenti della rete PSTN (Public Switched Telephone Network) devono comporre per partecipare a una conferenza.
    

    > [!NOTE]
    > Questo numero viene visualizzato negli inviti alle riunioni e nella pagina Web Impostazioni conferenza telefonica con accesso esterno.



6.  In **Nome visualizzato** digitare una descrizione per il numero di accesso esterno. Questo è il nome associato al numero di accesso esterno nei risultati di ricerca di Lync.
    

    > [!NOTE]
    > Questo nome viene visualizzato nel client quando un utente chiama il numero di accesso.



7.  In **URI linea** digitare il numero E.164 del numero di accesso esterno nel formato URI TEL, preceduto dal simbolo + e senza utilizzare spazi. Ad esempio, tel:+14255550200.
    

    > [!NOTE]
    > Non è possibile riutilizzare lo stesso URI linea per un altro numero di accesso per conferenze con accesso esterno.



8.  In **URI SIP** eseguire le operazioni seguenti:
    
      - Nella casella di testo digitare un URI SIP univoco per il numero di accesso per conferenze con accesso esterno. Questo URI SIP viene visualizzato in diverse posizioni, tra cui, in via esemplificativa, nei messaggi di notifica delle chiamate e nelle versioni precedenti dei client Communicator.
        

        > [!NOTE]
        > Non è possibile riutilizzare lo stesso URI SIP per un altro numero di accesso per conferenze con accesso esterno. L'URI SIP non può essere modificato dopo che il numero di accesso è stato creato. L'unico modo per modificare l'URI SIP è quello di eliminare e ricreare il numero di accesso.

    
      - Nell'elenco a discesa fare clic sul dominio dell' applicazione Operatore Conferenza che supporta il numero di accesso esterno.

9.  In **Pool** fare clic sul pool che esegue l'istanza di Operatore Conferenza che supporta il numero di accesso esterno.
    

    > [!NOTE]
    > Se è necessario modificare il pool dopo avere creato il numero di accesso, utilizzare il cmdlet <STRONG>Move-CsApplicationEndpoint</STRONG> oppure eliminare e ricreare il numero di accesso.



10. In **Lingua principale** fare clic sulla lingua in cui verranno riprodotte le richieste per il numero di accesso esterno.
    

    > [!NOTE]
    > La lingua principale è la lingua utilizzata da Operatore Conferenza per rispondere alla chiamata. Le lingue supportate vengono visualizzate insieme a ogni numero di telefono di accesso nella pagina Web Impostazioni conferenza telefonica con accesso esterno.



11. (Facoltativo) In **Lingue secondarie (massimo quattro)** fare clic su **Aggiungi** , selezionare una o più lingue aggiuntive che si desidera supportare per i chiamanti al numero di accesso esterno e quindi fare clic su **OK** .
    

    > [!NOTE]
    > È possibile selezionare fino a quattro lingue secondarie per ogni numero di accesso esterno. Gli utenti possono selezionare una lingua secondaria prima di immettere l'ID conferenza quando chiamano per partecipare a una conferenza.



12. Per aggiungere un'area per il numero di accesso esterno, in **Aree associate** fare clic su **Aggiungi** , su una o più aree associate ai dial plan per il numero di accesso esterno e quindi su **OK** .

13. Per eliminare un'area dal numero di accesso esterno, in **Aree associate** fare clic sull'area desiderata e quindi su **Rimuovi** .

14. Fare clic su **Commit** .

