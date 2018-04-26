---
title: 'Lync Server 2013: (Facoltativo) Modificare il mapping dei tasti per i comandi DTMF'
TOCTitle: (Facoltativo) Modificare il mapping dei tasti per i comandi DTMF
ms:assetid: d753b78d-400c-4df2-957f-e7576b2019c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398943(v=OCS.15)
ms:contentKeyID: 49302121
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (Facoltativo) Modificare il mapping dei tasti per i comandi DTMF in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-30_

Gli utenti delle conferenze telefoniche con accesso esterno possono premere i tasti del telefono per eseguire comandi multifrequenza (DTMF). I comandi DTMF consentono agli utenti che accedono dall'esterno a una conferenza di controllare mediante la tastiera del telefono le impostazioni della conferenza, ad esempio disattivare e riattivare il proprio audio o bloccare e sbloccare la conferenza. È possibile utilizzare i cmdlet per cambiare i tasti utilizzati per i comandi DTMF. Questo passaggio è facoltativo.


> [!NOTE]
> Per informazioni dettagliate su questi cmdlet e sulle possibili opzioni DTMF, vedere la documentazione di Lync Server Management Shell o la Guida della riga di comando di Lync Server Management Shell.



## Per modificare il mapping dei tasti dei comandi DTMF

1.  Accedere al computer come membro del gruppo **RTCUniversalServerAdmins** oppure come membro del ruolo **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente al prompt:
    
        Get-CsDialinConferencingDtmfConfiguration
    
    Questo cmdlet restituisce le impostazioni DTMF utilizzate per le conferenze telefoniche con accesso esterno.

4.  Eseguire il cmdlet seguente e specificare il tasto da premere per ogni opzione che si desidera modificare:
    
        Set-CsDialinConferencingDtmfConfiguration [-Identity <global or site collection to be changed>]
        [-AdmitAll <default key is 8>] [-AudienceMuteCommand <default key is 4>]
        [-CommandCharacter <* (default) | #>] [-EnableDisableAnnouncementsCommand <default key is 9>]
        [-HelpCommand <default key is 1>] [-LockUnlockConferenceCommand <default key is 7>]
        [-MuteUnmuteCommand <default key is 6>] [-PrivateRollCallCommand <default key is 3>]
    
    Questo cmdlet modifica le impostazioni DTMF utilizzate per le conferenze telefoniche con accesso esterno.
    
    Ad esempio:
    
        Set-CsDialinConferencingDtmfConfiguration -EnableDisableAnnouncementsCommand 4 -AudienceMuteCommand 9
    
    In questo esempio il tasto da premere per abilitare o disabilitare l'annuncio viene scambiato con il tasto da premere per disattivare e riattivare l'audio di tutti i partecipanti. Poiché non è specificato alcun parametro Identity, le modifiche verranno applicate alle impostazioni DTMF globali.

5.  (Facoltativo) Per creare altri set di comandi DTMF per siti specifici, utilizzare il cmdlet **New-CsDialinConferencingDtmfConfiguration** con l'identità di un sito. Quando si creano nuove impostazioni DTMF per i siti, le impostazioni dei siti hanno la precedenza su quelle globali. Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell o la Guida della riga di comando di Lync Server Management Shell.

