---
title: Eseguire la migrazione degli utenti di Lync Online a Lync in locale
TOCTitle: Eseguire la migrazione degli utenti di Lync Online a Lync in locale
ms:assetid: 0e29605b-db2d-4cbf-b6a9-15db6b9fdabc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn689115(v=OCS.15)
ms:contentKeyID: 62247331
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione degli utenti di Lync Online a Lync in locale

 

_**Ultima modifica dell'argomento:** 2015-03-09_

> [!IMPORTANT]  
> Questi passaggi sono necessari solo per la migrazione di account utente abilitati originariamente per Lync in Lync Online, prima della distribuzione di Lync in locale. Per spostare gli utenti abilitati originariamente per Lync in locale e spostati in un secondo momento in Lync Online, vedere <a href="lync-server-2013-administering-users-in-a-hybrid-deployment.md">Amministrazione degli utenti in una distribuzione ibrida di Lync Server 2013</a>.<br />Inoltre, è necessario che tutti gli utenti da spostare dispongano di account nell'Active Directory locale.

## Migrazione di utenti abilitati originariamente in Lync Online a Lync in locale

1.  Per prima cosa, assicurarsi che l'organizzazione sia configurata per la distribuzione ibrida.
    
      - Installare lo Strumento di sincronizzazione di Microsoft Azure Active Directory. Per ulteriori informazioni, vedere <http://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool.aspx>.
    
      - Per consentire agli utenti di utilizzare l'accesso Single Sign-On per Lync Online, installare Active Directory Federation Services <http://social.technet.microsoft.com/wiki/contents/articles/1011.active-directory-federation-services-ad-fs-overview.aspx>.
    
      - Nella distribuzione locale, in Lync Server Management Shell, digitare i seguenti cmdlet per creare il provider di hosting per Lync Online:
        
        ```
        Set-CSAccessEdgeConfiguration -AllowOutsideUsers 1 -AllowFederatedUsers 1 -UseDnsSrvRouting -EnablePartnerDiscovery $true
        ```
        ```
        New-CSHostingProvider -Identity LyncOnline -Name LyncOnlin -ProxyFqdn "sipfed.online.lync.com" -Enabled $true -EnabledSharedAddressSpace $true -HostsOCSUsers $true -VerificationLevel UseSourceVerification -IsLocal $false -AutodiscoverUrl https://webdir.online.lync.com/Autodiscover/AutodiscoverService.svc/root
        ```

2.  Verificare che nei server perimetrali locali sia presente la catena di certificati che consente la connessione a Lync Online, come mostrato nella tabella seguente. È possibile eseguire il download della catena qui: [https://corp.sts.microsoft.com/Onboard/ADFS\_Onboarding\_Pack/corp\_sts\_certs.zip](https://corp.sts.microsoft.com/onboard/adfs_onboarding_pack/corp_sts_certs.zip) .
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Certificato</th>
    <th>Archivio certificati</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Baltimore CyberTrust Root</p></td>
    <td><p>CA radice attendibile</p></td>
    </tr>
    <tr class="even">
    <td><p>Microsoft Internet Authority (nuovo certificato CA)</p></td>
    <td><p>CA intermedia</p></td>
    </tr>
    <tr class="odd">
    <td><p>MSIT Machine Auth CA2 (nuova CA2 emittente)</p></td>
    <td><p>CA intermedia</p></td>
    </tr>
    </tbody>
    </table>


3.  Nell'Active Directory locale, abilitare gli account utente interessati per Lync in locale. È possibile eseguire questa operazione per un singolo utente digitando il seguente cmdlet:
    
        Enable-CsUser
        -Identity "username" 
        -SipAddress "sip: username@contoso.com"
        -HostingProviderProxyFqdn "sipfed.online.lync.com"
    
    Oppure è possibile creare uno script in grado di leggere i nomi utente da un file e utilizzarli come input per il cmdlet Enable-CsUser:
    
        Enable-CsUser
        -Identity $Identity 
        -SipAddress $SipAddress 
        -HostingProviderProxyFqdn "sipfed.online.lync.com"

4.  Eseguire DirSync per sincronizzare gli utenti di Lync Online con gli utenti aggiornati di Lync in locale.

5.  Aggiornare alcuni record DNS per indirizzare tutto il traffico SIP a Lync in locale:
    
      - Aggiornare il record A **lyncdiscover.contoso.com** in modo che punti all'FQDN del server proxy inverso locale.
    
      - Aggiornare il record SRV ***\_sip*.\_tls.contoso.com** in modo che venga risolto nell'indirizzo VIP o IP pubblico del servizio Access Edge di Lync in locale.
    
      - Aggiornare il record SRV ***\_sipfederationtls*.\_tcp.contoso.com** in modo che venga risolto nell'indirizzo VIP o IP pubblico del servizio Access Edge di Lync in locale.
    
      - Se l'organizzazione utilizza DNS suddivisi (a volte definiti DNS di tipo split brain), assicurarsi che gli utenti che risolvono i nomi attraverso la zona DNS interna vengano indirizzati al pool Front End.

6.  Digitare il cmdlet `Get-CsUser` per controllare alcune proprietà relative agli utenti da spostare. È necessario assicurarsi che HostingProviderProxyFQDN sia impostato su `"sipfed.online.lync.com"` e che gli indirizzi SIP siano configurati correttamente.

7.  Spostare gli utenti di Lync Online a Lync in locale.
    
    Per spostare un singolo utente, digitare:
    
    ```
    $cred = Get-Credential
    ```
    ```
    Move-CsUser -Identity <username>@contoso.com -Target "<fe-pool>.contoso.com" -Credential $cred -HostedMigrationOverrideURL <URL>
    ```
    
    È possibile spostare più utenti tramite il cmdlet **Get-CsUSer** con il parametro –Filter per selezionare gli utenti con una proprietà specifica. Ad esempio, è possibile selezionare tutti gli utenti di Lync Online applicando un filtro basato su {Hosting Provider –eq “sipfed.online.lync.om”}. È quindi possibile inviare gli utenti restituiti al cmdlet **Move-CsUSer**, come mostrato di seguito.
    
        Get-CsUser -Filter {Hosting Provider -eq "sipfed.online.lync.com"} | Move-CsUser -Target "<fe-pool>.contoso.com" -Credential $creds -HostedMigrationOverrideURL <URL>
    
    Il formato dell'URL specificato per il parametro **HostedMigrationOverrideUrl** deve essere l'URL del pool in cui è in esecuzione il servizio di migrazione ospitata, nel formato seguente: *Https://\<FQDN pool\>/HostedMigration/hostedmigrationService.svc*.
    
    È possibile determinare l'URL del servizio di migrazione ospitata visualizzando l'URL del Pannello di controllo di Lync Online per l'account del tenant Office 365.
    
    ## Per determinare l'URL del servizio di migrazione ospitata per il tenant Office 365
    
    1.  Accedere al tenant Office 365 come amministratore.
    
    2.  Aprire l'**Interfaccia di amministrazione di Lync**.
    
    3.  Con l'**Interfaccia di amministrazione di Lync** visualizzata, selezionare e copiare l'URL nella barra degli indirizzi fino a **lync.com**. L'URL è simile a quello seguente:
        
        `https://webdir0a.online.lync.com/lscp/?language=en-US&tenantID=`
    
    4.  Sostituire **webdir** nell'URL con **admin**. Si otterrà quanto segue:
        
        `https://admin0a.online.lync.com`
    
    5.  Aggiungere la stringa seguente all'URL: **/HostedMigration/hostedmigrationservice.svc**.
        
        L'URL risultante, che corrisponde al valore di **HostedMigrationOverrideUrl**, è simile al seguente:
        
        `https://admin0a.online.lync.com/HostedMigration/hostedmigrationservice.svc`
    

    > [!NOTE]
    > La dimensione massima predefinita per i file di log delle transazioni del database rtcxds è 16 GB. Questa dimensione potrebbe non essere sufficiente se si sta spostando un numero elevato di utenti contemporaneamente, soprattutto se il mirroring è abilitato. Per risolvere questo problema, è possibile aumentare la dimensione dei file oppure eseguire regolarmente il backup dei file di log. Per ulteriori informazioni, vedere <A class=uri href="http://support.microsoft.com/kb/2756725">http://support.microsoft.com/kb/2756725</A>.



8.  Questo passaggio è facoltativo. Se è necessario effettuare l'integrazione con Exchange 2013 Online, è necessario utilizzare un provider di hosting aggiuntivo. Per informazioni dettagliate, vedere [Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online](lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md).

9.  Gli utenti sono stati spostati. Per controllare che un utente presenti i valori corretti per gli attributi visualizzati nella seguente tabella, digitare questo cmdlet:
    
        Get-CsUser | fl DisplayName,HostingProvider,SipAddress,Enabled
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Attributo di Active Directory</th>
    <th>Nome attributo</th>
    <th>Valore corretto per l'utente di Lync Online</th>
    <th>Valore corretto per gli utenti di Lync in locale</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>msRTCSIP-DeploymentLocator</p></td>
    <td><p>HostingProvider</p></td>
    <td><p>sipfed.online.lync.com</p></td>
    <td><p>SRV:</p></td>
    </tr>
    <tr class="even">
    <td><p>msRTCSIP-PrimaryUserAddress</p></td>
    <td><p>SIPAddress</p></td>
    <td><p>sip:userName@contoso.com</p></td>
    <td><p>sip:userName@contoso.com</p></td>
    </tr>
    <tr class="odd">
    <td><p>sRTCSIP-UserEnabled</p></td>
    <td><p>Enabled</p></td>
    <td><p>True</p></td>
    <td><p>True</p></td>
    </tr>
    </tbody>
    </table>


10. Ogni utente spostato dovrà disconnettersi da Lync, quindi dovrà effettuare nuovamente l'accesso. All'accesso, è necessario che gli utenti verifichino i propri elenchi contatti e aggiungano i contatti, se necessario.
    
    Tenere presente che per le riunioni pianificate non viene eseguita la migrazione da Lync Online a Lync in locale. Gli utenti dovranno pianificare nuovamente tali riunioni dopo lo spostamento.
    
    Dopo aver aggiornato i record DNS e aver indirizzato tutti gli utenti a Lync in locale, l'attributo HostingProvider indirizza l'utente di Lync all'utilizzo dei record SRV oppure al provider di Lync Online “sipfed.online.lync.com.”

