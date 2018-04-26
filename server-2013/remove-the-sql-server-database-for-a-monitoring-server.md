---
title: Rimuovere il database di SQL Server per un server Monitoring Server
TOCTitle: Rimuovere il database di SQL Server per un server Monitoring Server
ms:assetid: aed5e394-d63e-4ad4-af40-f12d3a044344
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721848(v=OCS.15)
ms:contentKeyID: 49887706
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere il database di SQL Server per un server Monitoring Server

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Dopo avere rimosso un Monitoring Server di Microsoft Lync Server 2010, è possibile rimuovere i database di SQL Server in cui sono ospitati i dati del server. Utilizzare le procedure seguenti per rimuovere le definizioni da Generatore di topologie e quindi rimuovere i file di log e di database dal server di database.

## Per rimuovere il database di SQL Server mediante Generatore di topologie

1.  Nel Front End Server di Lync Server 2013 aprire Generatore di topologie.

2.  In Generatore di topologie passare a **Componenti condivisi** e quindi ad **Archivi SQL Server** , fare clic con il pulsante destro del mouse sull'istanza di SQL Server associata al Monitoring Server rimosso o riconfigurato e quindi scegliere **Elimina** .

3.  Pubblicare la topologia e quindi verificare lo stato della replica.

## Per rimuovere i file di database da SQL Server

1.  Per rimuovere i database dal server basato su SQL Server, è necessario essere un membro del gruppo sysadmins nel server SQL Server in cui vengono rimossi i file di database.

2.  Aprire Lync Server Management Shell.

3.  Nella riga di comando digitare quanto segue:
    
        Uninstall-CsDataBase -DatabaseType Monitoring -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    Dove *\<FQDN\>* è il nome di dominio completo del server di database e *\<instance\>* è l'istanza di database denominata facoltativa.

4.  Quando il cmdlet **Uninstall-CsDataBase** richiede di confermare le azioni, leggere le informazioni, quindi premere **S** (o premere Invio) per continuare oppure premere **N** , quindi Invio se si desidera interrompere il cmdlet, ad esempio in caso di errori.

