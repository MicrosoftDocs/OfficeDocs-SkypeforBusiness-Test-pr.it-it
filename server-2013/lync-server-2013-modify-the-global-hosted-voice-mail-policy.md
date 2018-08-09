---
title: "Lync Server 2013: Modifica criteri globali di segreteria telefonica ospitata"
TOCTitle: "Lync Server 2013: Modifica criteri globali di segreteria telefonica ospitata"
ms:assetid: f059b3ce-a7d8-4ea9-b10b-0052222ec2ce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412994(v=OCS.15)
ms:contentKeyID: 49302411
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare i criteri globali di segreteria telefonica ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-24_

I criteri *globali* di segreteria telefonica ospitata vengono installati con Lync Server 2013. È possibile modificarli in base a specifiche esigenze, ma non è possibile rinominarli né eliminarli. Per modificare i criteri globali, utilizzare il cmdlet Set-CsHostedVoicemailPolicy per impostare i parametri sui valori appropriati per la distribuzione.

Per informazioni dettagliate sul cmdlet [Set-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostedVoicemailPolicy), vedere la documentazione relativa a Lync Server Management Shell.

## Per modificare i criteri globali di segreteria telefonica ospitata

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsHostedVoicemailPolicy per impostare i parametri dei criteri globali per l'ambiente. Ad esempio, eseguire:
    
        Set-CsHostedVoicemailPolicy -Destination ExUM.fabrikam.com -Organization "corp1.litwareinc.com"
    
    Poiché questo comando non specifica il parametro Identity dei criteri, interfaccia della riga di comando Windows PowerShell imposta i valori seguenti nei criteri globali di segreteria telefonica ospitata:
    
      - **Destination** specifica il nome di dominio completo (FQDN) del servizio di messaggistica unificata di Exchange ospitato. Questo parametro è facoltativo, ma se si tenta di abilitare un utente per la segreteria telefonica ospitata e i criteri assegnati non includono un valore Destination, l'abilitazione avrà esito negativo.
    
      - **Organization** specifica un elenco di tenant di Exchange delimitati da virgole che ospitano gli utenti di Lync Server. Ogni tenant deve essere specificato come FQDN sul tenant nel servizio di messaggistica unificata di Exchange ospitato.
    

    > [!NOTE]
    > Nell'esempio di cmdlet precedente, il valore "corp1.litwareinc.com" sostituisce eventuali valori già presenti nel parametro Organization. Se ad esempio i criteri contengono già un elenco di organizzazioni delimitate da virgola, l'elenco completo verrà sostituito. Se si desidera aggiungere un'organizzazione all'elenco anziché sostituire l'intero elenco, eseguire un comando analogo al seguente.

    
        $a = Get-CsHostedVoicemailPolicy
        $a.Organization += ",corp3.litwareinc.com"
        Set-CsHostedVoicemailPolicy -Organization $a.Organization

