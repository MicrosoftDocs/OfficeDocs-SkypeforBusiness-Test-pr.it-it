---
title: Consentire la federazione con tutti i domini
TOCTitle: Consentire la federazione con tutti i domini
ms:assetid: d26f1057-a76c-447a-9efe-72efdce4c15e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362855(v=OCS.15)
ms:contentKeyID: 56269983
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Consentire la federazione con tutti i domini

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Se si vuole consentire agli utenti dell'organizzazione di comunicare con utenti di qualsiasi altro dominio, è necessario eseguire due operazioni. Come prima cosa, usare il cmdlet [New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md) per creare un'istanza dell'oggetto AllowAllKnownDomains:

    $x = New-CsEdgeAllowAllKnownDomains

Chiamare quindi il cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) e impostare il valore della proprietà AllowedDomains sulla variabile ($x in questo esempio) che contiene l'oggetto AllowAllKnownDomains:

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

