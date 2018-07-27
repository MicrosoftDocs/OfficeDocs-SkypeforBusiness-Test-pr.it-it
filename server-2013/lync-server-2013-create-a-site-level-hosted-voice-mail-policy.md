---
title: Creare criteri di segreteria telefonica ospitata a livello di sito in Lync Server 2013
TOCTitle: Creare criteri di segreteria telefonica ospitata a livello di sito in Lync Server 2013
ms:assetid: 145892c8-a6ca-45fb-9e83-786f709dd775
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398216(v=OCS.15)
ms:contentKeyID: 49299763
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare criteri di segreteria telefonica ospitata a livello di sito in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-24_

Un criterio a livello di *sito* può influire su tutti gli utenti situati nel sito per cui il criterio viene definito. Se un utente è configurato per l'accesso alla messaggistica unificata di Exchange ospitata e non gli è stato assegnato un criterio per utente, verrà applicato il criterio a livello di sito. Se non è stato distribuito un criterio a livello di sito, verrà applicato il criterio globale.

Per informazioni dettagliate sulla configurazione dei criteri sito, vedere nella documentazione di Lync Server Management Shell i cmdlet seguenti:

  - [New-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostedVoicemailPolicy)

  - [Set-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostedVoicemailPolicy)

  - [Get-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostedVoicemailPolicy)

## Per creare un criterio segreteria telefonica ospitata con ambito sito

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet New-CsHostedVoicemailPolicy per creare il criterio. Ad esempio, eseguire:
    
        New-CsHostedVoicemailPolicy -Identity site:Redmond -Destination ExUM.fabrikam.com -Description "Hosted voice mail policy for the Redmond site." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"
    
    In questo esempio viene creato un criterio segreteria telefonica ospitata con ambito sito e vengono impostati i parametri seguenti:
    
      - **Identity** specifica un identificatore univoco per il criterio, che include l'ambito. Per un criterio con ambito sito, il valore del parametro Identity deve essere specificato nel formato `site:`*\<nome\>*, ad esempio `site:Redmond`.
    
      - **Destination** specifica il nome di dominio completo (FQDN) del servizio di messaggistica unificata di Exchange ospitata. Questo parametro è facoltativo, ma se si tenta di abilitare un utente per la segreteria telefonica ospitata e il criterio assegnato all'utente non dispone di un valore Destination, l'abilitazione avrà esito negativo.
    
      - **Description** fornisce informazioni descrittive facoltative sul criterio.
    
      - **Organization** specifica un elenco separato da virgole dei tenant di Exchange che ospitano gli utenti di Lync Server 2013. Ogni tenant deve essere specificato come FQDN di quel tenant nel servizio di messaggistica unificata di Exchange ospitata.

