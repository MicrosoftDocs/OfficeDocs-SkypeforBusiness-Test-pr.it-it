---
title: Eliminare un annuncio
TOCTitle: Eliminare un annuncio
ms:assetid: 26ea7149-4470-4c22-9bab-8a4065aca44e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687998(v=OCS.15)
ms:contentKeyID: 49887485
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un annuncio

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per eliminare un annuncio usato per le chiamate ai numeri non assegnati, seguire questa procedura.

## Per eliminare un annuncio

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Elencare tutti gli annunci disponibili nell'organizzazione. Nella riga di comando digitare il comando seguente:
    
        Get-CsAnnouncement

4.  Nell'elenco risultante individuare l'annuncio da eliminare e copiare il GUID, quindi nella riga di comando digitare il comando seguente:
    
        Remove-CsAnnouncement -Identity "<Service:service ID/guid>" 
    
    Ad esempio:
    
        Remove-CsAnnouncement -Identity "ApplicationServer:Redmond.contoso.com/1951f734-c80f-4fb2-965d-51807c792b90"
    

    > [!NOTE]
    > Per informazioni dettagliate su altre opzioni, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAnnouncement">Get-CsAnnouncement</A> e <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsAnnouncement">Remove-CsAnnouncement</A>.



## Vedere anche

#### Attività

[Creare un annuncio in Lync Server 2013](lync-server-2013-create-an-announcement.md)  

#### Ulteriori risorse

[Remove-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsAnnouncement)  
[Get-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAnnouncement)

