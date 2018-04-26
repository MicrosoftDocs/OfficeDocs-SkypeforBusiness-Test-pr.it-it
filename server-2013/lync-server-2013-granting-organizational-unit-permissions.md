---
title: 'Lync Server 2013: Concessioni di autorizzazioni per unità organizzative'
TOCTitle: Concessioni di autorizzazioni per unità organizzative
ms:assetid: 95ee5ffa-39b1-4d80-87a2-27bb364f7396
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398763(v=OCS.15)
ms:contentKeyID: 49301375
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Concessioni di autorizzazioni per unità organizzative in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-05-14_

È possibile utilizzare il cmdlet **Grant-CsOuPermission** per concedere autorizzazioni a oggetti in unità organizzative specificate in modo che i membri dei gruppi universali RTC creati con la preparazione della foresta possano accedervi pur non essendo membri del gruppo Domain Admins. Le autorizzazioni aggiunte all'unità organizzativa specificata sono le stesse aggiunte dal cmdlet **Enable-CsAdDomain** ai contenitori di computer e utenti durante la preparazione del dominio.

Utilizzare il cmdlet **Test-CsOuPermission** per verificare le autorizzazioni impostate utilizzando il cmdlet **Grant-CsOuPermission**.

È possibile utilizzare il cmdlet **Revoke-CsOuPermission** per rimuovere le autorizzazioni concesse utilizzando il cmdlet **Grant-CsOuPermission**.

## Per concedere le autorizzazioni unità organizzativa

1.  Accedere a un computer che esegue Lync Server 2013 nel dominio in cui si desidera concedere le autorizzazioni unità organizzativa. Se l'unità organizzativa si trova in un dominio figlio diverso, usare un account membro del gruppo Domain Admins o del gruppo Enterprise Admins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU> [-Domain <Domain FQDN>]
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

## Per verificare le autorizzazioni unità organizzativa

1.  Accedere a un computer che esegue Lync Server 2013 nel dominio in cui si desidera verificare le autorizzazioni unità organizzativa concesse mediante il cmdlet **Grant-CsOuPermission**. Se l'unità organizzativa si trova in un dominio figlio diverso, usare un account membro del gruppo Domain Admins o del gruppo Enterprise Admins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Test-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU> [-Domain <Domain FQDN>]
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

## Per revocare le autorizzazioni unità organizzativa

1.  Accedere a un computer che esegue Lync Server 2013 nel dominio in cui si desidera revocare le autorizzazioni unità organizzativa concesse dal cmdlet **Grant-CsOuPermission**. Se l'unità organizzativa si trova in un dominio figlio diverso, usare un account membro del gruppo Domain Admins o del gruppo Enterprise Admins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Revoke-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU> [-Domain <Domain FQDN>]
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

