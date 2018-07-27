---
title: Assegnazione di un certificato di autenticazione da server a server a Microsoft Lync Server 2013
TOCTitle: Assegnazione di un certificato di autenticazione da server a server a Microsoft Lync Server 2013
ms:assetid: c7413954-2504-47f4-a073-44548aff1c0c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205253(v=OCS.15)
ms:contentKeyID: 49301914
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnazione di un certificato di autenticazione da server a server a Microsoft Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-24_

Per determinare se è stato già assegnato a Microsoft Lync Server 2013 un certificato di autenticazione da server a server, eseguire il comando seguente da Lync Server 2013 Management Shell:

    Get-CsCertificate -Type OAuthTokenIssuer

Se non vengono restituite informazioni sul certificato, è necessario assegnare un certificato dell'autorità di certificazione token per poter utilizzare l'autenticazione da server a server. Come regola generale, è possibile utilizzare qualsiasi certificato di Lync Server 2013 come certificato OAuthTokenIssuer. Ad esempio, il certificato predefinito di Lync Server 2013 può essere utilizzato anche come certificato OAuthTokenIssuer. È possibile inoltre utilizzare come certificato OAUthTokenIssuer qualsiasi certificato di server Web contenente il nome del dominio SIP nel campo dell'oggetto. I due requisiti principali per il certificato utilizzato per l'autenticazione da server a server sono i seguenti: 1) è necessario configurare lo stesso certificato come certificato OAuthTokenIssuer in tutti i Front End Server e 2) il certificato deve essere almeno di 2048 bit.

Se non si dispone di un certificato da utilizzare per l'autenticazione da server a server, è possibile ottenere un nuovo certificato, importarlo e quindi utilizzarlo per l'autenticazione da server a server. Dopo aver richiesto e ottenuto il nuovo certificato, è possibile accedere a uno dei Front End Server e utilizzare un comando di Windows PowerShell simile al seguente per importare e assegnare il certificato:

    Import-CsCertificate -Identity global -Type OAuthTokenIssuer -Path C:\Certificates\ServerToServerAuth.pfx  -Password "P@ssw0rd"

Nel comando precedente il parametro Path rappresenta il percorso completo del file di certificato e il parametro Password rappresenta la password assegnata al certificato. Questa procedura deve essere eseguita una sola volta. Il servizio di replica di Lync Server creerà quindi automaticamente un insieme di attività pianificate per decrittografare e distribuire il certificato in tutti i Front End Server.

In alternativa, è possibile utilizzare come certificato di autenticazione da server a server un certificato esistente. Come già specificato, è possibile utilizzare a tale scopo il certificato predefinito. La coppia seguente di comandi di Windows PowerShell recupera il valore della proprietà Thumbprint del certificato predefinito e quindi utilizza tale valore per impostare il certificato predefinito come certificato di autenticazione da server a server:

    $x = (Get-CsCertificate -Type Default).Thumbprint
    Set-CsCertificate -Identity global -Type OAuthTokenIssuer -Thumbprint $x

Nel comando precedente il certificato recuperato viene configurato in modo da funzionare come certificato di autenticazione da server a server globale. In questo modo il certificato verrà replicato in tutti i Front End Server e da essi utilizzato. Come già specificato, questo comando deve essere eseguito una sola volta e solo in un Front End Server. Anche se tutti i Front End Server devono utilizzare lo stesso certificato, non è necessario configurare il certificato OAuthTokenIssuer in ognuno di essi. Sarà sufficiente configurarlo una volta e quindi il server di replica di Lync Server lo copierà in ogni server.

Il cmdlet Set-CsCertificate configura immediatamente il certificato in questione come certificato OAuthTokenIssuer corrente. Tenere presente che in Lync Server 2013 vengono mantenute due copie di un tipo di certificato: il certificato corrente e il certificato precedente. Se si desidera utilizzare immediatamente il nuovo certificato come certificato OAuthTokenIssuer, utilizzare il cmdlet Set-CsCertificate.

È inoltre possibile utilizzare il cmdlet Set-CsCertificate per distribuire un nuovo certificato, ovvero configurare un nuovo certificato in modo che diventi il certificato OAuthTokenIssuer corrente in un determinato momento. Il comando seguente ad esempio recupera il certificato predefinito e quindi lo configura in modo che subentri come certificato OAuthTokenIssuer corrente a partire dal 1° luglio 2012:

    $x = (Get-CsCertificate -Type Default).Thumbprint
    Set-CsCertificate -Identity global -Type OAuthTokenIssuer -Thumbprint $x -EffectiveDate "7/1/2012" -Roll

Il 1° luglio 2012 il nuovo certificato verrà configurato come certificato OAuthTokenIssuer corrente e il certificato OAuthTokenIssuer attivo fino a quel momento verrà configurato come certificato precedente.

Se non si desidera utilizzare Windows PowerShell, è possibile utilizzare la console MMC Certificati per esportare un certificato da un Front End Server e quindi importarlo in tutti gli altri Front End Server. Se si sceglie questa soluzione, esportare la chiave privata insieme al certificato.

> [!CAUTION]  
> In questo caso, la procedura deve essere eseguita in ogni Front End Server. Se infatti si esportano e si importano certificati procedendo in questo modo, Lync Server 2013 non replicherà il certificato in ogni Front End Server.

Dopo aver importato il certificato in tutti i Front End Server, è possibile assegnarlo utilizzando la Distribuzione guidata di Lync Server anziché Windows PowerShell. Per assegnare un certificato utilizzando la Distribuzione guidata, eseguire le operazioni seguenti in un computer in cui è stata installata la Distribuzione guidata:

1.  Fare clic sul pulsante Start, scegliere Tutti i programmi, **Microsoft Lync Server 2013** e quindi **Distribuzione guidata di Lync Server**.

2.  Nella Distribuzione guidata fare clic su **Installa o aggiorna il sistema Lync Server**.

3.  Nella pagina Microsoft Lync Server 2013 fare clic su **Esegui** al di sotto dell'intestazione **Passaggio 3: Richiesta, installazione o assegnazione dei certificati**. Nota: se nel computer sono stati già installati certificati, anziché il pulsante **Esegui** sarà disponibile il pulsante **Riesegui**.

4.  Nella Configurazione guidata certificati selezionare il certificato **OAuthTokenIssuer** e quindi fare clic su **Assegna certificato**.

5.  Nella pagina **Assegnazione certificato** della procedura guidata Assegnazione certificato fare clic su **Avanti**.

6.  Nella pagina **Archivio certificati** selezionare il certificato da utilizzare per l'autenticazione da server a server e quindi fare clic su **Avanti**.

7.  Nella pagina Riepilogo assegnazione certificato fare clic su **Avanti**.

8.  Nella pagina Esecuzione comandi in corso fare clic su **Fine**.

9.  Chiudere la Creazione guidata certificati e la Distribuzione guidata.

