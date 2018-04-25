---
title: "Lync Server 2013: Testare e segnalare la disponibilità funzionale per l'autenticazione Kerberos"
TOCTitle: Testare e segnalare la disponibilità funzionale per l'autenticazione Kerberos
ms:assetid: d52c39e5-747d-4f29-88aa-30fd6f26b99c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398925(v=OCS.15)
ms:contentKeyID: 49302107
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testare e segnalare la disponibilità funzionale per l'autenticazione Kerberos in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-16_

Per eseguire correttamente questa procedura, è necessario essere connessi come utente membro del gruppo RTCUniversalServerAdmins.

È possibile utilizzare il cmdlet **Test-CsKerberosAccountAssignment**  Windows PowerShell per testare e segnalare la disponibilità funzionale di un'assegnazione di siti per l'autenticazione Kerberos. Con il parametro Report facoltativo, il cmdlet scrive un rapporto HTML in C:\\Logs nel computer in cui viene eseguito il comando. Il parametro Verbose facoltativo consente di visualizzare informazioni sull'attività sullo schermo.

## Per testare e segnalare la disponibilità funzionale per l'autenticazione Kerberos per un sito

1.  Come membro del gruppo RTCUniversalServerAdmins, accedere a un computer del dominio in cui è in esecuzione Lync Server 2013 oppure a un computer in cui sono installati gli strumenti di amministrazione.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Dalla riga di comando eseguire il comando seguente:
    
        Test-CsKerberosAccountAssignment -Identity "site:SiteName" -Report "c:\logs\FileName.htm" -Verbose
    
    Ad esempio:
    
        Test-CsKerberosAccountAssignment -Identity "site:Redmond" -Report "c:\logs\KerberosReport.htm" -Verbose

