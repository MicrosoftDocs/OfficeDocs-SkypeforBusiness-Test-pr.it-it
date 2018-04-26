---
title: Spostare gli utenti in un altro pool in Lync Server 2013
TOCTitle: Spostare gli utenti in un altro pool in Lync Server 2013
ms:assetid: e7b4968c-0e9d-4d56-b5f1-9edf0f7206f8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182600(v=OCS.15)
ms:contentKeyID: 49302323
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare gli utenti in un altro pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-11_

È possibile utilizzare Pannello di controllo di Lync Server per assegnare gli utenti a un server o a un pool specifico.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se tutti gli utenti di un pool che esegue Microsoft Office Communications Server 2007 R2 o una versione precedente vengono spostati in un pool di Lync Server 2013 di destinazione in un ambiente Active Directory complesso, è possibile che la replica di Active Directory sia più lenta. Per evitare questo problema, è possibile utilizzare filtri di ricerca per spostare separatamente gli utenti da pool che eseguono Microsoft Office Communications Server 2007 R2 o una versione precedente. In alternativa, è possibile utilizzare Lync Server Management Shell per spostare gli utenti con i cmdlet. Inoltre, la funzionalità di filtro funziona con gli utenti di Lync Server 2013.</td>
</tr>
</tbody>
</table>


## Per spostare un gruppo selezionato di utenti in un server o un pool diverso

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Cerca utenti** digitare anche solo la prima parte del nome visualizzato, nome, cognome, nome dell'account Gestione account di protezione, indirizzo SIP o URI (Uniform Resource Identifier (URI) di linea dell'account utente desiderato e quindi fare clic su **Trova**.

5.  Nell'elenco della tabella selezionare uno o più utenti specifici.

6.  Scegliere **Sposta utenti selezionati nel pool** dal menu **Azione**.

7.  In **Sposta utenti** selezionare il pool in cui spostare gli utenti in **Pool di registrazione di destinazione**.

8.  (Facoltativo) Se il server o il pool di destinazione non è disponibile, selezionare la casella di controllo **Forza**.
    

    > [!WARNING]
    > Se si seleziona <STRONG>Forza</STRONG>, l'account utente viene spostato, ma i dati utente associati vengono eliminati, ad esempio le conferenze pianificate dall'utente. Se non si seleziona questa casella di controllo, vengono spostati sia l'account sia i dati associati.



## Per spostare tutti gli utenti da un server o un pool a un server o un pool diverso

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Scegliere **Sposta tutti gli utenti nel pool** dal menu **Azione**.

5.  In **Sposta utenti** selezionare il pool contenente gli account utente da spostare in **Pool di registrazione di origine**.

6.  In **Pool di registrazione di destinazione** selezionare il pool in cui spostare gli utenti.

7.  (Facoltativo) Se il server o il pool di destinazione non è disponibile, selezionare la casella di controllo **Forza**.
    

    > [!WARNING]
    > Se si seleziona <STRONG>Forza</STRONG>, l'account utente viene spostato, ma i dati utente associati vengono eliminati, ad esempio le conferenze pianificate dall'utente. Se non si seleziona questa casella di controllo, vengono spostati sia l'account sia i dati associati.



## Per spostare gli utenti da un pool a un altro mediante un filtro

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  In **Ricerca utente** fare clic su **Cerca** e quindi su **Aggiungi filtro**.

5.  Nei criteri di ricerca selezionare **Pool di registrazione**, **Uguale a**, **FQDN pool** e quindi fare clic su **Trova**.

6.  Scegliere **Sposta tutti gli utenti nel pool** dal menu **Azione**.
    

    > [!NOTE]
    > Quando a un set esistente di utenti viene applicato un filtro, l'opzione <STRONG>Sposta tutti gli utenti nel pool</STRONG> si trova nel contesto di un subset filtrato di utenti, non di <STRONG><EM>tutti</EM></STRONG> i possibili utenti.



7.  In **Sposta utenti** selezionare il pool contenente gli account utente da spostare in **Pool di registrazione di origine**.

8.  In **Pool di registrazione di destinazione** selezionare il pool in cui spostare gli utenti.

9.  (Facoltativo) Se il server o il pool di destinazione non è disponibile, selezionare la casella di controllo **Forza**.
    

    > [!WARNING]
    > Se si seleziona <STRONG>Forza</STRONG>, l'account utente viene spostato, ma i dati utente associati vengono eliminati, ad esempio le conferenze pianificate dall'utente e i contatti. Se non si seleziona questa casella di controllo, vengono spostati sia l'account sia i dati associati.



## Per spostare gli utenti da un pool a un altro mediante Lync Management Shell

1.  A seconda di come vengono eseguiti i comandi di Windows PowerShell, ossia in locale o in remoto, è necessario accedere come membro dei ruoli amministrativi corretti di Lync Server 2013, come indicato di seguito:
    
    1.  Se i comandi vengono eseguiti nel computer locale (ad esempio si accede direttamente a un Front End Server): Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).
    
    2.  Se i comandi vengono eseguiti in remoto in un altro computer (ad esempio si accede a un computer e si eseguono i comandi in remoto da un Front End Server Standard Edition): Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per spostare singoli utenti, utilizzare il cmdlet Move-CsUser come indicato di seguito:
    
        Move-CsUser -Identity "Pilar Ackerman" -Target "pool01.contoso.net"
    
    Dove l'utente da spostare si chiama Luisa Cazzaniga e verrà spostato dal pool principale assegnato al pool pool01.contoso.net

4.  Per spostare un numero elevato di utenti, utilizzare i filtri con il cmdlet **Get-CsUser** e passare il set di utenti risultanti a **Move-CsUser**:
    
        Get-CsUser -Filter {RegistrarPool -eq "CurrentPoolFqdn"} | Move-CsUser -Target "TargetPoolFQDN"
    
    La combinazione dei comandi di **Get-CsUser** e **Move-CsUser** può generare questo risultato:
    
        Get-CsUser -Filter {RegistrarPool -eq "pool02.contoso.net"} | Move-CsUser -Target "pool01.contoso.net"

## Vedere anche

#### Ulteriori risorse

[Modifica delle proprietà degli account utente](lync-server-2013-modifying-user-account-properties.md)

