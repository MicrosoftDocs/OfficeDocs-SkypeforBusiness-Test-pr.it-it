---
title: Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013
TOCTitle: Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013
ms:assetid: 22dec3cc-4b6b-4df2-b269-5b35df4731a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ660292(v=OCS.15)
ms:contentKeyID: 49887477
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-13_

Le comunicazioni audio/video (A/V) sono un componente chiave di Microsoft Lync Server 2013. Funzionalità quali la condivisione di applicazioni e le audio e videoconferenze si basano sui certificati assegnati al servizio A/V Edge, in particolare al servizio di autenticazione A/V.

> [!IMPORTANT]  
> <ol>
> 
> <li><p>Questa nuova funzionalità è progettata per il certificato del servizio A/V Edge e <em>OAuthTokenIssuer</em>. È possibile fornire altri tipi di certificati con il servizio A/V Edge e il tipo di certificato OAuth, ma essi non potranno sfruttare il comportamento di coesistenza come il certificato del servizio A/V Edge.</p></li>
> 
> 
> <li><p>I cmdlet Lync Server Management Shell PowerShell utilizzati per gestire i certificati di Microsoft Lync Server 2013 fanno riferimento al certificato del servizio A/V Edge come tipo di certificato <em>AudioVideoAuthentication</em> e al certificato OAuthServer come tipo <em>OAuthTokenIssuer</em>. Per identificare in modo univoco i certificati e nel resto dell'argomento, si farà riferimento a questi certificati con lo stesso tipo di identificatore, <em>AudioVideoAuthentication</em> e <em>OAuthTokenIssuer</em>.</p></li></ol>


Il servizio di autenticazione A/V è responsabile dell'emissione di token utilizzati dai client e altri consumer A/V. I token vengono generati da attributi sul certificato e la scadenza del certificato ha come conseguenza la perdita di connessione e il requisito di partecipare di nuovo con un nuovo token generato dal nuovo certificato. Questo problema viene alleviato grazie a una nuova funzionalità di Lync Server 2013: la possibilità di gestire temporaneamente un nuovo certificato prima della scadenza di quello vecchio e consentire a entrambi di continuare a funzionare per un periodo di tempo. Questa funzionalità utilizza la funzionalità aggiornata nel cmdlet di Lync Server Management Shell Set-CsCertificate. Il nuovo parametro -Roll, con il parametro esistente -EffectiveDate, collocherà il nuovo certificato AudioVideoAuthentication nell'archivio certificati. Il vecchio certificato AudioVideoAuthentication rimane disponibile per la convalida dei token emessi. Con l'attivazione del nuovo certificato AudioVideoAuthentication si verificano gli eventi seguenti:

> [!tip]  
> Utilizzando i cmdlet di Lync Server Management Shell per gestire i certificati, è possibile richiedere certificati separati e distinti per ogni scopo nel server perimetrale. La Creazione guidata certificati nella Distribuzione guidata di Lync Server è utile per creare certificati, ma si tratta in genere del tipo <strong>predefinito</strong> che associa tutti gli utilizzi dei certificati per il server perimetrale in un singolo certificato. Se si intende utilizzare la funzionalità di certificati in sequenza, la procedura consigliata consiste nel disassociare il certificato AudioVideoAuthentication dagli scopi degli altri certificati. È possibile effettuare il provisioning e gestire temporaneamente un certificato di tipo predefinito, ma solo la parte AudioVideoAuthentication del certificato combinato sfrutterà i vantaggi della gestione temporanea. Ad esempio, un utente che partecipa a una conversazione di messaggistica istantanea, alla scadenza del certificato dovrà disconnettersi e riconnettersi per utilizzare il nuovo certificato associato al servizio Access Edge. Un comportamento analogo si ha nel caso di un utente che partecipa a una conferenza Web utilizzando il servizio Web Conferencing Edge. Il certificato OAuthTokenIssuer è un tipo specifico condiviso in tutti i server. Il certificato viene creato e gestito in una sola posizione ed è archiviato nell'archivio di gestione centrale per tutti i server.

Per comprendere appieno le opzioni e i requisiti relativi all'uso del cmdlet Set-CsCertificate e alla gestione temporanea di certificati tramite tale cmdlet prima della scadenza del certificato corrente, sono necessarie altre informazioni. Il parametro -Roll è importante, ma ha essenzialmente un solo scopo. Se viene definito come parametro, si segnala a Set-CsCertificate che verranno fornite informazioni sul certificato interessato definite da -Type (ad esempio AudioVideoAuthentication e OAuthTokenIssuer), quando il certificato diventerà effettivo in base alla definizione di -EffectiveDate.

**-Roll:** il parametro -Roll è obbligatorio e dispone di dipendenze che devono essere fornite con esso. Parametri obbligatori per definire completamente quali certificati saranno interessati e come saranno applicati:

**-EffectiveDate:** il parametro -EffectiveDate definisce quando il nuovo certificato sarà -attivo insieme al certificato corrente. Il parametro -EffectiveDate può essere vicino all'ora di scadenza del certificato corrente oppure corrispondere a un periodo di tempo più lungo. Un valore minimo consigliato per -EffectiveDate per il certificato AudioVideoAuthentication è di 8 ore, ovvero la durata predefinita del token per i token del servizio A/V Edge emessi utilizzando il certificato AudioVideoAuthentication.

Quando si gestiscono temporaneamente certificati OAuthTokenIssuer, esistono diversi requisiti per il tempo di anticipo prima che il certificato diventi effettivo. Il tempo di anticipo minimo per il certificato OAuthTokenIssuer è di 24 ore prima dell'ora di scadenza del certificato corrente. Il tempo di anticipo prolungato per la coesistenza è dovuto ad altri ruoli del server dipendenti dal certificato OAuthTokenIssuer (ad esempio Exchange Server) che ha un periodo di memorizzazione più lungo per i materiali di autenticazione e chiave di crittografia creati dal certificato.

**-Thumbprint:** l'identificazione digitale è un attributo univoco per il relativo certificato. Il parametro -Thumbprint è utilizzato per identificare il certificato che sarà interessato dalle azioni del cmdlet Set-CsCertificate.

**-Type:** il parametro -Type può accettare un tipo di utilizzo a singolo certificato o un elenco separato da virgola di tipi di utilizzo di certificati. I tipi di certificati identificato lo scopo del certificato per il cmdlet e il server. Ad esempio, il tipo AudioVideoAuthentication è destinato a essere utilizzato dal servizio A/V Edge e dal servizio di autenticazione A/V. Se si decide di gestire temporaneamente ed effettuare il provisioning di certificati di un tipo diverso contemporaneamente, è necessario considerare il più lungo tempo di anticipo effettivo minimo richiesto per i certificati. Ad esempio, è necessario gestire temporaneamente i certificati di tipo AudioVideoAuthentication e OAuthTokenIssuer. Il valore minimo di -EffectiveDate deve essere il maggiore dei due certificati, in questo caso OAuthTokenIssuer, che ha un tempo di anticipo di almeno 24 ore. Se non si desidera gestire temporaneamente il certificato AudioVideoAuthentication con un tempo di anticipo di 24 ore, gestirlo separatamente con un valore di EffectiveDate più adeguato ai requisiti specifici.

## Per aggiornare o rinnovare un certificato servizio A/V Edge con parametri -Roll e -EffectiveDate

1.  Accedere al computer locale come membro del gruppo Administrators.

2.  Richiedere un rinnovo o un nuovo certificato AudioVideoAuthentication con chiave privata esportabile per il certificato esistente nel servizio A/V Edge.

3.  Importare il nuovo certificato AudioVideoAuthentication nel server perimetrale e in tutti gli altri server perimetrale nel pool (se è presente un pool distribuito).

4.  Configurare il certificato importato con il cmdlet Set-CsCertificate e utilizzare il parametro -Roll con il parametro -EffectiveDate. La data effettiva deve essere definita come ora di scadenza del certificato corrente (14:00:00 o 2:00:00 PM) meno la durata del token (otto ore per impostazione predefinita). Ciò definisce un'ora in cui impostare il certificato come attivo, che corrisponde a -EffectiveDate \<string\>: “7/22/2012 6:00:00 AM”.
    
    > [!IMPORTANT]  
    > Per un pool di server perimetrali, è necessario avere effettuato la distribuzione e il provisioning di tutti i certificati AudioVideoAuthentication entro la data e l'ora definite dal parametro -EffectiveDate del primo certificato distribuito per evitare possibili interruzioni delle comunicazioni A/V a causa della scadenza di un certificato più vecchio prima del rinnovo di tutti i token client e consumer tramite il nuovo certificato.    
    Comando Set-CsCertificate con i parametri -Roll e -EffectiveTime:
    
        Set-CsCertificate -Type AudioVideoAuthentication -Thumbprint <thumb print of new certificate> -Roll -EffectiveDate <date and time for certificate to become active>
    
    Esempio di comando Set-CsCertificate:
    
        Set-CsCertificate -Type AudioVideoAuthentication -Thumbprint "B142918E463981A76503828BB1278391B716280987B" -Roll -EffectiveDate "7/22/2012 6:00:00 AM"
    
    > [!IMPORTANT]  
    > È necessario formattare il parametro EffectiveDate secondo le impostazioni di lingua e paese del server. Nell'esempio vengono utilizzate le impostazioni di paese e lingua Inglese (Stati Uniti).

Per capire meglio il processo utilizzato da Set-CsCertificate, -Roll e -EffectiveDate per gestire temporaneamente un nuovo certificato per l'emissione di nuovi token AudioVideoAuthentication pur continuando a utilizzare un certificato esistente per convalidare token AudioVideoAuthentication utilizzati dai consumer, è utile servirsi di una sequenza temporale visiva.

Nell'esempio seguente, l'amministratore determina che il certificato del servizio A/V Edge scadrà alle 14.00 del 22/07/2012. Richiede e riceve un nuovo certificato e lo importa in ciascun server perimetrale del pool. Alle 2.00 del 22/07/2012 inizia a eseguire Get-CsCertificate con -Roll, -Thumbprint equivalente alla stringa di identificatore digitale del nuovo certificato e -EffectiveTime impostato su 22/07/2012 6.00. Esegue il comando in ogni server perimetrale.

![Uso dei parametri Roll ed EffectiveDate.](images/JJ660292.21d51a76-0d03-4ed7-a37e-a7c14940265f(OCS.15).jpg "Uso dei parametri Roll ed EffectiveDate.")

All'ora effettiva (6.00 del 22/7/2012), tutti i nuovi token vengono emessi dal nuovo certificato. Alla convalida, i token verranno prima convalidati rispetto al nuovo certificato e, in caso di esito negativo, verrà effettuato un tentativo con il vecchio certificato. Questo processo che prevede prima l'uso del nuovo certificato e del vecchio certificato come fallback viene ripetuto fino alla scadenza del vecchio certificato. Una volta scaduto il vecchio certificato (22/7/2012 alle 14.00), i token verranno convalidati solo mediante il nuovo certificato. Il vecchio certificato potrà essere rimosso senza problemi utilizzando il cmdlet Remove-CsCertificate con il parametro -Previous.

    Remove-CsCertificate -Type AudioVideoAuthentication -Previous

## Per aggiornare o rinnovare un certificato OAuthTokenIssuer con parametri -Roll e -EffectiveDate

1.  Accedere al computer locale come membro del gruppo Administrators.

2.  Richiedere un rinnovo o un nuovo certificato OAuthTokenIssuer con chiave privata esportabile per il certificato esistente nel servizio A/V Edge.

3.  Importare il nuovo certificato OAuthTokenIssuer in un Front End Server nel pool (se è presente un pool distribuito). Il certificato OAuthTokenIssuer viene replicato globalmente e deve solo essere aggiornato e rinnovato in ogni server nella distribuzione. Il Front End Server viene utilizzato come esempio.

4.  Configurare il certificato importato con il cmdlet Set-CsCertificate e utilizzare il parametro -Roll con il parametro -EffectiveDate. La data effettiva deve essere definita come ora di scadenza del certificato corrente (14:00:00 o 2:00:00 PM) meno un minimo di 24 ore.
    
    Comando Set-CsCertificate con i parametri -Roll e -EffectiveTime:
    
        Set-CsCertificate -Type OAuthTokenIssuer -Thumbprint <thumb print of new certificate> -Roll -EffectiveDate <date and time for certificate to become active>
    
    Esempio di comando Set-CsCertificate:
    
        Set-CsCertificate -Type OAuthTokenIssuer -Thumbprint "B142918E463981A76503828BB1278391B716280987B" -Roll -EffectiveDate "7/21/2012 1:00:00 PM"
    
    > [!IMPORTANT]  
    > È necessario formattare il parametro EffectiveDate secondo le impostazioni di lingua e paese del server. Nell'esempio vengono utilizzate le impostazioni di paese e lingua Inglese (Stati Uniti).

All'ora effettiva (1.00.00 del 21/07/2012), tutti i nuovi token vengono emessi dal nuovo certificato. Alla convalida, i token verranno prima convalidati rispetto al nuovo certificato e, in caso di esito negativo, verrà effettuato un tentativo con il vecchio certificato. Questo processo che prevede prima l'uso del nuovo certificato e del vecchio certificato come fallback viene ripetuto fino alla scadenza del vecchio certificato. Una volta scaduto il vecchio certificato (22/7/2012 alle 14.00), i token verranno convalidati solo mediante il nuovo certificato. Il vecchio certificato potrà essere rimosso senza problemi utilizzando il cmdlet Remove-CsCertificate con il parametro -Previous.

    Remove-CsCertificate -Type OAuthTokenIssuer -Previous

## Vedere anche

#### Concetti

[Pianificare i certificati dei server perimetrali in Lync Server 2013](lync-server-2013-plan-for-edge-server-certificates.md)  
[Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)  

#### Ulteriori risorse

[Configurare i certificati perimetrali per Lync Server 2013](lync-server-2013-set-up-edge-certificates.md)  
[Set-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCertificate)  
[Remove-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCertificate)

