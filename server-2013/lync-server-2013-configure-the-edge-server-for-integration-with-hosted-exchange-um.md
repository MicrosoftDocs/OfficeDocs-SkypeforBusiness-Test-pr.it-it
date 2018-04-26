---
title: "Lync Server 2013: Configurare il server perimetrale per l'integrazione con la messaggistica unificata di Exchange ospitata"
TOCTitle: Configurare il server perimetrale per l'integrazione con la messaggistica unificata di Exchange ospitata
ms:assetid: ede3f2f9-f412-418e-a705-8d8ec98176c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399075(v=OCS.15)
ms:contentKeyID: 49302378
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il server perimetrale per l'integrazione con la messaggistica unificata di Exchange ospitata

 

_**Ultima modifica dell'argomento:** 2015-01-23_

Per fornire agli utenti di Lync Server 2013 delle funzionalità di segreteria telefonica nella Messaggistica unificata di Exchange ospitata, è necessario definire la configurazione seguente nel server perimetrale:

  - Configurare il server perimetrale per la federazione.

  - Replicare i dati dell' archivio di gestione centrale nel server perimetrale e verificare la replica.

  - Creare un provider di hosting nel server perimetrale.

Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell relativa a cmdlet seguenti:

  - [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  - [New-CsHostingProvider](new-cshostingprovider.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima di eseguire queste operazioni, è necessario creare un record DNS SRV esterno per il servizio Exchange di hosting. Per informazioni dettagliate, vedere <a href="lync-server-2013-create-a-dns-srv-record-for-integration-with-hosted-exchange-um.md">Creare un Record DNS SRV per l'integrazione con la messaggistica unificata di Exchange ospitata</a>.</td>
</tr>
</tbody>
</table>


## Per configurare il server perimetrale per la federazione

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsAccessEdgeConfiguration per configurare il server per la federazione. Ad esempio, eseguire:
    
        Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -AllowFederatedUsers 1 -EnablePartnerDiscovery 0
    
    Nell'esempio precedente vengono impostati i parametri seguenti:
    
      - **UseDnsSrvRouting** specifica che i server perimetrali si baseranno su record DNS SRV per l'invio e la ricezione di richieste di federazione.
    
      - **AllowFederatedUsers** specifica se agli utenti interni è consentito comunicare con utenti di domini federati. Questa proprietà determina inoltre se gli utenti interni possono comunicare con gli utenti in uno scenario di dominio diviso.
    
      - **EnablePartnerDiscovery** specifica se Lync Server utilizzerà i record DNS per tentare di individuare domini di partner non presenti nell'elenco di domini consentiti di Active Directory. Se False, Lync Server 2013 attuerà la federazione solo con i domini presenti nell'elenco di domini consentiti. Questo parametro è obbligatorio se si utilizza il routing del servizio DNS. Nella maggior parte delle distribuzioni, il valore è impostato su False per impedire di aprire la federazione a tutti i partner.

## Per replicare i dati nel server perimetrale e verificare la replica

  - Verificare che la replica nel server perimetrale sia completa. Per informazioni sulla procedura, vedere [Verificare la connettività tra server interni e server perimetrali in Lync Server 2013](lync-server-2013-verify-connectivity-between-internal-servers-and-edge-servers.md).

## Per creare un provider di hosting nel server perimetrale

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet **New-CsHostingProvider** per configurare il provider di hosting. Ad esempio, eseguire:
    
        New-CsHostingProvider -Identity Fabrikam.com -Enabled $True -EnabledSharedAddressSpace $True -HostsOCSUsers $False -ProxyFQDN "proxyserver.fabrikam.com" -IsLocal $False -VerificationLevel UseSourceVerification
    
    Nell'esempio precedente vengono impostati i parametri seguenti:
    
      - **Identity** specifica un identificatore di valore di stringa univoco per il provider di hosting da creare, in questo esempio **Fabrikam.com** . Si noti che il comando non riesce se è già stato configurato un provider esistente per questo valore Identity.
    
      - **Enabled** indica se la connessione di rete tra il dominio dell'organizzazione e il provider di hosting è abilitata. Finché il valore non verrà impostato su **True** , le due organizzazioni non potranno scambiarsi messaggi.
    
      - **EnabledSharedAddressSpace** indica se il provider di hosting verrà utilizzato in uno scenario con spazio degli indirizzi SIP condiviso (dominio diviso).
        

        > [!NOTE]
        > Prima di impostare <CODE>EnableSharedAddressSpace</CODE> su True, tentare di risolvere internamente il record SRV della federazione. Se non è possibile completare questa operazione, sarà necessario creare i record _sipfederationtls._tcp.&lt;domain&gt; e _sip._tls.&lt;domain&gt; nel DNS interno. Tali record devono fare riferimento all'indirizzo IP esterno di Access Interface del server perimetrale.

    
      - **HostsOCSUsers** indica se il provider di hosting verrà utilizzato per ospitare gli account di Lync Server 2013. Se **False** , il provider ospiterà altri tipi di account, ad esempio quelli di Microsoft Exchange.
    
      - **ProxyFQDN** specifica il nome di dominio completo (FQDN) del server proxy utilizzato dal provider di hosting, in questo esempio **proxyserver.fabrikam.com** . Questo valore non può essere modificato. Se il provider di hosting cambia server proxy è necessario eliminare e ricreare la voce per il provider.
    
      - **IsLocal** indica se il server proxy utilizzato dal provider di hosting è contenuto nella topologia di Lync Server 2013.
    
      - **VerficationLevel** indica il livello di verifica consentito per i messaggi inviati e ricevuti dal provider ospitato. Specificare **UseSourceVerification**, che si basa sul livello di verifica incluso nei messaggi inviati dal provider di hosting. Se il livello non è specificato, il messaggio verrà rifiutato in quanto non verificabile.

## Vedere anche

#### Attività

[Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md)  

#### Concetti

[Verificare la connettività tra server interni e server perimetrali in Lync Server 2013](lync-server-2013-verify-connectivity-between-internal-servers-and-edge-servers.md)  

#### Ulteriori risorse

[New-CsHostingProvider](new-cshostingprovider.md)

