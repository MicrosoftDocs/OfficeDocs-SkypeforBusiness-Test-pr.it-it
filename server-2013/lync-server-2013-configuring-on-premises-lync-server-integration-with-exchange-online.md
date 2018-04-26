---
title: "Lync Server 2013: Configurazione dell'integrazione di Lync Server locale con Exchange Online"
TOCTitle: Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online
ms:assetid: 95a20117-2064-43c4-94fe-cac892cadb6f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh533880(v=OCS.15)
ms:contentKeyID: 49301369
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online

 

_**Ultima modifica dell'argomento:** 2014-07-02_

I clienti che utilizzano distribuzioni locali di Lync Server 2013 possono ora configurare l'interoperabilità con Microsoft Outlook Web App in Microsoft Exchange Online in una modalità di distribuzione ibrida. Le funzionalità di interoperabilità includono Single Sign-On e integrazione della messaggistica istantanea e della presenza con l'interfaccia di Outlook Web App. Per abilitare l'integrazione è necessario configurare l' server perimetrale nella distribuzione locale di Lync Server completando le attività seguenti:

  - Configurare uno spazio degli indirizzi SIP condiviso

  - Configurare un provider di hosting nell' server perimetrale

  - Verificare la replica dell' archivio di gestione centrale aggiornato

## Configurare uno spazio degli indirizzi SIP condiviso

Per integrare la distribuzione locale di Lync Server 2013 con Exchange Online è necessario configurare uno spazio degli indirizzi SIP condiviso. Lo stesso spazio degli indirizzi di dominio SIP viene supportato sia da Lync Server che dal servizio Exchange Online.

Utilizzando Lync Server Management Shell, configurare l' server perimetrale per la federazione eseguendo il cmdlet **Set-CSAccessEdgeConfiguration** con i parametri visualizzati nell'esempio seguente:

    Set-CsAccessEdgeConfiguration -AllowFederatedUsers $True

  - Il parametro **AllowFederatedUsers** specifica se gli utenti interni sono autorizzati a comunicare con gli utenti di domini federati. Questa proprietà determina inoltre se gli utenti interni possono comunicare con gli utenti in uno spazio degli indirizzi SIP condiviso con Lync Server ed Exchange Online.

Per informazioni dettagliate sull'utilizzo di Lync Server Management Shell, vedere [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Configurare un provider di hosting nel server perimetrale

Utilizzando Lync Server Management Shell, configurare un provider di hosting nell' server perimetrale eseguendo il cmdlet **New-CsHostingProvider** con i parametri visualizzati nell'esempio seguente:

    New-CsHostingProvider -Identity "Exchange Online" -Enabled $True -EnabledSharedAddressSpace $True -HostsOCSUsers $False -ProxyFqdn "exap.um.outlook.com" -IsLocal $False -VerificationLevel UseSourceVerification


> [!NOTE]
> Se si utilizza Office 365 gestito tramite 21Vianet in Cina, sostituire il valore del parametro <STRONG>ProxyFqdn</STRONG> in questo esempio ("exap.um.outlook.com") con il nome di dominio completo del servizio gestito da 21Vianet: "exap.um.partner.outlook.cn".



  - **Identity** specifica un identificatore di valore stringa univoco per il provider di hosting che si sta creando, ad esempio "Exchange Online". I valori che contengono spazi devono essere racchiusi tra virgolette doppie.

  - **Enabled** indica se la connessione di rete tra il dominio e il provider di hosting è abilitata. Deve essere impostato su True.

  - **EnabledSharedAddressSpace** indica se il provider di hosting verrà utilizzato in uno scenario di spazio degli indirizzi SIP condiviso. Deve essere impostato su True.

  - **HostsOCSUsers** indica se il provider di hosting viene utilizzato per ospitare Office Communications Server o Lync Server. Deve essere impostato su False.

  - **ProxyFQDN** specifica il nome di dominio completo (FQDN) del server proxy utilizzato dal provider di hosting. Per Exchange Online, l'FQDN è exap.um.outlook.com.

  - **IsLocal** indica se il server proxy utilizzato dal provider di hosting è contenuto nella topologia di Lync Server. Deve essere impostato su False.

  - **VerificationLevel** indica il livello di verifica consentito per i messaggi inviati da e verso il provider ospitato. Specificare **UseSourceVerification**, che dipende dal livello di verifica incluso nei messaggi inviati dal provider di hosting. Se il livello non è specificato, il messaggio verrà rifiutato in quanto non verificabile.

## Verificare la replica dell'archivio di gestione centrale aggiornato

Le modifiche apportate utilizzando i cmdlet nelle sezioni precedenti vengono applicate automaticamente all' server perimetrale e in genere la replica richiede meno di un minuto. È possibile convalidare lo stato di replica e quindi confermare che tutte le modifiche siano state applicate all' server perimetrale utilizzando i cmdlet seguenti.

Per verificare gli aggiornamenti della replica, in un server della distribuzione di Lync Server eseguire il cmdlet seguente:

    Get-CsManagementStoreReplicationStatus

Per confermare l'applicazione delle modifiche, nel server perimetrale eseguire il cmdlet seguente:

    Get-CsHostingProvider -LocalStore

## Vedere anche

#### Ulteriori risorse

[Fornire agli utenti di Lync Server 2013 la segreteria telefonica nella messaggistica unificata di Exchange ospitata](lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md)  
[Integrazione della messaggistica unificata di Exchange ospitata in Lync Server 2013](lync-server-2013-hosted-exchange-unified-messaging-integration.md)

