---
title: 'Lync Server 2013: Preparazione dello schema di Active Directory'
TOCTitle: Preparazione dello schema di Active Directory
ms:assetid: 067726ae-fd3f-4133-a32f-26d2603ac674
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398119(v=OCS.15)
ms:contentKeyID: 49299561
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione dello schema di Active Directory in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-27_

Prima di iniziare a preparare Servizi di dominio Active Directory, è possibile aprire i file di schema mediante un editor di testo, quale ad esempio il Blocco note Windows, o vedere [Estensioni dello schema, classi e attributi di Active Directory utilizzati da Lync Server 2013](lync-server-2013-active-directory-schema-extensions-classes-and-attributes-used-by-lync-server.md) per informarsi su tutte le estensioni dello schema di Servizi di dominio Active Directory che verranno modificate per Lync Server 2013. Lync Server utilizza quattro file di schema:

  - ExternalSchema.ldf, utilizzato per l'interoperabilità con Microsoft Exchange Server

  - ServerSchema.ldf, che è il file di schema di Lync Server 2013 principale

  - BackCompatSchema.ldf, utilizzato per l'interoperabilità con gli eventuali componenti di versioni precedenti

  - VersionSchema.ldf, utilizzato per le informazioni sulla versione dello schema preparato

Tutti i file con estensione ldf vengono installati durante la preparazione dello schema, indipendentemente dal fatto che si stia eseguendo la migrazione da una versione precedente o eseguendo un'installazione pulita. Questi file di schema vengono installati nella stessa sequenza con cui sono riportati nell'elenco precedente e sono disponibili nella cartella \\Support\\schema del supporto di installazione.

Le estensioni dello schema di Lync Server vengono replicate in tutti i domini, con un impatto significativo sul traffico di rete. Eseguire la preparazione dello schema in un momento di scarso utilizzo della rete.


> [!NOTE]
> Se è necessario aggiungere il supporto dei client mobili Microsoft® Office Communicator Mobile 2007 R2 per Java e Microsoft® Office Communicator Mobile per Nokia 1.0 alla distribuzione di Lync Server 2013, preparare lo schema di Active Directory per Microsoft Office Communications Server 2007 R2 durante l'installazione di Lync Server 2013. Per il software e la documentazione necessari, vedere la pagina Web all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=207172">http://go.microsoft.com/fwlink/p/?linkId=207172</A>.



## ADSI Edit

Active Directory Service Interfaces Editor (ADSI Edit) è uno strumento di amministrazione di Servizi di dominio Active Directory che consente di verificare la preparazione e la replica dello schema.

ADSI Edit viene installato per impostazione predefinita quando si installa il ruolo Servizi di dominio Active Directory per impostare un server come controller di dominio. Per Windows Server 2008 e Windows Server 2008 R2, ADSI Edit (adsiedit.msc) è incluso in Strumenti di amministrazione remota del server. È inoltre possibile installare Strumenti di amministrazione remota del server in server membri del dominio o in server autonomi. Il pacchetto di Strumenti di amministrazione remota del server viene copiato in tali server per impostazione predefinita durante l'installazione di Windows, ma non viene installato per impostazione predefinita. Per installare i singoli strumenti, utilizzare Server Manager. È possibile accedere ad ADSI Edit da **Strumenti di amministrazione ruoli** , **Strumenti per Servizi di dominio Active Directory** , **Strumenti di Controller di dominio Active Directory** .

Per Windows Server 2003, ADSI Edit è incluso negli Strumenti di supporto, disponibili nella cartella \\SUPPORT\\TOOLS del CD di Windows Server 2003 oppure scaricabili dalla pagina Web "Strumenti di supporto a 32 bit di Windows Server 2003 Service Pack 2" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=125770](http://go.microsoft.com/fwlink/p/?linkid=125770). Le istruzioni per l'installazione degli Strumenti di supporto dal CD del prodotto sono disponibili nella pagina Web "Installare gli Strumenti di supporto di Windows" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=125771](http://go.microsoft.com/fwlink/p/?linkid=125771). Adsiedit.dll viene registrato automaticamente quando si installano gli strumenti di supporto. Se invece i file sono stati copiati nel computer, è necessario eseguire il comando **regsvr32** per registrare il file adsiedit.dll prima che sia possibile eseguire lo strumento.

## Contenuto della sezione

  - [Esecuzione della preparazione dello schema in Lync Server 2013](lync-server-2013-running-schema-preparation.md)

  - [Verifica della replica dello schema in Lync Server 2013](lync-server-2013-verifying-schema-replication.md)

## Vedere anche

#### Ulteriori risorse

[Preparazione della foresta per Lync Server 2013](lync-server-2013-preparing-the-forest.md)  
[Preparazione dei domini per Lync Server 2013](lync-server-2013-preparing-domains.md)

