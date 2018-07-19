---
title: Eliminare un gruppo di agenti
TOCTitle: Eliminare un gruppo di agenti
ms:assetid: df385fd1-62f4-42b7-a349-4eb38dea50c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182597(v=OCS.15)
ms:contentKeyID: 49302199
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un gruppo di agenti

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utilizzare una delle procedure seguenti per eliminare un gruppo di agenti.

## Per utilizzare il Pannello di controllo di Lync Server per eliminare un gruppo di agenti

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Response Group** e quindi su **Gruppo**.

4.  Nella pagina **Response Group** digitare tutto o parte del nome del gruppo di agenti da eliminare nel campo di ricerca.

5.  Nell'elenco risultante fare clic sul gruppo da eliminare, fare clic su **Modifica** e quindi su **Elimina**.

6.  Fare clic su **OK**.

## Per utilizzare i cmdlet per eliminare un gruppo di agenti

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare il comando seguente:
    
        Get-CsRgsAgentGroup -Identity <Application Server service> -Name "<name of agent group>" | Remove-CsRgsAgentGroup
    
    Ad esempio:
    
        Get-CsRgsAgentGroup -Identity service:ApplicationServer:redmond.contoso.com -Name "Human Resources" | Remove-CsRgsAgentGroup

## Vedere anche

#### Attività

[Creare o modificare un gruppo di agenti in Lync Server 2013](lync-server-2013-create-or-modify-an-agent-group.md)  

#### Ulteriori risorse

[Remove-CsRgsAgentGroup](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsRgsAgentGroup)  
[Get-CsRgsAgentGroup](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsRgsAgentGroup)

