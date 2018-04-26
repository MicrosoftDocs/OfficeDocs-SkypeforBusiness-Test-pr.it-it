---
title: 'Lync Server 2013: Failover del pool di server perimetrali utilizzato per la federazione di XMPP'
TOCTitle: Failover del pool di server perimetrali utilizzato per la federazione di XMPP
ms:assetid: 587e7829-a26b-46f8-8aad-b78a7b325b55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688065(v=OCS.15)
ms:contentKeyID: 49887573
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failover del pool di server perimetrali utilizzato per la federazione di XMPP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

All'interno dell'organizzazione un solo pool di server perimetrali è designato come pool da usare per la federazione XMPP. Se questo pool non è disponibile, per consentire il funzionamento della federazione XMPP è necessario eseguire il failover di questa a un altro pool di server perimetrali.

Quando si installano i pool di server perimetrali e si abilita la federazione XMPP per la prima volta, per semplificare il processo di ripristino di emergenza della federazione XMPP è possibile impostare record DNS SRV esterni per tutti i pool di server perimetrali, invece che per uno solo. Per ciascuno di questi record SRV deve essere impostata una priorità diversa. Tutto il traffico di federazione XMPP passa per il pool con il record SRV con la priorità più alta. Per ulteriori informazioni sull'abilitazione e la configurazione della federazione XMPP, vedere [Configurazione della federazione di XMPP in Lync Server 2013](lync-server-2013-setting-up-xmpp-federation.md).

Nella procedura seguente EdgePool1 è il pool di server perimetrali che ospita la federazione XMPP originariamente ed EdgePool2 è il pool che la ospiterà.

## Failover del pool di server perimetrali utilizzato per la federazione di XMPP

1.  Se oltre al pool di server perimetrali non disponibile non ne sono stati distribuiti altri, distribuirne uno. Per informazioni dettagliate, vedere [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md).

2.  In ogni server perimetrale del nuovo pool di server perimetrali che ora ospita la federazione XMPP (EdgePool2) eseguire il cmdlet seguente:
    
        Stop-CsWindowsService

3.  Eseguire il cmdlet seguente per puntare la route della federazione XMPP a EdgePool2:
    
        Set-CsSite Site2 -XmppExternalFederationRoute EdgeServer2.contoso.com
    
    In questo esempio, Site2 è il sito che contiene il pool di server perimetrali che ospiterà la route della federazione XMPP ed EdgeServer2.contoso.com è l'FQDN di un server perimetrale del pool.

4.  Nel server DNS esterno modificare il record A DNS della federazione XMPP in modo che punti a EdgeServer2.contoso.com.

5.  Se non si dispone già di un record SRV DNS per la federazione XMPP che viene risolto nel pool di server perimetrali che ospiterà ora la federazione XMPP, aggiungerlo come indicato nell'esempio seguente. Il valore di porta del record SRV deve essere 5269.
    
        _xmpp-server._tcp.contoso.com

6.  Verificare che la porta 5269 del pool di server perimetrali che ora ospita la federazione XMPP sia aperta esternamente.

7.  Avviare i servizi in tutti i server perimetrali del pool che ospiterà la federazione XMPP:
    
        Start-CsWindowsService

