---
title: Visualizzazione delle informazioni sul dial plan
TOCTitle: Visualizzazione delle informazioni sul dial plan
ms:assetid: 25ed0112-a8a7-418a-8c2c-580081be692a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687997(v=OCS.15)
ms:contentKeyID: 49887482
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sul dial plan

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per visualizzare informazioni per un dial plan esistente, eseguire i passaggi illustrati nella procedura seguente. Se si desidera creare un nuovo dial plan, vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md).

## Per visualizzare informazioni su un dial plan dal Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Dial plan**.

4.  Nella pagina **Dial plan** fare doppio clic sul nome di un dial plan.
    

    > [!NOTE]
    > È possibile visualizzare informazioni per un solo dial plan alla volta.



## Visualizzazione di dial plan utilizzando i cmdlet di Windows PowerShell

  - È anche possibile visualizzare i dial plan utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet **Get-CsDialPlan**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).
    
    Per visualizzare informazioni su tutti i dial plan, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsDialPlan
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity                 : Global
        Description              :
        DialinConferencingRegion :
        NormalizationRules       : {Description=;
                                   Pattern=^(\d+)$;Translation=$1;Name=
                                   KeepAll;IsInternalExtension=False}
        CountryCode              :
        State                    :
        City                     :
        ExternalAccessPrefix     :
        SimpleName               : DefaultProfile
        OptimizeDeviceDialing    : False

## Vedere anche

#### Attività

[Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)  
[Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md)

