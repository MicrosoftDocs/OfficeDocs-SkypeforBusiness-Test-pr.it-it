---
title: Visualizzare le informazioni sul dispositivo per conferenze
TOCTitle: Visualizzare le informazioni sul dispositivo per conferenze
ms:assetid: 838bdbf8-8b68-4eb6-8fa3-45bfd5b0b1cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994043(v=OCS.15)
ms:contentKeyID: 52062190
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sul dispositivo per conferenze

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Per visualizzare informazioni sui dispositivi per conferenze configurati per l'utilizzo nell'organizzazione, è possibile utilizzare Windows PowerShell e il cmdlet **Get-CsMeetingRoom**. Eseguire il cmdlet **Get-CsMeetingRoom** da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



Se si utilizza il cmdlet **Get-CsMeetingRoom** senza parametri, vengono restituite informazioni su tutti i dispositivi per conferenze. I parametri facoltativi offrono modi diversi per filtrare le informazioni. Per informazioni dettagliate, vedere la sezione dei parametri per [Get-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingRoom).


## Visualizzazione delle informazioni su tutti i dispositivi per conferenze

  - Per visualizzare informazioni dettagliate su tutti i dispositivi per conferenze, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsMeetingRoom
    
    Il cmdlet restituisce informazioni simili alle seguenti per ogni dispositivi per conferenze. Si noti che in questo esempio sono incluse solo alcune delle informazioni che verranno visualizzate quando si esegue il cmdlet:
    
        ContactOptionFlags                : 64
        OwnerUrn                          : urn:device:roomsystem
        OriginatorSid                     :
        SamAccountName                    : room12129
        UserPrincipalName                 : room1219@litwareinc.com
        FirstName                         : 
        LastName                          :
        WindowsEmailAddress               :
        Sid                               : S-1-5-21-2831376166-2963252556-2165051629-1257
        LineServerURI                     :
        AudioVideoDisabled                : False
        IPPBXSoftPhoneRoutingEnabled      : False
        RemoteCallControlTelephonyEnabled : False
        PrivateLine                       :
        AcpInfo                           : {}
        HostedVoiceMail                   :
        DisplayName                       : Room 1219

## Visualizzazione delle informazioni su un dispositivo per conferenze specifico

  - Per visualizzare informazioni su un dispositivo per conferenze specifico, includere il parametro Identity seguito dall'identità del dispositivo per conferenze, in genere il nome visualizzato di Active Directory. Ad esempio:
    
        Get-CsMeetingRoom -Identity "Room 1219"

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Get-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingRoom).

