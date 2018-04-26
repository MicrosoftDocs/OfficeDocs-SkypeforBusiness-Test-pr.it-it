---
title: Configurare il supporto della federazione per un dominio di Lync Online
TOCTitle: Configurare il supporto della federazione per un dominio di Lync Online
ms:assetid: 19d5d5be-cd7f-47b8-b6c5-651a3191def7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202166(v=OCS.15)
ms:contentKeyID: 49299832
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il supporto della federazione per un dominio di Lync Online

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per attuare una federazione con un cliente di Microsoft Lync Online 2010, è necessario eseguire le operazioni seguenti:

  - Configurare il supporto per il dominio del cliente di Lync Online 2010, ad esempio contoso.onmicrosoft.com. Come spiegato nella sezione [Prerequisiti per la federazione con un cliente di Lync Online](lync-server-2013-prerequisites-for-federating-with-a-lync-online-customer.md) di questa documentazione, la federazione deve già essere stata abilitata per l'organizzazione. Se si abilita la federazione, è necessario specificare il metodo da utilizzare per controllare l'accesso da parte dei domini federati. Se l'organizzazione è stata configurata in modo da utilizzare l'individuazione, l'aggiunta del dominio all'elenco dei domini consentiti dell'organizzazione è facoltativa. Se l'individuazione dei domini non è stata abilitata, sarà necessario aggiungere il nome del dominio del cliente di Lync Online a tale elenco. È possibile aggiungere un nome di dominio utilizzando il Pannello di controllo di Lync Server o eseguendo il cmdlet **New-CSAllowedDomain**. Per informazioni dettagliate sull'utilizzo del Pannello di controllo di Lync Server, inclusa l'abilitazione dell'individuazione dei domini, vedere [Gestire i provider federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-providers-for-your-organization.md) nella documentazione relativa alle operazioni. Per informazioni dettagliate sull'utilizzo del cmdlet **New-CSAllowedDomain** per l'aggiunta di un dominio, vedere [New-CsAllowedDomain](new-csalloweddomain.md) nella documentazione relativa alle operazioni.
    

    > [!NOTE]
    > Un cliente di Lync Online può disporre di più domini. Se si intende attuare la federazione con più di un dominio, sarà necessario configurare il supporto per ogni dominio con il quale si desidera supportare la federazione e l'amministratore del cliente di Lync Online dovrà abilitare la federazione per tutti i domini interessati.



  - Configurare il supporto per il provider di hosting del dominio del cliente di Lync Online 2010 con cui attuare la federazione. Utilizzare la procedura disponibile in questa sezione per configurare il supporto per tale provider.
    

    > [!NOTE]
    > Questo passaggio è necessario solo per la federazione con dominio di un cliente di Lync Online, non per la federazione con un dominio distribuito in locale nella posizione di un partner federato.



## Per configurare il supporto per un provider di hosting

1.  Da un Front End Server, Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet **New-CsHostingProvider** per creare e configurare il provider di hosting. Ad esempio, eseguire quanto segue:
    
        New-CsHostingProvider -Identity LyncOnline -ProxyFqdn "sipfed.online.lync.com" -VerificationLevel UseSourceVerification -Enabled $True -EnabledSharedAddressSpace $False -HostsOCSUsers $False -IsLocal $False
    
    Nell'esempio precedente vengono impostati i parametri seguenti:
    
      - **Identity** specifica un identificatore di valore stringa univoco per il provider di hosting che si sta creando. Il comando avrà esito negativo se è stato già configurato un provider esistente con lo stesso valore di Identity.
    
      - **ProxyFQDN** specifica il nome di dominio completo (FQDN) del server proxy utilizzato dal provider di hosting. Questo valore non può essere modificato. Se il provider di hosting cambia server proxy, sarà necessario eliminare e quindi ricreare la voce per il provider.
    
      - **VerificationLevel** specifica come o se i messaggi inviati da un provider di hosting devono essere verificati per accertare che provengano effettivamente da quel provider.
    
      - **Enabled** indica se la connessione di rete fra il proprio dominio e il provider di hosting è abilitata. Finché il valore non viene impostato su **True**, le due organizzazioni non potranno scambiarsi messaggi.
    
      - **EnabledSharedAddressSpace** indica se il provider di hosting viene utilizzato in uno scenario di spazio degli indirizzi SIP condiviso (dominio diviso).
    
      - **HostsOCSUsers** indica se il provider di hosting viene utilizzato per ospitare account di Lync Server. Se è impostato su **False**, il provider ospita altri tipi di account, ad esempio account di Microsoft Exchange.
    
      - **IsLocal** indica se il server proxy utilizzato dal provider di hosting è contenuto all'interno della topologia di Lync Server.
    
    Per informazioni dettagliate sull'utilizzo di questo cmdlet, vedere [New-CsHostingProvider](new-cshostingprovider.md) nella documentazione relativa alle operazioni.

