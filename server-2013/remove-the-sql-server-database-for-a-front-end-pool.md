---
title: Rimuovere il database di SQL Server per un pool Front End
TOCTitle: Rimuovere il database di SQL Server per un pool Front End
ms:assetid: 6bb932df-3ed7-49b6-ae17-61e4c6a5fe82
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688084(v=OCS.15)
ms:contentKeyID: 49887597
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere il database di SQL Server per un pool Front End

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Dopo aver rimosso un  pool Front End di Microsoft Lync Server 2010 o aver riconfigurato il pool per l'utilizzo di un database diverso, è possibile rimuovere i database di SQL Server che ospitano i dati del pool. Utilizzare le procedure seguenti per rimuovere le definizioni dal Generatore di topologie e quindi rimuovere il database e il file di registro dal server di database.

## Per rimuovere il database di SQL Server mediante Generatore di topologie

1.  Dal Front End Server di Lync Server 2013, aprire Generatore di topologie e scaricare la topologia esistente.

2.  In Generatore di topologie passare a **Componenti condivisi** e quindi ad **Archivi SQL Server**, fare clic con il pulsante destro del mouse sull'istanza di SQL Server associata al pool Front End rimosso o riconfigurato e quindi scegliere **Elimina**.

3.  Pubblicare la topologia, quindi verificare lo stato della replica.

## Per rimuovere i database degli utenti e delle applicazioni da SQL Server

1.  Per rimuovere i database in SQL Server, è necessario essere un membro del gruppo sysadmins di SQL Server per il server SQL Server in cui si desidera rimuovere i file di database.

2.  Aprire Lync Server Management Shell

3.  Per rimuovere il database dall'archivio utenti del pool, digitare:
    
        Uninstall-CsDataBase -DatabaseType User -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    Dove *\<FQDN\>* è il nome di dominio completo (FQDN) del server di database e *\<instance\>* è l'istanza di database denominata, se ne è stata definita una.

4.  Per rimuovere il database dall'archivio applicazioni del pool, digitare:
    
        Uninstall-CsDataBase -DatabaseType Application -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    Dove *\<FQDN\>* è l'FQDN del server di database e *\<istanza\>* è l'istanza di database denominata, se ne è stata definita una.

5.  Quando il cmdlet **Uninstall-CsDataBase** richiede di confermare le azioni, leggere le informazioni, quindi premere **S** (o premere Invio) per continuare oppure premere **N** , quindi Invio se si desidera interrompere il cmdlet, ad esempio in caso di errori.

