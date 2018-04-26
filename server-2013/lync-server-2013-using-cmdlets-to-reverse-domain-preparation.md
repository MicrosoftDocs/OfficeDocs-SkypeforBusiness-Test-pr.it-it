---
title: 'Lync Server 2013: Utilizzo di cmdlet per ripristinare la preparazione del dominio'
TOCTitle: Utilizzo di cmdlet per ripristinare la preparazione del dominio
ms:assetid: 014dba5d-fcb3-44c9-9d63-ae0755276dac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398071(v=OCS.15)
ms:contentKeyID: 49299486
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di cmdlet per ripristinare la preparazione del dominio per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

Utilizzare il cmdlet **Disable-CsAdDomain** per annullare il passaggio di preparazione di un dominio.

## Per utilizzare i cmdlet per annullare la preparazione di un dominio

1.  Accedere a qualsiasi server del dominio come membro del gruppo Domain Admins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Disable-CsAdDomain [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] 
        [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] 
    
    Ad esempio:
    
        Disable-CsAdDomain -Domain domain1.contoso.net -GlobalSettingsDomainController dc01.domain1.contoso.net -Force
    
    Se il parametro Force è presente, viene eseguito il rollback della preparazione del dominio, anche se sono attivati uno o più Front End Server o A/V Conferencing Server nel dominio. Se il parametro Force non è presente, il rollback della preparazione del dominio verrà interrotto se vengono attivati Front End Server o A/V Conferencing Server nel dominio.
    

    > [!NOTE]
    > Il parametro GlobalSettingsDomainController consente di indicare la posizione in cui sono archiviate le impostazioni globali. Se le impostazioni sono archiviate nel contenitore di sistema (situazione che in genere si verifica con distribuzioni di aggiornamento per le quali non è stata eseguita la migrazione delle impostazioni globali nel contenitore della configurazione), è necessario definire un controller di dominio nella radice della foresta di Active Directory. Se le impostazioni globali sono archiviate nel contenitore della configurazione (situazione che in genere si verifica con le nuove distribuzioni o con distribuzioni di aggiornamento per le quali è stata eseguita la migrazione delle impostazioni nel contenitore della configurazione), è necessario definire qualsiasi controller di dominio nella foresta. Se non si specifica questo parametro, il cmdlet presupporrà che le impostazioni siano archiviate nel contenitore della configurazione e farà riferimento a qualsiasi controller di dominio in AD&nbsp;DS.



## Vedere anche

#### Attività

[Esecuzione della preparazione del dominio per Lync Server 2013](lync-server-2013-running-domain-preparation.md)  

#### Ulteriori risorse

[Preparazione dei domini per Lync Server 2013](lync-server-2013-preparing-domains.md)

