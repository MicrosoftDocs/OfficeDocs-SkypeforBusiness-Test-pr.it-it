---
title: 'Lync Server 2013: Preparazione dei domini'
TOCTitle: Preparazione dei domini
ms:assetid: 8eea541c-5f9d-4afc-92a8-a31d6f742544
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398721(v=OCS.15)
ms:contentKeyID: 49301298
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione dei domini per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

La preparazione del dominio è l'ultima operazione per la preparazione di Servizi di dominio Active Directory per Lync Server 2013. Questa operazione comporta l'aggiunta delle voci di controllo di accesso necessarie ai gruppi universali che concedono autorizzazioni per ospitare e gestire gli utenti nell'ambito del dominio. Con la preparazione del dominio vengono create voci di controllo di accesso nella radice del dominio e tre contenitori predefiniti degli utenti, dei computer e dei controller di dominio.

È possibile eseguire la preparazione del dominio in qualsiasi computer presente nel dominio in cui viene distribuito Lync Server. È necessario preparare qualsiasi dominio che ospiterà Lync Server o utenti.

Se l'ereditarietà delle autorizzazioni è disabilitata o le autorizzazioni degli utenti autenticati sono disabilitate nell'organizzazione, durante la preparazione del dominio sono necessari alcuni passaggi aggiuntivi. Per informazioni dettagliate, vedere [Preparazione di un ambiente Servizi di dominio Active Directory bloccato in Lync Server 2013](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md).

Se nell'organizzazione vengono utilizzate unità organizzative anziché i tre contenitori predefiniti, ovvero Utenti, Computer e Controller di dominio, sarà necessario concedere al gruppo Authenticated Users l'accesso in lettura alle unità organizzative. L'accesso in lettura ai contenitori è necessario per la preparazione del dominio. Se il gruppo Utenti autenticati non dispone di accesso in lettura all'unità organizzativa, eseguire il cmdlet **Grant-CsOuPermission** come illustrato negli esempi di codice seguenti per concedere l'autorizzazione di lettura per ogni unità organizzativa.

    Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU > 

    Grant-CsOuPermission -ObjectType "user","contact",inetOrgPerson" -OU "ou=Redmond,dc=contoso,dc=net"

Per informazioni dettagliate sul cmdlet **Grant-CsOuPermission**, vedere la documentazione relativa a Lync Server Management Shell.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per ulteriori informazioni sulle voci di controllo di accesso create nella radice del dominio e nei contenitori degli utenti, dei computer e dei controller di dominio, vedere <a href="lync-server-2013-changes-made-by-domain-preparation.md">Modifiche apportate durante la preparazione del dominio in Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Esecuzione della preparazione del dominio per Lync Server 2013](lync-server-2013-running-domain-preparation.md)

  - [Utilizzo di cmdlet per ripristinare la preparazione del dominio per Lync Server 2013](lync-server-2013-using-cmdlets-to-reverse-domain-preparation.md)

