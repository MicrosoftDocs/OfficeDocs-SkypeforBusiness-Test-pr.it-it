---
title: 'Lync Server 2013: Sincronizzare la password di un account di autenticazione Kerberos con IIS'
TOCTitle: Sincronizzare la password di un account di autenticazione Kerberos con IIS
ms:assetid: 05925a66-2684-4c1b-adfa-69bd0da1bf38
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398107(v=OCS.15)
ms:contentKeyID: 49299558
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sincronizzare la password di un account di autenticazione Kerberos con IIS in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2010-11-08_

Per eseguire correttamente questa procedura, è necessario essere connessi come utente membro del gruppo RTCUniversalServerAdmins.

In un sito i Front End Server, i server Standard Edition e i Director possono utilizzare un account di autenticazione Kerberos per autenticare le richieste inviate ai servizi Web. Questa procedura consente di individuare ogni server che esegue i servizi Web in un sito a cui sia stato assegnato un account Kerberos e di aggiornare le impostazioni di configurazione di Internet Information Services (IIS) per l'utilizzo di tale account. Per informazioni dettagliate, vedere [Impostare la password di un account di autenticazione Kerberos in un server in Lync Server 2013](lync-server-2013-set-a-kerberos-authentication-account-password-on-a-server.md).

## Per impostare e configurare una password per l'account di autenticazione Kerberos

1.  Eseguire l'accesso a un computer di origine, ad esempio fe01.contoso.com, come membri del gruppo RTCUniversalServerAdmins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Dalla riga di comando di Lync Server Management Shell eseguire i due comandi seguenti:
    
        Set-CsKerberosAccountPassword -FromComputer SourceComputer -ToComputer DestinationComputer
    
    Ad esempio:
    
        Set-CsKerberosAccountPassword -FromComputer fe01.contoso.com -ToComputer dir01.contoso.com
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il nome del computer di origine e del computer di destinazione deve essere un nome di dominio completo (FQDN) del server. Non è possibile utilizzare l'FQDN del pool, a meno che il nome del pool non corrisponda al nome del computer utilizzato come origine o destinazione.</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Dopo aver apportato le necessarie modifiche all'autenticazione Kerberos, ad esempio l'aggiunta o la rimozione di un account, è necessario eseguire <strong>Enable-CsTopology</strong> dal prompt dei comandi di Lync Server Management Shell.</td>
    </tr>
    </tbody>
    </table>

