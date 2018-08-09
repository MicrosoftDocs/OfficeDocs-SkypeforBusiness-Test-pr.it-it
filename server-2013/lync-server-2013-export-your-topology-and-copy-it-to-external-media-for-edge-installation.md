---
title: "Lync Server 2013: Esporta/copia topol. su supp. est. per installaz. perimetr."
TOCTitle: Esportare la topologia e copiarla su supporto esterno per l'installazione perimetrale
ms:assetid: def9f416-c519-4a72-b242-7d3057d9c1fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398983(v=OCS.15)
ms:contentKeyID: 49302214
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Dopo la pubblicazione della topologia, la Distribuzione guidata di Lync Server richiede accesso ai dati dell' archivio di gestione centrale per avviare il processo di distribuzione nel server. Nella rete interna i dati sono disponibili direttamente dai server, ma i server perimetrali non inclusi nel dominio interno non possono accedervi. Per rendere disponibili i dati di configurazione della topologia per una distribuzione di server perimetrali, è necessario esportare tali dati in un file da copiare in un supporto esterno, ad esempio un'unità USB o una condivisione di rete disponibile dal server perimetrale, prima di eseguire la Distribuzione guidata di Lync Server nel server perimetrale. Eseguire la procedura seguente per rendere disponibili i dati di configurazione della topologia nel server perimetrale da distribuire.


> [!NOTE]
> Dopo l'installazione di Lync Server 2013 in un server perimetrale, quest'ultimo viene gestito con gli strumenti di amministrazione nella rete interna, che replica automaticamente la configurazione di tutti i server perimetrali nella distribuzione. L'unica eccezione è costituita dalle operazioni di assegnazione e installazione dei certificati, nonché di arresto e avvio dei servizi, operazioni che devono essere entrambe eseguite nel server perimetrale.



## Per rendere disponibili i dati della topologia in un server perimetrale tramite Lync Server Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  In Lync Server Management Shell eseguire il cmdlet seguente:
    
        Export-CsConfiguration -FileName <ConfigurationFilePath.zip>

3.  Copiare il file esportato in un supporto esterno, ad esempio un'unità USB o una condivisione di rete disponibile dal server perimetrale durante la distribuzione.

