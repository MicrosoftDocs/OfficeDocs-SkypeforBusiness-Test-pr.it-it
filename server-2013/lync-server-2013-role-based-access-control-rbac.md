---
title: Controllo degli accessi in base al ruolo (RBAC) per Lync Server 2013
TOCTitle: Controllo degli accessi in base al ruolo (RBAC) per Lync Server 2013
ms:assetid: d01fba36-eb7e-4de9-9bba-5102ae157820
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481134(v=OCS.15)
ms:contentKeyID: 59679245
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Controllo degli accessi in base al ruolo (RBAC) per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

Microsoft Lync Server 2013 include gruppi di controllo degli accessi in base al ruolo (RBAC) per consentire all'utente di delegare attività amministrative mantenendo standard di sicurezza elevati. Tali gruppi vengono creati durante la preparazione della foresta. Per informazioni dettagliate sulla preparazione della foresta, vedere [Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-active-directory-domain-services-for-lync-server.md). Per informazioni dettagliate su specifici gruppi creati nella preparazione della foresta, vedere [Modifiche apportate durante la preparazione della foresta in Lync Server 2013](lync-server-2013-changes-made-by-forest-preparation.md) nella documentazione relativa alla distribuzione.

Con RBAC, i privilegi amministrativi vengono concessi assegnando agli utenti ruoli amministrativi predefiniti, inclusi gli 11 ruoli predefiniti che coprono la maggior parte delle attività amministrative. Ciascun ruolo è associato a un elenco specifico di cmdlet di Lync Server Management Shell che gli utenti in tale ruolo sono autorizzati a eseguire. È possibile utilizzare RBAC per seguire il principio dei "privilegi minimi", in base al quale agli utenti vengono concessi solo i diritti amministrativi necessari per svolgere le proprie mansioni. Per informazioni dettagliate, vedere [Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013](lync-server-2013-planning-for-role-based-access-control.md) nella documentazione relativa alla pianificazione.

