---
title: 'Lync Server 2013: Acquisizione di una posizione'
TOCTitle: Acquisizione di una posizione
ms:assetid: 9bf069aa-d240-4d95-be3a-e795537f8e70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205110(v=OCS.15)
ms:contentKeyID: 49301443
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Acquisizione di una posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-06_

In una distribuzione E9-1-1 di Lync Server 2013 ogni client Lync o Lync Phone Edition connesso internamente acquisisce la propria posizione. Dopo la registrazione SIP, il client fornisce tutte le informazioni sulla connettività di rete note in una richiesta di posizione al servizio Informazioni percorso, ovvero un servizio Web supportato da un database di SQL Server replicato. Ogni pool di siti centrale dispone di un servizio Informazioni percorso, che usa le informazioni di rete per eseguire una query sui record per individuare la posizione. Se viene rilevata una corrispondenza, il servizio Informazioni percorso restituisce una posizione al client. Se non esiste alcuna corrispondenza, all'utente può essere richiesto di immettere una posizione manualmente (a seconda delle impostazioni dei criteri di posizione). I dati sulla posizione vengono ritrasmessi al client in un formato XML standardizzato IETF (Internet Engineering Task Force) denominato Presence Information Data Format Location Object (PIDF-LO).

Il client Lync Server include i dati PIDF-LO come parte di una chiamata di emergenza e questi dati vengono usati dal provider del servizio E9-1-1 per determinare il PSAP appropriato e instrada la chiamata al PSAP insieme all'ESQK corretto, il che consente al dispatcher PSAP di ottenere la posizione del chiamante.

Nel diagramma seguente viene illustrato come un client Lync Server acquisisce una posizione (ad eccezione del metodo di posizione basato sull'indirizzo MAC di client di terze parti):

![Diagramma della modalità con cui il client acquisisce una posizione](images/JJ205110.4438f5fc-f1b2-444b-8565-09035363ed43(OCS.15).jpg "Diagramma della modalità con cui il client acquisisce una posizione")

Affinché un client possa acquisire una posizione, devono essere effettuati i passaggi seguenti:

1.  L'amministratore popola il database del servizio Informazioni percorso con la wiremap di rete (tabelle che mappano vari tipi di indirizzi di rete agli ERL corrispondenti).

2.  Se si usa un provider di servizi E9-1-1 del trunk SIP, l'amministratore convalida le parti dell'indirizzo civico dell'ERL rispetto al database MSAG (Master Street Address Guide) mantenuto dal provider del servizio E9-1-1. Se si usa un gateway ELIN, l'amministratore assicura che l'operatore PSTN carichi gli ELIN nel database Automatic Location Identification (ALI).

3.  Durante la registrazione o in caso di un qualsiasi cambiamento della rete, un client connesso internamente invia una richiesta di posizione contenente gli indirizzi di rete individuati del clienti al servizio Informazioni percorso.

4.  Il servizio Informazioni percorso esegue query sui record pubblicati per un percorso e, se viene individuata una corrispondenza, restituisce l'ERL al client in formato PIDF-LO.

