---
title: 'Lync Server 2013: Concessione di autorizzazioni di installazione'
TOCTitle: Concessione di autorizzazioni di installazione
ms:assetid: 15982bfe-6844-44f6-815a-72dcaf0e4d21
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398225(v=OCS.15)
ms:contentKeyID: 49299784
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Concessione di autorizzazioni di installazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-27_

È possibile utilizzare il cmdlet **Grant-CsSetupPermission** per aggiungere autorizzazioni Read, Write, ReadSPN e WriteSPN al gruppo RTCUniversalServerAdmins per una determinata unità organizzativa (OU) di Active Directory. I membri del gruppo RTCUniversalServerAdmins dell'unità organizzativa specificata possono quindi installare server Lync Server 2013 nel dominio in questione senza essere membri del gruppo Domain Admins.

Utilizzare il cmdlet **Test-CsSetupPermission** per verificare le autorizzazioni impostate utilizzando il cmdlet **Grant-CsSetupPermission**.

È possibile utilizzare il cmdlet **Revoke-CsSetupPermission** per rimuovere le autorizzazioni concesse utilizzando il cmdlet **Grant-CsSetupPermission**.

## Per concedere autorizzazioni di installazione

1.  Connettersi a un computer che esegue Lync Server 2013 nel dominio in cui si desidera concedere le autorizzazioni di installazione. Utilizzare un account membro del gruppo Domain Admins o del gruppo Enterprise Admins se l'unità organizzativa si trova in un altro dominio figlio.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Grant-CsSetupPermission -ComputerOu <DN of the OU or container where the computer objects that will run Lync Server reside > [-Domain <Domain FQDN>]
    
    È possibile specificare il parametro ComputerOu in base al contesto dei nomi predefinito del dominio specificato, ad esempio CN=computer. In alternativa, è possibile specificare tale parametro come nome distinto (DN) completo dell'unità organizzativa (OU), ad esempio "CN=computer,DC=Contoso,DC=com". In quest'ultimo caso, è necessario specificare un nome distinto dell'unità organizzativa che sia coerente con il dominio specificato.
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

## Per verificare le autorizzazioni di installazione

1.  Connettersi a un computer che esegue Lync Server 2013 nel dominio in cui si desidera verificare le autorizzazioni di installazione concesse mediante il cmdlet **Grant-CsSetupPermission**. Utilizzare un account membro del gruppo Domain Admins o del gruppo Enterprise Admins se l'unità organizzativa si trova in un altro dominio figlio.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Test-CsSetupPermission -ComputerOu <DN of the OU or container where the computer objects that will run Lync Server reside> [-Domain <Domain FQDN>]
    
    È possibile specificare il parametro ComputerOu in base al contesto dei nomi predefinito del dominio specificato, ad esempio CN=computer. In alternativa, è possibile specificare tale parametro come nome distinto (DN) completo dell'unità organizzativa (OU), ad esempio "CN=computer,DC=Contoso,DC=com". In quest'ultimo caso, è necessario specificare un nome distinto dell'unità organizzativa che sia coerente con il dominio specificato.
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

## Per revocare le autorizzazioni di installazione

1.  Eseguire l'accesso a un computer che esegue Lync Server 2013 nel dominio in cui si desidera revocare le autorizzazioni di installazione concesse mediante il cmdlet **Grant-CsSetupPermission**. Utilizzare un account membro del gruppo Domain Admins o del gruppo Enterprise Admins se l'unità organizzativa si trova in un altro dominio figlio.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Revoke-CsSetupPermission -ComputerOu <DN of the OU or container where the computer objects that will run Lync Server reside > [-Domain <Domain FQDN>]
    
    È possibile specificare il parametro ComputerOu in base al contesto dei nomi predefinito del dominio specificato, ad esempio CN=computer. In alternativa, è possibile specificare tale parametro come nome distinto (DN) completo dell'unità organizzativa (OU), ad esempio "CN=computer,DC=Contoso,DC=com". In quest'ultimo caso, è necessario specificare un nome distinto dell'unità organizzativa che sia coerente con il dominio specificato.
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

