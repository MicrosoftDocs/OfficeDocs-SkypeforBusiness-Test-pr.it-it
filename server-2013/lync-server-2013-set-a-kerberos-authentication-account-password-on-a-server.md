---
title: 'Lync Server 2013: Impostare la password di un account di autenticazione Kerberos in un server'
TOCTitle: Impostare la password di un account di autenticazione Kerberos in un server
ms:assetid: 902d3292-678d-4512-9248-586053cb638b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398734(v=OCS.15)
ms:contentKeyID: 49301313
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostare la password di un account di autenticazione Kerberos in un server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-16_

Per eseguire correttamente questa procedura, è necessario essere connessi come utente membro del gruppo RTCUniversalServerAdmins.

È necessario impostare una password sull'account Kerberos per ogni sito che dispone di Front End Server, server Standard Edition e Director. È possibile impostare la password eseguendo il cmdlet **Set-CsKerberosAccountPassword** di Windows PowerShell in un server del sito, ad esempio un Front End Server. Per ogni sito è necessario eseguire il cmdlet **Set-CsKerberosAccountPassword** . Il cmdlet configura Internet Information Services (IIS) per il servizio servizi Web e quindi imposta la password dell'account computer in Servizi di dominio Active Directory. Un metodo alternativo, basato sul parametro utilizzato con il cmdlet, consente di configurare IIS in un unico server utilizzando un altro server configurato come origine per la password dell'account Kerberos.

Quando si usa il cmdlet **Set-CsKerberosAccountPassword** per impostare una password, Kerberos imposta la password su una stringa generata in modo casuale. Questo cmdlet contatta tutte le istanze di IIS in tutti i siti centrali di Lync Server 2013 ai quali è assegnato questo account.

## Per impostare una password per un account di autenticazione Kerberos

1.  Accedere a qualsiasi computer del dominio in cui è installato Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire i due comandi seguenti dalla riga di comando:
    
        Set-CsKerberosAccountPassword -UserAccount "Domain\UserAccount"
    
    Ad esempio:
    
        Set-CsKerberosAccountPassword -UserAccount "contoso\KerbAuth"
    

    > [!NOTE]
    > È necessario specificare il parametro UserAccount nel formato Dominio\Utente. Il formato Utente@Dominio.estensione non è supportato per fare riferimento a oggetti computer creati ai fini dell'autenticazione Kerberos.

    
    > [!IMPORTANT]  
    > Dopo aver apportato le necessarie modifiche all'autenticazione Kerberos, ad esempio l'aggiunta o la rimozione di un account, è necessario eseguire <strong>Enable-CsTopology</strong> dal prompt dei comandi di Lync Server Management Shell.
