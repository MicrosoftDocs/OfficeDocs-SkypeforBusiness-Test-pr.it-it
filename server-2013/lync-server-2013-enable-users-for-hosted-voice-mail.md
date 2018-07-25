---
title: 'Lync Server 2013: Abilitare gli utenti per la segreteria telefonica ospitata'
TOCTitle: Abilitare gli utenti per la segreteria telefonica ospitata
ms:assetid: fa559f8f-ef99-43a1-b580-9e998b95efb8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413062(v=OCS.15)
ms:contentKeyID: 49302544
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare gli utenti per la segreteria telefonica ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-24_

Seguire la procedura per abilitare gli utenti di Lync Server 2013 per la segreteria telefonica in un servizio di messaggistica unificata di Exchange ospitata.

Per informazioni dettagliate, vedere [Gestione di utenti di Exchange ospitati in Lync Server 2013](lync-server-2013-hosted-exchange-user-management.md) nella documentazione relativa alla pianificazione.

Per informazioni dettagliate sul cmdlet [Set-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUser), vedere la documentazione relativa a Lync Server Management Shell.

> [!important]  
> Per poter abilitare un utente di Lync Server 2013 alla segreteria telefonica ospitata, è necessario distribuire un criterio di segreteria telefonica ospitata applicato all'account relativo. Per informazioni dettagliate, vedere <a href="lync-server-2013-hosted-voice-mail-policies.md">Criteri di segreteria telefonica ospitata in Lync Server 2013</a>.

## Per abilitare gli utenti alla segreteria telefonica ospitata

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsUser per configurare l'account utente per la segreteria telefonica ospitata. Ad esempio, eseguire:
    
        Set-CsUser -HostedVoiceMail $True -Identity "contoso\kenmyer"
    
    Nell'esempio precedente vengono impostati i parametri seguenti:
    
      - **HostedVoiceMail** consente di instradare le chiamate alla segreteria telefonica di un utente alla messaggistica unificata di Exchange ospitata. Inoltre segnala a Microsoft Lync 2013 di accendere la spia della chiamata alla segreteria telefonica.
    
      - **Identity** specifica l'account utente da modificare. Il valore di Identity può essere specificato utilizzando qualsiasi dei formati seguenti:
        
          - Indirizzo SIP dell'utente
        
          - Nome dell'entità utente di Active Directory dell'utente
        
          - Dominio\\nome di accesso dell'utente (ad esempio, contoso\\davidegarghentini)
        
          - Nome visualizzato di Servizi di dominio Active Directory (ad esempio, Davide Garghentini). Se si utilizza il nome visualizzato come valore di Identity, è possibile utilizzare il carattere jolly asterisco (\*). Ad esempio, il valore di Identity "\* Smith" restituisce tutti gli utenti il cui nome visualizzato termina con un valore di stringa "Smith".
        

        > [!NOTE]
        > Non è possibile utilizzare il nome account SAM di Active Directory dell'utente come valore di Identity poiché il nome account SAM non è necessariamente univoco nella foresta.


