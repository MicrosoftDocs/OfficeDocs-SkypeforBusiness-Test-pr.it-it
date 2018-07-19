---
title: 'Lync Server 2013: Criteri di segreteria telefonica ospitata'
TOCTitle: Criteri di segreteria telefonica ospitata
ms:assetid: d62a35ed-cbe2-4f06-86b4-e192c18435c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398932(v=OCS.15)
ms:contentKeyID: 49302103
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Criteri di segreteria telefonica ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

I *criteri di segreteria telefonica ospitata* forniscono all'applicazione di routing della messaggistica unificata di Exchange di Lync Server 2013 informazioni sulla destinazione a cui instradare le chiamate per gli utenti le cui cassette postali si trovano in un servizio di Exchange ospitato.


> [!NOTE]
> I criteri di segreteria telefonica ospitata sono necessari solo per l'integrazione di Lync Server 2013 con la messaggistica unificata di Exchange ospitata. Non sono invece necessari per l'integrazione con la messaggistica unificata di Exchange locale.



## Ambito dei criteri di segreteria telefonica ospitata

L'ambito dei criteri di segreteria telefonica ospitata determina il livello gerarchico a cui si applicano i criteri. È possibile configurare questi criteri con i livelli di ambito seguenti:

  - I criteri *globali* possono potenzialmente influire su tutti gli utenti della distribuzione di Lync Server 2013. Se un utente è abilitato per l'accesso alla messaggistica unificata di Exchange ospitata, ma non gli sono stati assegnati criteri per utente e al relativo sito non sono stati assegnati criteri a livello di sito, si applicano i criteri globali. I criteri globali vengono installati con Lync Server 2013. È possibile modificarli in base a specifiche esigenze, ma non è possibile rinominarli né eliminarli.

  - I criteri a livello di *sito* possono influire su tutti gli utenti situati nel sito per cui sono definiti. Se un utente è configurato per l'accesso alla messaggistica unificata di Exchange e non gli sono stati assegnati criteri per utente, si applicano i criteri a livello di sito.

  - I criteri *per utente* possono influire solo su singoli utenti o gruppi. Per applicare criteri per utente, è necessario assegnarli esplicitamente a singoli utenti, gruppi e oggetti contatto.


> [!NOTE]
> Nella maggior parte dei casi, è necessario un solo criterio di segreteria telefonica ospitata. È spesso possibile modificare i criteri globali in base a specifiche esigenze. Se si distribuiscono più criteri di segreteria telefonica ospitata, l'ambito di tutti questi criteri sarà per utente.



## Attributi dei criteri di segreteria telefonica ospitata

I criteri di segreteria telefonica definiscono due attributi che l'applicazione di routing della messaggistica unificata di Exchange di Lync Server 2013 inserisce nell'URI di richiesta di un messaggio INVITE inviato all'implementazione di messaggistica unificata di Exchange ospitata:

  - **Destination :** nome di dominio completo (FQDN) del servizio di messaggistica unificata di Exchange ospitato. Questo valore viene utilizzato dal server perimetrale di Lync Server locale per il routing.
    

    > [!NOTE]
    > L'FQDN di Exchange Online è exap.um.outlook.com.



  - **Organization :** nome di dominio completo del tenant del servizio di messaggistica unificata di Exchange ospitata che include le cassette postali degli utenti di Lync Server 2013. I criteri di segreteria telefonica possono contenere più organizzazioni. Se sono incluse più organizzazioni, questo attributo deve essere un elenco di tenant di Exchange Server delimitati da virgole che ospitano le cassette postali degli utenti di Lync Server 2013.


> [!NOTE]
> L'amministratore tenant del servizio di messaggistica unificata di Exchange ospitato fornirà i valori necessari per le impostazioni degli attributi Destination e Organization. Per configurare i criteri, è necessario eseguire il cmdlet New-CsHostedVoicemailPolicy o utilizzare il cmdlet set-cshostedvoicemailpolicy per modificare quelli esistenti, ad esempio i criteri globali.



Per informazioni dettagliate sulla gestione dei criteri di segreteria telefonica ospitata, vedere la documentazione di Lync Server Management Shell relativa ai cmdlet seguenti:

  - New-CsHostedVoicemailPolicy

  - set-cshostedvoicemailpolicy

  - Get-CsHostedVoicemailPolicy

## Assegnazione di criteri di segreteria telefonica per utente

Se i criteri di segreteria telefonica ospitata vengono definiti con l'ambito per utente, è necessario assegnarli esplicitamente. È possibile eseguire il cmdlet Grant-CsHostedVoicemailPolicy per assegnare i criteri a singoli utenti o gruppi.

Per informazioni dettagliate sull'assegnazione o la rimozione di criteri di segreteria telefonica ospitata per utente, vedere la documentazione di Lync Server Management Shell relativa ai cmdlet seguenti:

  - Grant-CsHostedVoicemailPolicy

  - Remove-CsHostedVoicemailPolicy

