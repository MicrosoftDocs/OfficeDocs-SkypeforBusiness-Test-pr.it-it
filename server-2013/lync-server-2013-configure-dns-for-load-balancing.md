---
title: 'Lync Server 2013: Configurare DNS per il bilanciamento del carico'
TOCTitle: Configurare DNS per il bilanciamento del carico
ms:assetid: 1b2e8414-8676-4872-8ecf-ea07196f74de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398251(v=OCS.15)
ms:contentKeyID: 49299840
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare DNS per il bilanciamento del carico in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per eseguire correttamente questa procedura, è necessario connettersi al server o al dominio almeno come membro del gruppo Domain Admins o DnsAdmins.

Il bilanciamento del carico DNS (Domain Name System) consente di bilanciare il traffico di rete specifico di Lync Server 2013, ad esempio il traffico SIP e il traffico multimediale. Il bilanciamento del carico DNS è supportato per pool Front End, pool di server perimetrali, pool di server Director e pool Mediation Server autonomi. Per un pool configurato per l'utilizzo del bilanciamento del carico DNS devono essere definiti due nomi di dominio completi (FQDN), ovvero il normale FQDN del pool che viene utilizzato dal bilanciamento del carico DNS (ad esempio, pool1.contoso.com) e che viene risolto negli indirizzi IP fisici dei server del pool e un altro FQDN per i servizi Web del pool (ad esempio, web1.contoso.net) che viene risolto nell'indirizzo IP virtuale del pool. Per informazioni dettagliate sul bilanciamento del carico DNS, vedere [Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md) nella documentazione relativa alla pianificazione.


> [!NOTE]
> Per il traffico HTTPS da client a server è ancora necessario utilizzare il bilanciamento del carico hardware.



Prima di poter utilizzare il bilanciamento del carico DNS, è necessario eseguire le operazioni seguenti:

1.  Sostituire l'FQDN del pool dei servizi Web interni.
    

    > [!WARNING]
    > Se si decide di forzare i Servizi Web interni con un FQDN personalizzato, ogni FQDN deve essere diverso da quello di tutti gli altri pool Front End, Server Director o pool di server Director.



2.  Creare record host A DNS per risolvere l'FQDN del pool negli indirizzi IP di tutti i server inclusi nel pool.

3.  Abilitare la sequenza casuale degli indirizzi IP oppure, per DNS di Windows Server, abilitare il round robin.
    

    > [!NOTE]
    > Il round robin è abilitato per impostazione predefinita.



## Per sostituire l'FQDN dei servizi Web interni

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console espandere il nodo Pool Enterprise Edition Front End.

3.  Fare clic con il pulsante destro del mouse sul pool, scegliere **Modifica proprietà** e quindi fare clic su **Servizi Web** .

4.  Sotto **Servizi Web interni** selezionare la casella di controllo **Sostituisci FQDN** .

5.  Digitare l'FQDN del pool che viene risolto negli indirizzi IP fisici dei server del pool.

6.  Sotto **Servizi Web esterni** digitare l'FQDN del pool esterno che viene risolto negli indirizzi IP virtuali del pool e quindi fare clic su **OK** .

7.  Nell'albero della console fare clic su **Lync Server 2013** e quindi nel riquadro **Azioni** fare clic su **Pubblica topologia** .

## Per creare i record host (A) DNS per tutti i server del pool interno

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **DNS** .

2.  In **Gestore DNS** fare clic sul server DNS che gestisce i record per espanderlo.

3.  Fare clic sulla voce **Zone di ricerca diretta** per espanderla.

4.  Fare clic con il pulsante destro del mouse sul dominio DNS a cui aggiungere i record e quindi scegliere **Nuovo host (A o AAAA)** .

5.  Nella casella **Nome** digitare il nome del record host. Il nome del dominio verrà aggiunto automaticamente.

6.  Nella casella Indirizzo IP digitare l'indirizzo IP del singolo Front End Server e quindi selezionare **Crea record puntatore (PTR) associato** o **Consenti a tutti gli utenti autenticati di aggiornare i record DNS con lo stesso nome proprietario** , se applicabile.

7.  Continuare a creare i record per tutti i Front End Server membri che parteciperanno al bilanciamento del carico DNS.
    
    Se ad esempio si dispone di un pool denominato pool1.contoso.com e di tre Front End Server, sarà necessario creare le voci DNS seguenti:
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>FQDN</th>
    <th>Tipo</th>
    <th>Dati</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Pool1.contoso.com</p></td>
    <td><p>Host (A)</p></td>
    <td><p>192.168.1.1</p></td>
    </tr>
    <tr class="even">
    <td><p>Pool1.contoso.com</p></td>
    <td><p>Host (A)</p></td>
    <td><p>192.168.1.2</p></td>
    </tr>
    <tr class="odd">
    <td><p>Pool1.contoso.com</p></td>
    <td><p>Host (A)</p></td>
    <td><p>192.168.1.3</p></td>
    </tr>
    </tbody>
    </table>
    
    Per informazioni dettagliate sulla creazione di record host (A) DNS, vedere [Configurare i record host DNS per Lync Server 2013](lync-server-2013-configure-dns-host-records.md).

## Per abilitare il round robin per Windows Server

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **DNS** .

2.  Espandere **DNS** , fare clic con il pulsante destro del mouse sul server DNS che si desidera configurare e quindi scegliere **Proprietà** .

3.  Fare clic sulla scheda **Avanzate** , selezionare **Attiva round robin** e **Attiva ordinamento netmask** e quindi fare clic su **OK** .
    
    ![Finestra di dialogo del round robin DNS](images/Gg398251.e7bf6125-8d78-4460-8401-0a8e7e21d305(OCS.15).jpg "Finestra di dialogo del round robin DNS")


> [!NOTE]
> Questa funzionalità è abilitata per impostazione predefinita.



## Vedere anche

#### Concetti

[Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md)

