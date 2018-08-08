---
title: "Lync Server 2013: Configura password degli account di autenticaz. Kerberos"
TOCTitle: Configurazione delle password degli account di autenticazione Kerberos
ms:assetid: b435f88e-4a77-4be7-b7e5-c17484303b74
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412870(v=OCS.15)
ms:contentKeyID: 49301719
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle password degli account di autenticazione Kerberos in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2010-11-03_

Dopo aver creato l'oggetto computer per l'account di autenticazione Kerberos, è possibile configurare la password per l'account. Eseguire il cmdlet Windows PowerShell per impostare la password dell'account Kerberos in un server. È possibile impostare la password nell'oggetto creato per l'autenticazione Kerberos. La password può essere impostata su un valore noto, ma per impostazione predefinita è una password casuale. La password è disponibile per tutte le origini di autenticazione Kerberos che utilizzano l'account. Utilizzare i cmdlet di Windows PowerShell per configurare e gestire le password degli account Kerberos.


> [!NOTE]
> L'oggetto account Kerberos è un oggetto computer, ma utilizza il parametro UserAccount per le operazioni nei cmdlet di Windows PowerShell a cui si fa riferimento. Si noti che questo non è un errore, ma il comportamento previsto del cmdlet quando viene utilizzato con la creazione e la manutenzione di account Kerberos.



## Argomenti della sezione

  - [Impostare la password di un account di autenticazione Kerberos in un server in Lync Server 2013](lync-server-2013-set-a-kerberos-authentication-account-password-on-a-server.md)

  - [Sincronizzare la password di un account di autenticazione Kerberos con IIS in Lync Server 2013](lync-server-2013-synchronize-a-kerberos-authentication-account-password-to-iis.md)

