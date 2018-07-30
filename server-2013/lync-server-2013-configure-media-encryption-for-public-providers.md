---
title: 'Lync Server 2013: Configurare la crittografia multimediale per i provider pubblici'
TOCTitle: Configurare la crittografia multimediale per i provider pubblici
ms:assetid: a95814cf-c5a9-4652-8ffc-c469a2653153
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205149(v=OCS.15)
ms:contentKeyID: 49301604
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la crittografia multimediale per i provider pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-12-12_

Per informazioni dettagliate sulle licenze necessarie e su come eseguire il processo di provisioning, vedere la guida al provisioning della connettività per la messaggistica istantanea pubblica per Microsoft Lync Server, Office Communications Server e Live Communications Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=155970](http://go.microsoft.com/fwlink/p/?linkid=155970).

Se si sta implementando la federazione audio/video (A/V) con Windows Live Messenger, è necessario modificare due parametri, ovvero il livello di crittografia di Lync Server e il criterio EnablePublicCloudAccess. Per impostazione predefinita, il livello di crittografia è impostato su RequireEncryption. È necessario impostarlo su SupportEncryption. Se il criterio EnablePublicCloudAccess è impostato su False, deve essere impostato su **True** . A tale scopo, è possibile utilizzare Lync Server Management Shell.

> [!IMPORTANT]  
> Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze utente/dispositivo in aggiunta alla licenza CAL (Client Access License) standard per Lync. Il prossimo anno la federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.

## Configurare la federazione per Windows Live

1.  Avviare Lync Server Management Shell nel Front End Server. A tale scopo, fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Al prompt dei comandi digitare i comandi seguenti:
    
    ```
    Set-CsMediaConfiguration -EncryptionLevel SupportEncryption
    ```
    ```
    Set-CsExternalAccessPolicy Global -EnablePublicCloudAccess $true -EnablePublicCloudAudioVideoAccess $true
    ```

    > [!NOTE]
    > Questo passaggio è necessario perché Windows Live Messenger non supporta la crittografia dei dati audio/video. Il comando configura il criterio globale su un'impostazione di crittografia supportata anziché di crittografia richiesta per tali dati. I client che supportano la crittografia, come Lync 2013, la utilizzeranno comunque.


