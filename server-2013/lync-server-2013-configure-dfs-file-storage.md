---
title: "Lync Server 2013: Configurare l'archiviazione dei file"
TOCTitle: Configurare l'archiviazione dei file
ms:assetid: a985be20-5a00-4f38-b45b-83dc82de3827
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205150(v=OCS.15)
ms:contentKeyID: 49301608
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare l'archiviazione dei file per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-13_

Lync Server 2013 supporta l'utilizzo di condivisioni file in un file system distribuito (DFS, Distributed File System). Per informazioni dettagliate sul file system DFS per Windows Server 2008, vedere la Guida dettagliata ai file system distribuiti per Windows Server 2008 all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202835](http://go.microsoft.com/fwlink/p/?linkid=202835). Per utilizzare un file system DFS, Lync Server 2013 richiede quanto segue:

  - Gli spazi dei nomi devono essere basati sul dominio.

  - Tutti i server dello spazio dei nomi devono eseguire almeno Windows 2008.

L'installazione di Lync Server 2013 richiede che le autorizzazioni per la cartella condivisa consentano l'accesso completo all'amministratore. Lync Server 2013 quindi utilizzerà le autorizzazioni file NTFS per accedere tramite ACL alle cartelle. Le autorizzazioni di condivisione DFS ereditate non verranno utilizzate per limitare l'accesso.

Per ulteriori informazioni sui requisiti delle condivisioni file, vedere [Supporto dell'archiviazione di file in Lync Server 2013](lync-server-2013-file-storage-support.md) nella documentazione relativa al supporto.

Nella procedura seguente viene illustrato come configurare correttamente le autorizzazioni delle cartelle condivise utilizzando la procedura guidata per lo spazio dei nomi DFS, come descritto nella guida all'installazione di DFS.

## Per configurare le autorizzazioni delle cartelle condivise

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **Gestione DFS** .

2.  Nell'albero della console dello snap-in Gestione DFS fare clic con il pulsante destro del mouse sul server dello spazio dei nomi, ad esempio filesrv1.contoso.com, e quindi scegliere **Modifica impostazioni** .

3.  Selezionare **Autorizzazioni cartella condivisa** .

4.  Selezionare **Usa autorizzazioni personalizzate** .

5.  Per il gruppo degli amministratori, selezionare quanto segue in **Consenti** :
    
      - **Controllo completo**
    
      - **Modifica**
    
      - **Lettura**

6.  Fare clic su **Applica** e quindi su **OK** .

