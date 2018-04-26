---
title: Rimuovere il database di SQL Server per un server di archiviazione
TOCTitle: Rimuovere il database di SQL Server per un server di archiviazione
ms:assetid: 6e8a1fcd-ed09-43b0-82c9-60e7ce116a01
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688087(v=OCS.15)
ms:contentKeyID: 49887602
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere il database di SQL Server per un server di archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Dopo aver rimosso un server di archiviazioneMicrosoft Lync Server 2010, è possibile rimuovere i database di SQL Server che ospitavano i dati del pool. Utilizzare le procedure seguenti per rimuovere le definizioni da Generatore di topologie e quindi rimuovere i file di database e di registro dal server di database.

## Per rimuovere il database di SQL Server mediante Generatore di topologie

1.  Nel Front End Server di Lync Server 2013 aprire Generatore di topologie.

2.  In Generatore di topologie passare a **Componenti condivisi** e quindi ad **Archivi SQL Server**, fare clic con il pulsante destro del mouse sull'istanza di SQL Server associata al server di archiviazione rimosso o riconfigurato e quindi scegliere **Elimina**.

3.  Pubblicare la topologia e quindi verificare lo stato della replica.

## Per rimuovere i file di database da SQL Server

1.  Per rimuovere i database in SQL Server, è necessario essere un membro del gruppo sysadmins di SQL Server per il server SQL Server in cui si desidera rimuovere i file di database.

2.  Aprire Lync Server Management Shell.

3.  Nella riga di comando digitare quanto segue:
    
        Uninstall-CsDataBase -DatabaseType Archiving -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    Dove *\<FQDN\>* è il nome di dominio completo (FQDN) del server di database e *\<instance\>* è l'istanza di database denominata, se ne è stata definita una.

4.  Quando il cmdlet **Uninstall-CsDataBase** richiede di confermare le azioni, leggere le informazioni, quindi premere **S** (o premere Invio) per continuare oppure premere **N** , quindi Invio se si desidera interrompere il cmdlet, ad esempio in caso di errori.

