---
title: "Lync Server 2013: Verificare l'accesso tramite il proxy inverso"
TOCTitle: Verificare l'accesso tramite il proxy inverso
ms:assetid: 3076a786-e022-4d41-91ec-1bf252b2a468
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429697(v=OCS.15)
ms:contentKeyID: 49300079
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare l'accesso tramite il proxy inverso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-29_

Eseguire la procedura seguente per verificare che gli utenti possano accedere alle informazioni nel proxy inverso. Potrebbe essere necessario completare la configurazione del firewall e la configurazione di DNS (Domain Name System) prima che l'accesso funzioni correttamente.

## Per verificare che sia possibile accedere al sito Web tramite Internet

  - Aprire un Web browser, digitare nella barra degli indirizzi gli URL utilizzati dai client per accedere ai file della Rubrica e al sito Web per le conferenze, come indicato di seguito:
    
      - Per il server della Rubrica, digitare un URL simile al seguente: **https:// *FQDNWebfarmesterno* /abs**, dove *FQDNWebfarmesterno* è l'FQDN esterno dei servizi Web esterni che ospita i servizi Rubrica. L'utente deve ricevere una richiesta di verifica HTTP, poiché la sicurezza delle directory nella cartella del server della Rubrica è configurata per l'uso dell'autenticazione di Windows per impostazione predefinita.
    
      - Per le conferenze, digitare un URL simile al seguente: **https:// *FQDNWebfarmesterno* /meet** dove *FQDNWebfarmesterno* è l'FQDN esterno della Web farm che ospita il contenuto delle riunioni. Questo URL dovrebbe visualizzare la pagina di risoluzione dei problemi per le conferenze. In alternativa, confermare che l'URL semplice per le funzioni di conferenza funzioni correttamente. Un URL semplice di esempio per la partecipazione alla conferenza può essere https://meet.contoso.com
    
      - Per l'espansione dei gruppi di distribuzione, digitare un URL simile al seguente: **https:// *FQDNWebfarmesterno* /GroupExpansion/service.svc**. L'utente dovrebbe ricevere una richiesta di verifica HTTP, poiché la sicurezza delle directory nel servizio di espansione dei gruppi di distribuzione è configurata per l'utilizzo dell'autenticazione di Windows per impostazione predefinita.
    
      - Per l'accesso remoto, digitare l'URL semplice come in questo esempio: **https:// *FQDNWebfarmesterno* /dialin** dove *FQDNWebfarmesterno* è l'FQDN esterno della Web farm che ospita la pagina di accesso per la conferenza telefonica con accesso remoto. L'utente deve essere indirizzato alla pagina di accesso remoto. In alternativa, confermare che l'URL semplice per l'accesso remoto funzioni correttamente. Un URL semplice di esempio per l'accesso remoto può essere https://dialin.contoso.com
    
      - Per verificare che l'URL di individuazione automatica funzioni, digitare https://lyncdiscover. *externaldomainFQDN* . Il browser richiederà all'utente di aprire un file. Selezionare Blocco note per aprirlo. Una risposta tipica risulterebbe simile a quella riportata di seguito:
        
            {"AccessLocation":"External","Root":{"Links":[{"href":"https:\/\/extweb.contoso.com\/Autodiscover\/AutodiscoverService.svc\/root\/domain","token":"Domain"},
            {"href":"https:\/\/extweb.contoso.com\/Autodiscover\/AutodiscoverService.svc\/root\/user","token":"User"},
            {"href":"https:\/\/lyncweb.contoso.com\/Autodiscover\/AutodiscoverService.svc\/root\/oauth\/user","token":"OAuth"}]}}

