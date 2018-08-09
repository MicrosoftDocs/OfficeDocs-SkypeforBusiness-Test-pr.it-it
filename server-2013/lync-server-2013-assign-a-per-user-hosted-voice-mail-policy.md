---
title: "Lync Server 2013: Assegna criteri di segreteria telef. ospitata per utenti"
TOCTitle: "Lync Server 2013: Assegna criteri di segreteria telef. ospitata per utenti"
ms:assetid: d44c71a0-4407-4ab4-b7e0-d671dde3425f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398919(v=OCS.15)
ms:contentKeyID: 49302078
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri di segreteria telefonica ospitata per utente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2010-11-07_

La distribuzione di uno o più criteri di segreteria telefonica ospitata per utente è facoltativa. Se si distribuiscono i criteri per utente, è necessario assegnarli in modo esplicito a utenti, gruppi o oggetti contatto.

Per informazioni dettagliate sull'assegnazione o la rimozione di criteri di segreteria telefonica ospitata per utente, vedere la documentazione di Lync Server Management Shell relativa ai cmdlet seguenti:

  - Grant-CsHostedVoicemailPolicy

  - Remove-CsHostedVoicemailPolicy

## Per assegnare criteri di segreteria telefonica ospitata per utente

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Grant-CsHostedVoicemailPolicy per assegnare criteri di segreteria telefonica ospitata per utente a singoli utenti, gruppi e oggetti contatto. Ad esempio, eseguire:
    
        Grant-CsHostedVoicemailPolicy -Identity "Ken Myer" -PolicyName ExRedmond
    
    In questo esempio il criterio ExRedmond è stato assegnato all'utente Davide Garghentini.
    
    **Identity** specifica l'account utente da modificare. Il valore di Identity può essere specificato utilizzando uno dei formati seguenti:
    
      - Indirizzo SIP dell'utente
    
      - Nome dell'entità utente di Active Directory
    
      - Nome di dominio\\accesso dell'utente, ad esempio contoso\\davidegarghentini
    
      - Nome visualizzato dei servizi di dominio Active Directory dell'utente, ad esempio Davide Garghentini. Se si utilizza il nome visualizzato come valore di Identity, è possibile utilizzare il carattere jolly asterisco (\*). Ad esempio, il valore di Identity "\* Smith" restituisce tutti gli utenti con un nome visualizzato che termina con il valore di stringa "Smith".
    

    > [!NOTE]
    > Il nome account SAM di Active Directory dell'utente non può essere utilizzato come valore di Identity perché non è necessariamente univoco nella foresta.


