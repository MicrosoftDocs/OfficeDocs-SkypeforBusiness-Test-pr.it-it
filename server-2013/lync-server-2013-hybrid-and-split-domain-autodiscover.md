---
title: Distribuzione ibrida e dominio diviso - Individuazione automatica
TOCTitle: Distribuzione ibrida e dominio diviso - Individuazione automatica
ms:assetid: c855bcc5-b656-4d2d-92d6-f016f2797d3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945652(v=OCS.15)
ms:contentKeyID: 52062264
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione ibrida e dominio diviso - Individuazione automatica

 

_**Ultima modifica dell'argomento:** 2013-02-14_

Uno spazio indirizzo SIP condiviso, noto anche come distribuzione di *dominio diviso* o distribuzione *ibrida*, è una configurazione in cui gli utenti sono distribuiti in una distribuzione locale e un ambiente online. Il risultato desiderato è che gli utenti, indipendentemente dalla posizione in cui si trova il server principale (in locale oppure online), accedano alla distribuzione e vengano reindirizzati alla posizione del server principale. A questo scopo, la funzionalità di individuazione automatica di Lync Server 2013 viene utilizzata per reindirizzare gli utenti online alla topologia online. È possibile ottenere questo risultato configurando l'URL del servizio di individuazione automatica mediante Lync Server Management Shell e i cmdlet **Get-CsHostingProvider** e **Set-CsHostingProvider**.

## Mobilità per la distribuzione del dominio diviso

Sarà necessario raccogliere e prendere nota degli attributi distribuiti seguenti:

  - In Lync Server Management Shell digitare
    
        Get-CsHostingProvider

  - Nei risultati, individuare il provider online con l'attributo **ProxyFQDN**. Ad esempio, sipfed.online.lync.com.

  - Prendere nota del valore di ProxyFQDN.

  - Abilitare la federazione nel Pannello di controllo di Lync Server locale, consentendo la federazione con il provider online.

  - Abilitare la federazione per il provider online. Per impostazione predefinita, tutti gli utenti online sono abilitati per la federazione dei domini e possono comunicare con tutti i domini.

  - Se si prevede di definire domini bloccati e consentiti, determinare i domini che verranno esplicitamente consentiti o bloccati.

  - Per la federazione online è necessario pianificare le eccezioni del firewall, i certificati e i record dell'host DNS (A oppure AAAA se si utilizza IPv6). È inoltre necessario configurare i criteri di federazione. Per informazioni dettagliate, vedere [Pianificazione della federazione di Lync Server e Office Communications Server](lync-server-2013-planning-for-lync-server-and-office-communications-server-federation.md).

