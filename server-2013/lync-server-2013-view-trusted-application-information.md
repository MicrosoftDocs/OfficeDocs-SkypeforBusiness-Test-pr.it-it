---
title: Visualizzare informazioni sulle applicazioni attendibili
TOCTitle: Visualizzare informazioni sulle applicazioni attendibili
ms:assetid: 7b916323-96fb-4308-bc95-c178de41a3d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688103(v=OCS.15)
ms:contentKeyID: 49887619
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare informazioni sulle applicazioni attendibili

 

_**Ultima modifica dell'argomento:** 2015-03-30_

Utilizzare la procedura seguente per le informazioni della applicazioni affidabili di Lync Server 2013 Management Shell in Lync Server Management Shell.

## Visualizzare le informazioni sulle applicazioni affidabili utilizzando i cmdlet Lync Server Management Shell

È possibile visualizzare informazioni sulle applicazioni affidabili utilizzando i cmdlet Lync Server Management Shell e **Get-CsTrustedApplication**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare le applicazioni affidabili

  - Per visualizzare tutte le applicazioni affidabili, digitare il seguente comando in Lync Server Management Shell e premere INVIO:
    
        Get-CsConferenceDisclaimer
    
    Il comando restituisce informazioni simili a questa, per ciascuna applicazione affidabile:
    
        Identity               : CN={5dedf4b0-a590-49b3-80cf-f16f914bbef9},CN=Application Contacts,CN=RTC
                                 Service,CN=Services,CN=Configuration,DC=litware,DC=com
        RegistrarPool          : 487279971
        HomeServer             : CN=Lc Services,CN=Microsoft,CN=co1:2,CN=Pools,CN=RTC
                                 Service,CN=Services,CN=Configuration,DC=litware,DC=com
        OwnerUrn               : urn:application:helpdesk
        SipAddress             : sip:RtcApplication-dbf5142f-2bb2-4c4f-9531-b7fea45c5000@litware.com
        DisplayName            :
        DisplayNumber          :
        LineURI                :
        PrimaryLanguage        : 0
        SecondaryLanguages     : {}
        EnterpriseVoiceEnabled : True
        ExUmEnabled            : False
        Enabled                : True

For details, see [Get-CsTrustedApplication](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTrustedApplication).

