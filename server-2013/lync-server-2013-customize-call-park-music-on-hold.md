---
title: Personalizzare la musica di attesa del parcheggio di chiamata in Lync Server 2013
TOCTitle: Personalizzare la musica di attesa del parcheggio di chiamata in Lync Server 2013
ms:assetid: 3d78e6f9-a4ae-49f4-a89f-4515acb49dac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688031(v=OCS.15)
ms:contentKeyID: 49887529
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Personalizzare la musica di attesa del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-10_

È possibile specificare file musicali personalizzati da utilizzare per la musica di attesa al posto del file musicale predefinito fornito con Lync Server 2013. Per personalizzare la musica di attesa, utilizzare il cmdlet **Set-CsCallParkServiceMusicOnHoldFile**.


> [!NOTE]
> Se si personalizza la musica di attesa e si desidera la stessa musica per più siti, è necessario configurare il file musicale per ogni sito in cui viene eseguita l'applicazione Parcheggio di chiamata.



## Per personalizzare il file musicale

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Set-CsCallParkServiceMusicOnHoldFile -Service <ServiceID where the Call Park application resides> -Content <Byte[]>
    
    > [!tip]  
    > Utilizzare il cmdlet <strong>Get-CsService</strong> per identificare il servizio. Per informazioni dettagliate, vedere <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsService">Get-CsService</a>.    
    L'esempio seguente mostra come ottenere il contenuto del file soothingmusic.wma sotto forma di matrice di byte e come assegnarlo a una variabile. Il file audio viene quindi assegnato come file di musica di attesa per Call Park. Per informazioni dettagliate, vedere [Set-CsCallParkServiceMusicOnHoldFile](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkServiceMusicOnHoldFile).
    
        $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
        Set-CsCallParkServiceMusicOnHoldFile -Service Redmond1-applicationserver-1 -Content $a

## Vedere anche

#### Ulteriori risorse

[Set-CsCallParkServiceMusicOnHoldFile](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkServiceMusicOnHoldFile)  
[Get-CsService](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsService)

