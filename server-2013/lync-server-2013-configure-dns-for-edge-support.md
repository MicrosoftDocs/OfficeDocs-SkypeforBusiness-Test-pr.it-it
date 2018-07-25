---
title: 'Lync Server 2013: Configurare DNS per il supporto dei componenti perimetrali'
TOCTitle: Configurare DNS per il supporto dei componenti perimetrali
ms:assetid: 955493e6-aa29-424d-bb81-1ef87b3b15e3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398756(v=OCS.15)
ms:contentKeyID: 49301365
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare DNS per il supporto dei componenti perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-15_

È necessario configurare record DNS (Domain Name System) per le interfacce perimetrali interne ed esterne, incluse le interfacce di server perimetrali e proxy inversi. Per impostazione predefinita, i server perimetrali non sono connessi a un dominio e non hanno quindi un nome di dominio completo. Al server perimetrale si fa riferimento solo in base al nome breve (computer) non con un nome di dominio completo. Tuttavia, Generatore di topologie usa gli FQDN e non i nomi brevi. Il nome del server perimetrale deve corrispondere all'FQDN usato da Generatore di topologie. A tale scopo, si definisce un suffisso che in combinazione con il nome del computer produca l'FQDN previsto. Usare la procedura descritta in “Per aggiungere il suffisso DNS al nome computer in server perimetrale non connesso a un dominio” per aggiungere il suffisso DNS al nome computer.


> [!NOTE]
> Per impostazione predefinita, DNS utilizza un algoritmo roundrobin per ruotare l'ordine dei dati di record di risorse restituiti in risposte di query in cui esistono più record di risorse dello stesso tipo per un nome di dominio DNS sottoposto a query. Il bilanciamento del carico DNS di Lync Server 2013 dipende da questo meccanismo. Verificare che questa impostazione non sia stata disabilitata. Se si utilizza un server DNS che non esegue un sistema operativo Windows, verificare che sia abilitato l'ordinamento di record di risorse round robin.



Usare le procedure seguenti in "**Per creare un record DNS SRV**” per creare e verificare ogni record DNS SRV. Usare la procedura in "**Per creare un record DNS A**" per definire i record DNS A necessari per l'accesso degli utenti esterni. Per verificare che i record siano stati configurati e funzionino correttamente, vedere "**Per verificare un record DNS**" in questo argomento. Per informazioni dettagliate su ogni record necessario per supportare l'accesso esterno, vedere [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

## Per aggiungere un suffisso DNS al nome del computer in un server perimetrale che non fa parte di un dominio

1.  Nel computer fare clic sul pulsante **Start** , fare clic con il pulsante destro del mouse su **Computer** e quindi scegliere **Proprietà** .

2.  In **Impostazioni relative a nome computer, dominio e gruppo di lavoro** fare clic su **Cambia impostazioni** .

3.  Nella scheda **Nome computer** fare clic su **Cambia** .

4.  In **Cambiamenti dominio/nome computer** fare clic su **Altro** .

5.  In **Suffisso DNS e nome NetBIOS del computer** digitare il nome del dominio interno (ad esempio corp.contoso.com) in **Suffisso DNS primario del computer** e quindi fare clic su **OK** tre volte.

6.  Riavviare il computer.

## Per creare un record SRV DNS

1.  Nel server DNS appropriato fare clic sul pulsante **Start** , scegliere **Pannello di controllo** , **Strumenti di amministrazione** e quindi **DNS** .
    
    > [!important]  
    > È necessario configurare DNS in modo che siano presenti le voci seguenti: 1) voci DNS esterne per ricerche DNS esterne da parte di utenti remoti e partner federati, 2) voci per ricerche DNS che devono essere utilizzate dai server perimetrali nella rete perimetrale (nota anche come DMZ e subnet schermata), inclusi i record A per i server interni che eseguono Lync Server 2013 e 3) voci DNS interne per ricerche da parte di client e server interni che eseguono Lync Server 2013.

2.  Nell'albero della console del dominio SIP espandere **Zone di ricerca diretta** e quindi fare clic con il pulsante destro del mouse sul dominio in cui è installato Lync Server 2013.

3.  Fare clic su **Altri nuovi record** .

4.  In **Selezionare tipo di record di risorsa** digitare **Posizione servizio (SRV)** e quindi su fare clic su **Crea record** .

5.  Specificare tutte le informazioni necessarie per il record SRV DNS.

## Per creare un record A DNS

1.  Nel server DNS fare clic sul pulsante **Start** , scegliere **Pannello di controllo** , **Strumenti di amministrazione** e quindi **DNS** .

2.  Nell'albero della console del dominio SIP espandere **Zone di ricerca diretta** e quindi fare clic con il pulsante destro del mouse sul dominio in cui è installato Lync Server 2013.

3.  Scegliere **Nuovo host (A o AAAA)** .

4.  Specificare tutte le informazioni necessarie per il record SRV DNS.

## Per verificare un record DNS

1.  Eseguire l'accesso a un computer client nel dominio.

2.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui** .

3.  Eseguire il comando seguente al prompt:
    
        nslookup <FQDN edge interface>

4.  Verificare di ricevere una risposta che si risolve nell'indirizzo IP appropriato per l'FQDN.

## Vedere anche

#### Attività

[Creare un Record DNS SRV per l'integrazione con la messaggistica unificata di Exchange ospitata](lync-server-2013-create-a-dns-srv-record-for-integration-with-hosted-exchange-um.md)  

#### Concetti

[Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)

