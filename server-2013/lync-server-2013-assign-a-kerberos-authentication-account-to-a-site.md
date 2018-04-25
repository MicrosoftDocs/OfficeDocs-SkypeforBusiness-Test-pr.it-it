---
title: 'Lync Server 2013: Assegnare un account di autenticazione Kerberos a un sito'
TOCTitle: Assegnare un account di autenticazione Kerberos a un sito
ms:assetid: 3d9c587c-c8b8-4f81-8ed9-1458a31fc292
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425901(v=OCS.15)
ms:contentKeyID: 49300288
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare un account di autenticazione Kerberos a un sito in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-16_

Per eseguire correttamente questa procedura, è necessario essere connessi come utente membro del gruppo RTCUniversalServerAdmins.

Dopo aver creato un account Kerberos, è necessario assegnarlo a un sito. Questo è un sito di Lync Server 2013 e non un sito Active Directory. È possibile creare più account di autenticazione Kerberos per distribuzione, ma è possibile assegnare un solo account a un sito. Utilizzare la procedura seguente per assegnare a un sito un account di autenticazione Kerberos creato precedentemente. Per informazioni dettagliate sulla creazione dell'account Kerberos, vedere [Creare un account di autenticazione Kerberos in Lync Server 2013](lync-server-2013-create-a-kerberos-authentication-account.md).

## Per assegnare un account di autenticazione Kerberos a un sito

1.  Come membro del gruppo RTCUniversalServerAdmins, accedere a un computer nel dominio che esegue Lync Server 2013 oppure a un computer in cui sono installati gli strumenti di amministrazione.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire i due comandi seguenti dalla riga di comando:
    
        New-CsKerberosAccountAssignment -UserAccount "Domain\UserAccount" -Identity "site:SiteName"
    
        Enable-CsTopology
    
    Ad esempio:
    
        New-CsKerberosAccountAssignment -UserAccount "contoso\kerbauth" -Identity "site:redmond"
    
        Enable-CsTopology
    

    > [!NOTE]
    > È necessario specificare il parametro UserAccount utilizzando il formato Dominio\Utente. Il formato Utente@Dominio.estensione non è supportato per fare riferimento agli oggetti computer creati per l'autenticazione Kerberos.

    
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

