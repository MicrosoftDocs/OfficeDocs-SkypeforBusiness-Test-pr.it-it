---
title: "Lync Server 2013: Genera rapporto sulle assegnazioni degli account Kerberos"
TOCTitle: Generare un rapporto sulle assegnazioni degli account Kerberos
ms:assetid: 523231f6-81b3-454b-996d-663d9bd5cf83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398343(v=OCS.15)
ms:contentKeyID: 49300575
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Generare un rapporto sulle assegnazioni degli account Kerberos in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-16_

Per eseguire correttamente questa procedura, è necessario essere connessi come utente membro del gruppo RTCUniversalServerAdmins.

È possibile utilizzare il cmdlet **Get-CsKerberosAccountAssignment** per richiedere informazioni sulle assegnazioni di account di autenticazione Kerberos e restituire informazioni sulle assegnazioni correnti nella distribuzione.

## Per recuperare le assegnazioni di account di autenticazione Kerberos per un sito

1.  Come membro del gruppo RTCUniversalServerAdmins, accedere a un computer nel dominio che esegue Lync Server 2013 oppure a un computer in cui sono installati gli strumenti di amministrazione.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire uno dei comandi seguenti dalla riga di comando:
    
      - Per recuperare tutte le assegnazioni di account di autenticazione Kerberos nell'organizzazione e restituire informazioni sulle assegnazioni per ognuna, eseguire il cmdlet senza parametri:
        
            Get-CsKerberosAccountAssignment
    
      - Per recuperare tutte le assegnazioni di account di autenticazione Kerberos nella distribuzione e restituire informazioni sulle assegnazioni del sito per ognuna, eseguire il cmdlet con il parametro Identity:
        
            Get-CsKerberosAccountAssignment -Identity "site:SiteName"
        
        Ad esempio:
        
            Get-CsKerberosAccountAssignment -Identity "site:Redmond"
    
      - Per recuperare tutte le assegnazioni di account di autenticazione Kerberos in un singolo sito e restituire informazioni sulle assegnazioni per ognuna, eseguire il cmdlet con il parametro Filter:
        
            Get-CsKerberosAccountAssignment -Filter "SiteName"
        
        Ad esempio:
        
            Get-CsKerberosAccountAssignment -Filter "*Redmond"
        

        > [!NOTE]
        > Se si specifica *NomeSito per il parametro Filter vengono restituite informazioni su tutti i siti che contengono il nome di sito specificato in qualsiasi posizione nell'identificatore di sito (ad esempio, tutti i siti che contengono la stringa Redmond nell'identificatore di sito).


