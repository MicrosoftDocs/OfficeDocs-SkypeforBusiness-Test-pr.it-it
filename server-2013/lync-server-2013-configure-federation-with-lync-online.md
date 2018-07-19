---
title: 'Lync Server 2013: Configurare la federazione con Lync Online'
TOCTitle: Configurare la federazione con Lync Online
ms:assetid: a10bd1d5-c003-46db-9f57-7d55d3fa08da
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205126(v=OCS.15)
ms:contentKeyID: 49301508
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la federazione di Lync Server 2013 con Lync Online

 

_**Ultima modifica dell'argomento:** 2015-08-19_

Eseguire i passaggi in questa sezione per configurare l'interoperabilità tra la distribuzione locale e Skype for Business online.

## Configurare il servizio Edge locale per la federazione con Skype for Business online

La federazione consente agli utenti nella distribuzione locale di comunicare con gli utenti di Office 365 nell'organizzazione. Per configurare la federazione, eseguire i seguenti cmdlet:

    Set-CSAccessEdgeConfiguration -AllowOutsideUsers 1 -AllowFederatedUsers 1 -UseDnsSrvRouting

    New-CSHostingProvider -Identity LyncOnline -ProxyFqdn "sipfed.online.lync.com" -Enabled $true -EnabledSharedAddressSpace $true -HostsOCSUsers $true -VerificationLevel UseSourceVerification -IsLocal $false -AutodiscoverUrl https://webdir.online.lync.com/Autodiscover/AutodiscoverService.svc/root

## Configurare il tenant Skype for Business online per uno spazio di indirizzi SIP condiviso

Un indirizzo SIP (Session Initiation Protocol) è un identificatore univoco per ogni utente in una rete, simile a un numero di telefono o un indirizzo di posta elettronica. Prima di provare a eseguire lo spostamento degli utenti Lync dall'ambiente locale a Skype for Business online, è necessario configurare il tenant di Office 365 per la condivisione di uno spazio degli indirizzi SIP con la distribuzione locale. Se il tenant non viene configurato, verrà visualizzato il seguente messaggio di errore:

Move-CsUser : HostedMigration fault: Error=(510), Description=(Il tenant dell'utente non è abilitato per lo spazio di indirizzi SIP.)

Per configurare uno spazio di indirizzi SIP condiviso, stabilire una sessione remota di PowerShell con Skype for Business online, quindi eseguire il seguente cmdlet:

    Set-CsTenantFederationConfiguration -SharedSipAddressSpace $true

Per stabilire una sessione remota di PowerShell con Skype for Business online, è prima necessario installare il modulo Skype for Business online per Windows PowerShell, disponibile al seguente indirizzo: [http://go.microsoft.com/fwlink/p/?LinkId=391911](http://go.microsoft.com/fwlink/p/?linkid=391911).

Dopo aver installato il modulo, sarà possibile stabilire una sessione remota con i seguenti cmdlet:

    Import-Module LyncOnlineConnector

    $cred = Get-Credential

    $CSSession = New-CsOnlineSession -Credential $cred

    Import-PSSession $CSSession -AllowClobber

Per ulteriori informazioni su come stabilire una sessione remota di PowerShell con Skype for Business online, vedere [Connessione a Lync Online tramite Windows PowerShell](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell).

Per ulteriori informazioni su come usare il modulo PowerShell di Skype for Business online, vedere [Uso di Windows PowerShell per gestire Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell).

## Vedere anche

#### Ulteriori risorse

[New-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostingProvider)

