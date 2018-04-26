---
title: 'Lync Server 2013: Verificare che ai dial plan siano state assegnate aree'
TOCTitle: 'Verificare che ai dial plan siano state assegnate aree '
ms:assetid: 3da3a907-0dbf-4440-b12f-370f94dd4c17
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425903(v=OCS.15)
ms:contentKeyID: 49300292
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare che ai dial plan in Lync Server 2013 siano state assegnate aree

 

_**Ultima modifica dell'argomento:** 2010-11-02_

Per i dial plan utilizzati per le conferenze telefoniche con accesso esterno deve essere specificata un' **Area per conferenze telefoniche con accesso esterno** , in modo che i numeri di accesso a tali conferenze vengano associati al dial plan appropriato. Quando si imposta un dial plan, si specifica l'area per conferenze telefoniche con accesso esterno applicabile. Quando quindi si crea il numero di accesso esterno, si selezionano le aree che associano il numero di accesso ai dial plan appropriati.

Poiché è importante specificare un'area per tutti i dial plan, è consigliabile utilizzare questa procedura per verificare che tutti i dial plan siano associati ad aree. Questo passaggio è facoltativo.

Utilizzare il cmdlet **Get-CsDialPlan** per verificare se l'area è impostata per tutti i dial plan di conferenza telefonica con accesso esterno. Se l'area non è inclusa nei dial plan, è possibile utilizzare il cmdlet **Set-CsDialPlan** per impostarla. È inoltre possibile utilizzare il Pannello di controllo di Lync Server per aggiornare l'area nei dial plan esistenti. Per informazioni dettagliate sull'utilizzo del Pannello di controllo di Lync Server, vedere [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md).

## Per verificare se nei dial plan è impostata la proprietà relativa all'area

1.  Eseguire l'accesso al computer come membro del gruppo RTCUniversalServerAdmins oppure del ruolo **Cs-VoiceAdministrator** , **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente al prompt:
    
        Get-CsDialPlan [-Identity <Identifier of the dial plans to be retrieved>]
    
    Ad esempio:
    
        Get-CsDialPlan
    
    In questo esempio vengono restituiti tutti i dial plan configurati per l'organizzazione.

4.  Esaminare i dial plan restituiti per identificare eventualmente quelli che non includono l'area di conferenza telefonica con accesso esterno. Per informazioni dettagliate, vedere la documentazione relativa a Lync Server Management Shell.

## Per impostare la proprietà relativa all'area per un dial plan

1.  Eseguire l'accesso al computer come membro del gruppo RTCUniversalServerAdmins oppure del ruolo **Cs-VoiceAdministrator** , **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per gli eventuali dial plan che non includono l'area di conferenza telefonica con accesso esterno, eseguire:
    
        Set-CsDialPlan [-Identity <Identity of the dial plan to be modified>] -DialinConferencingRegion "<new region>"
    
    Ad esempio:
    
        Set-CsDialPlan -Identity Redmond -DialinConferencingRegion "US West Coast"
    
    In questo esempio il dial plan con Identity Redmond viene modificato per impostare la proprietà DialinConferencingRegion su "US West Coast". Per informazioni dettagliate, vedere la documentazione relativa a Lync Server Management Shell.

