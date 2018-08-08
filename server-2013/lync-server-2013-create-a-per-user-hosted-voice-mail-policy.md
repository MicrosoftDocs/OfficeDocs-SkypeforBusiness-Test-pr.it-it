---
title: "Lync Server 2013:  Crea criteri di segreteria telefonica ospitata per utente"
TOCTitle: "Lync Server 2013:  Crea criteri di segreteria telefonica ospitata per utente"
ms:assetid: 39018a7c-e0c3-46a2-be4e-05604ec67a50
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425867(v=OCS.15)
ms:contentKeyID: 49300232
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare criteri di segreteria telefonica ospitata per utente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-24_

Un criterio *per utente* può avere effetto solo su singoli utenti, gruppi e oggetti contatto. Per distribuire un criterio per utente, è necessario assegnarlo esplicitamente a uno o più utenti, gruppi o oggetti contatto. Per informazioni dettagliate, vedere [Assegnare criteri di segreteria telefonica ospitata per utente in Lync Server 2013](lync-server-2013-assign-a-per-user-hosted-voice-mail-policy.md).

Per informazioni dettagliate sull'utilizzo di criteri segreteria telefonica ospitata per utente, vedere nella documentazione relativa a Lync Server Management Shell i cmdlet seguenti:

  - [New-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostedVoicemailPolicy)

  - [Set-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostedVoicemailPolicy)

  - [Get-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostedVoicemailPolicy)

## Per creare un criterio segreteria telefonica ospitata per utente

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet New-CsHostedVoicemailPolicy per creare il criterio, ad esempio:
    
        New-CsHostedVoicemailPolicy -Identity ExRedmond -Destination ExUM.fabrikam.com -Description "Hosted voice mail policy for Redmond users." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"
    
    Nell'esempio precedente viene creato un criterio segreteria telefonica ospitata con ambito per utente e vengono impostati i parametri seguenti:
    
      - **Identity** specifica un identificatore univoco per il criterio, che include l'ambito. Per un criterio con ambito per utente, questo valore di parametro viene specificato come stringa semplice, ad esempio ExRedmond.
    
      - **Destination** specifica il nome di dominio completo (FQDN) del servizio Messaggistica unificata di Exchange ospitato. Questo parametro è facoltativo, ma se si tenta di abilitare un utente per la segreteria telefonica ospitata e il criterio assegnato all'utente non dispone di un valore Destination, l'abilitazione avrà esito negativo.
    
      - **Description** fornisce informazioni descrittive facoltative sul criterio.
    
      - **Organization** specifica un elenco con valori delimitati da virgole dei tenant Exchange in cui sono situati gli utenti di Lync Server 2013. Ogni tenant deve essere specificato come FQDN del tenant nel servizio Messaggistica unificata di Exchange ospitato.

## Vedere anche

#### Attività

[Assegnare criteri di segreteria telefonica ospitata per utente in Lync Server 2013](lync-server-2013-assign-a-per-user-hosted-voice-mail-policy.md)

