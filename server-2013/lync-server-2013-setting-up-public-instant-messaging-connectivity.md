---
title: "Lync Server 2013: Configuraz. della connettività per messaggistica pubblica"
TOCTitle: Configurazione della connettività per la messaggistica istantanea pubblica
ms:assetid: 816dea2a-96fa-4a36-b6c2-a9402675868b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205041(v=OCS.15)
ms:contentKeyID: 49301149
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della connettività per la messaggistica istantanea pubblica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Se l'organizzazione desidera supportare la connettività di messaggistica istantanea pubblica con AOL, non è possibile utilizzare la Distribuzione guidata di Lync Server per richiedere il certificato. Eseguire le operazioni della procedura seguente.

## Configurazione della connettività per la messaggistica istantanea pubblica

1.  In un server Front End aprire il Generatore di topologie. Espandere Pool di server perimetrali e quindi fare clic con il pulsante destro del mouse sul server perimetrale o sul pool di server perimetrali. Scegliere Modifica proprietà.

2.  In Modifica proprietà, nella scheda Generale, selezionare Abilita federazione per pool di server perimetrali (porta 5061). Fare clic su OK.

3.  Fare clic su Azione, selezionare Topologia, quindi Pubblica. Quando viene richiesto, in Pubblicare la topologia fare clic su Avanti. Dopo il completamento della pubblicazione fare clic su Fine.

4.  Nel server perimetrale aprire la Distribuzione guidata di Lync Server. Fare clic su Installa o aggiorna il sistema Lync Server e quindi su Installazione o rimozione componenti di Lync Server. Fare clic su Riesegui.

5.  In Installazione componenti di Lync Server fare clic su Avanti. Nella schermata di riepilogo verranno visualizzate le azioni in esecuzione. Al termine della distribuzione, fare clic su Visualizza log per visualizzare i file di log disponibili. Fare clic su Fine per completare la distribuzione.

## Per creare una richiesta di certificato per l'interfaccia esterna del server perimetrale per il supporto della connettività di messaggistica istantanea pubblica con AOL

1.  Quando il modello richiesto è disponibile per la CA, utilizzare il cmdlet di Windows PowerShell seguente dal server perimetrale per richiedere il certificato:
    
        Request-CsCertificate -New -Type AccessEdgeExternal  -Output C:\ <certfilename.txt or certfilename.csr>  -ClientEku $true -Template <template name>
    
    Il nome predefinito del certificato del modello usato per Lync Server è Web Server. Specificare solo \<nome modello\> se è necessario utilizzare un modello diverso da quello predefinito.
    
    > [!IMPORTANT]  
    > Se l'organizzazione desidera supportare la messaggistica istantanea pubblica con AOL, è necessario utilizzare Windows PowerShell anziché la Configurazione guidata certificato per richiedere il certificato da assegnare al perimetro esterno per il servizio Access Edge. Il motivo è che il modello Web Server dell'Autorità di certificazione utilizzato dalla Configurazione guidata certificato per richiedere un certificato non supporta la configurazione dell'utilizzo chiavi avanzato (EKU) client. Prima di utilizzare Windows PowerShell per creare il certificato, l'amministratore della CA deve creare e distribuire un nuovo modello che supporta l'EKU client.
