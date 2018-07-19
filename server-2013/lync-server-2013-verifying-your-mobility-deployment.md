---
title: 'Lync Server 2013: Verifica della distribuzione per dispositivi mobili'
TOCTitle: Verifica della distribuzione per dispositivi mobili
ms:assetid: 72f9b4d3-57b0-4705-9480-cfdca313a70c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690024(v=OCS.15)
ms:contentKeyID: 49300966
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verifica della distribuzione per dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-12_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Dopo aver distribuito il servizio per dispositivi mobili Lync Server e il servizio di individuazione automatica di Lync Server, eseguire una transazione di prova per verificare il corretto funzionamento della distribuzione. È possibile eseguire **Test-CsUcwaConference** per testare la possibilità per due utenti che utilizzano client mobili di Lync 2013 di creare una conferenza, parteciparvi e comunicare. Per utilizzare questa transazione di prova, sono necessari due utenti effettivi o di prova e le rispettive credenziali complete.

Per testare l'invio di un messaggio istantaneo tra due utenti che utilizzano Lync 2010 Mobile si utilizza **Test-CsMcxP2PIM**. In modo analogo a **Test-CsUcwaConference**, è necessario utilizzare due utenti effettivi oppure due utenti di prova predefiniti.

## Per testare le funzionalità di conferenza per i client mobili di Lync 2013

1.  Accedere come membro del ruolo CsAdministrator in qualsiasi computer in cui sono installati Lync Server Management Shell e Ocscore.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare il comando seguente:
    
        Test-CsUcwaConference -TargetFqdn <FQDN of Front End pool> -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -OrganizerSipAddress sip:<SIP address of test user 1> -OrganizerCredential <test user 1 credentials> -ParticipantSipAddress sip:<SIP address of test user 2> -ParticipantCredential <test user 2 credentials> -v
    
    È possibile impostare le credenziali in uno script e passarle al cmdlet di prova, ad esempio:
    
        $passwd1 = ConvertTo-SecureString "Password01" -AsPlainText -Force
        $passwd2 = ConvertTo-SecureString "Password02" -AsPlainText -Force
        $testuser1 = New-Object Management.Automation.PSCredential("contoso\UserName1", $passwd1)
        $testuser2 = New-Object Management.Automation.PSCredential("contoso\UserName2", $passwd2)
        Test-CsUcwaConference -TargetFqdn pool01.contoso.com -Authentication Negotiate -OrganizerSipAddress sip:UserName1@contoso.com -OrganizerCredential $testuser1 -ParticipantSipAddress sip:UserName2@contoso.com -ParticipantCredential $testuser2 -v

## Per testare la messaggistica istantanea tra due persone per Lync 2010 Mobile

1.  Accedere come membro del ruolo CsAdministrator in qualsiasi computer in cui sono installati Lync Server Management Shell e Ocscore.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare il comando seguente:
    
        Test-CsMcxP2PIM -TargetFqdn <FQDN of Front End pool> -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -SenderSipAddress sip:<SIP address of test user 1> -SenderCredential <test user 1 credentials> -ReceiverSipAddress sip:<SIP address of test user 2> -ReceiverCredential <test user 2 credentials> -v
    
    È possibile impostare le credenziali in uno script e passarle al cmdlet di prova, ad esempio:
    
        $passwd1 = ConvertTo-SecureString "Password01" -AsPlainText -Force
        $passwd2 = ConvertTo-SecureString "Password02" -AsPlainText -Force
        $tuc1 = New-Object Management.Automation.PSCredential("contoso\UserName1", $passwd1)
        $tuc2 = New-Object Management.Automation.PSCredential("contoso\UserName2", $passwd2)
        Test-CsMcxP2PIM -TargetFqdn pool01.contoso.com -Authentication Negotiate -SenderSipAddress sip:UserName1@contoso.com -SenderCredential $tuc1 -ReceiverSipAddress sip:UserName2@contoso.com -ReceiverCredential $tuc2 -v

## Vedere anche

#### Ulteriori risorse

[Test-CsMcxP2PIM](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsMcxP2PIM)  
[Test-CsUcwaConference](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsUcwaConference)

