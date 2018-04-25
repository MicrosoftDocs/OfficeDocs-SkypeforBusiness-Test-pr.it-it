---
title: Creazione o modifica dei siti di rete
TOCTitle: Creazione o modifica dei siti di rete
ms:assetid: 358aa08a-c5bc-45fc-8017-19e6202f88c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520975(v=OCS.15)
ms:contentKeyID: 49300143
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione o modifica dei siti di rete

 

_**Ultima modifica dell'argomento:** 2012-10-08_

I siti di rete sono gli uffici o le postazioni configurate in ogni area di una distribuzione del servizio Controllo di ammissione di chiamata (CAC) o del servizio per chiamate di emergenza Enhanced 9-1-1. È possibile usare il Pannello di controllo di Microsoft Lync Server 2013 per configurare i siti e associarli alle aree. Ad esempio, un'area di rete per il Nord America potrebbe essere associata a siti di rete come Chicago, Redmond e Vancouver. Deve essere creato un sito di rete del servizio Controllo di ammissione di chiamata per ogni sito di un'organizzazione, anche se tale sito non presenta limitazioni della larghezza di banda. Dal Pannello di controllo di Lync Server è possibile creare, modificare ed eliminare siti di rete. Seguire le procedure seguenti per creare o modificare un sito di rete. Per informazioni dettagliate sull'eliminazione di un sito di rete esistente, vedere [Eliminazione di un sito di rete esistente](lync-server-2013-deleting-an-existing-network-site.md).

## Per creare un sito di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Sito**.

4.  Nella pagina **Sito** fare clic su **Nuovo**.

5.  In **Nuovo sito** digitare un nome per il sito nel campo **Nome**.
    

    > [!NOTE]
    > I nomi dei siti devono essere univoci nella distribuzione di Lync Server 2013.



6.  Nell'elenco a discesa **Area** selezionare un'area di rete da associare al sito.

7.  (Facoltativo) Se si desidera applicare limiti di larghezza di banda per le chiamate audio o video per il sito, selezionare il profilo del criterio larghezza di banda con le impostazioni appropriate nell'elenco a discesa **Criteri larghezza di banda**.
    

    > [!NOTE]
    > È possibile visualizzare i dettagli dei profili dei criteri larghezza di banda disponibili o creare un nuovo profilo di criterio larghezza di banda nella pagina <STRONG>Profilo criteri</STRONG> del gruppo <STRONG>Configurazione di rete</STRONG>. Per informazioni dettagliate, vedere <A href="lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md">Creazione o modifica di profili di criteri di larghezza di banda</A>.



8.  (Facoltativo) Se si desidera specificare impostazioni di posizione per questo sito, selezionare un criterio percorso nell'elenco a discesa **Criteri percorso**.
    

    > [!NOTE]
    > Il criterio percorso assegna impostazioni specifiche di Enhanced 9-1-1 (E9-1-1) e delle posizioni client al sito. È possibile visualizzare i dettagli dei criteri percorso disponibili o creare un nuovo criterio percorso nella pagina <STRONG>Criteri percorso</STRONG> del gruppo <STRONG>Configurazione di rete</STRONG>. Per informazioni dettagliate, vedere <A href="lync-server-2013-viewing-location-policy-information.md">Visualizzazione delle informazioni sui criteri percorso</A>.



9.  (Facoltativo) Digitare un valore nel campo **Descrizione** per fornire ulteriori informazioni sul sito che non possono essere espresse utilizzando solo il nome.

10. Fare clic su **Commit**.
    

    > [!NOTE]
    > Quando si crea un nuovo sito di rete, non si utilizza la tabella <STRONG>Subnet associate</STRONG>. L'associazione di una subnet a un sito viene effettuata quando si crea o si modifica la subnet. Per informazioni dettagliate, vedere <A href="lync-server-2013-create-or-modify-network-subnets.md">Creare o modificare subnet di rete</A>.



## Per modificare un sito di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Sito**.

4.  Nella pagina **Sito** fare clic sul sito che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Nella pagina **Modifica sito** è possibile modificare la descrizione, l'area, il profilo del criterio larghezza di banda e il criterio percorso associati al sito. Per informazioni dettagliate, vedere la sezione "Per creare un sito di rete" più indietro in questo argomento.

7.  Fare clic su **Commit**.

Non è possibile modificare la tabella **Subnet associate** in questa pagina. L'elenco di subnet associate viene fornito come riferimento per indicare quali subnet saranno interessate in caso di modifica delle impostazioni del sito.

## Per eliminare un sito di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Sito**.

4.  Nella pagina **Sito** fare clic sul sito che si desidera eliminare.
    

    > [!NOTE]
    > È possibile eliminare più siti contemporaneamente. A tale scopo, premere CTRL e selezionare più siti sempre tenendo premuto CTRL. In alternativa, per selezionare tutti i siti, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG>.



5.  Scegliere **Elimina** dal menu **Modifica**.

6.  Fare clic su **OK**.
    

    > [!WARNING]
    > Se un sito di rete è associato a una subnet di rete, non è possibile rimuoverlo. Se si tenta di rimuovere un sito associato a una subnet, verrà visualizzato un messaggio di errore. Per controllare se un sito è associato a eventuali subnet, fare clic sul sito e quindi scegliere <STRONG>Mostra dettagli</STRONG> dal menu <STRONG>Modifica</STRONG>.



## Vedere anche

#### Attività

[Eliminazione di un sito di rete esistente](lync-server-2013-deleting-an-existing-network-site.md)  

#### Ulteriori risorse

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

