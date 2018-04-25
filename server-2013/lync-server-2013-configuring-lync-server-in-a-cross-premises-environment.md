---
title: Configurazione di Microsoft Lync Server 2013 in un ambiente cross-premise
TOCTitle: Configurazione di Microsoft Lync Server 2013 in un ambiente cross-premise
ms:assetid: 700639ec-5264-4449-a8a6-d7386fad8719
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204990(v=OCS.15)
ms:contentKeyID: 49300933
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Microsoft Lync Server 2013 in un ambiente cross-premise

 

_**Ultima modifica dell'argomento:** 2014-02-05_

In una configurazione locale multipla, alcuni utenti sono ospitati su un'installazione locale di Microsoft Lync Server 2013, mentre altri sono ospitati sulla versione Office 365 di Lync Server. Per configurare l'autenticazione server-to-server authentication in un ambiente locale multiplo, è prima necessario configurare l'installazione locale di Lync Server 2013 affinché ritenga sicuro il server di autorizzazione di Office 365. Il passaggio iniziale di questo processo può essere eseguito attraverso il seguente script di Lync Server Management Shell:

    $TenantID = (Get-CsTenant -Filter {DisplayName -eq "Fabrikam.com"}).TenantId
    
    $sts = Get-CsOAuthServer microsoft.sts -ErrorAction SilentlyContinue
            
       if ($sts -eq $null)
          {
             New-CsOAuthServer microsoft.sts -MetadataUrl "https://accounts.accesscontrol.windows.net/$TenantId/metadata/json/1"
          }
       else
          {
             if ($sts.MetadataUrl -ne  "https://accounts.accesscontrol.windows.net/$TenantId/metadata/json/1")
                {
                   Remove-CsOAuthServer microsoft.sts
                   New-CsOAuthServer microsoft.sts -MetadataUrl "https://accounts.accesscontrol.windows.net/$TenantId/metadata/json/1"
                }
            }
    
    $exch = Get-CsPartnerApplication microsoft.exchange -ErrorAction SilentlyContinue
            
    if ($exch -eq $null)
       {
          New-CsPartnerApplication -Identity microsoft.exchange -ApplicationIdentifier 00000002-0000-0ff1-ce00-000000000000 -ApplicationTrustLevel Full -UseOAuthServer
        }
    else
        {
           if ($exch.ApplicationIdentifier -ne "00000002-0000-0ff1-ce00-000000000000")
              {
                 Remove-CsPartnerApplication microsoft.exchange
                 New-CsPartnerApplication -Identity microsoft.exchange -ApplicationIdentifier 00000002-0000-0ff1-ce00-000000000000 -ApplicationTrustLevel Full -UseOAuthServer 
              }
           else
              {
                 Set-CsPartnerApplication -Identity microsoft.exchange -ApplicationTrustLevel Full -UseOAuthServer
              }
       }
    
    Set-CsOAuthConfiguration -ServiceName 00000004-0000-0ff1-ce00-000000000000

Tenere a mente che il nome dell'area di autenticazione di un tenant è solitamente diverso da quello dell'organizzazione. Quasi mai il nome dell'area di autenticazione corrisponde a quello dell'ID del tenant. Per questo motivo, la prima riga dello script è utilizzata per restituire il valore della proprietà TenantId del tenant specificato (in questo caso, fabrikam.com) e per poi assegnare il nome alla variabile $TenantId:

    $TenantID = (Get-CsTenant -DisplayName "Fabrikam.com").TenantId

Al termine dello script, sarà necessario configurare una relazione di trust tra Lync Server 2013 e il server di autorizzazione, e una seconda relazione di trust tra Exchange 2013 e il server di autorizzazione. È possibile farlo soltanto attraverso i cmdlet di Microsoft Online Services.


> [!NOTE]
> Se i cmdlet di Microsoft Online Services non sono installati, è necessario eseguire due operazioni prima di procedere. Per prima cosa, scaricare e installare la versione a 64 bit di Microsoft Online Services Sign-in Assistant. Al termine dell'installazione, scaricare e installare la versione a 64 bit del modulo dei Microsoft Online Services per Windows PowerShell. Nel sito Web di Office 365 è possibile trovare informazioni sull'installazione e l'utilizzo del modulo dei Microsoft Online Services. Le istruzioni illustrano inoltre come configurare l'accesso single sign-on, la federazione e la sincronizzazione tra Office 365 e Active Directory.<BR>Se questi cmdlet non sono installati, lo script non verrà eseguito perché il cmdlet Get-CsTenant non sarà disponibile.



Dopo avere configurato Office 365 e creato i nomi del servizio principale di Office 365 per Lync Server 2013 e Exchange 2013, sarà necessario memorizzare le credenziali presso questi nomi. Per farlo, è necessario ottenere un certificato base64 X.509 salvato come file .CER. Questo certificato sarà quindi applicato ai nomi del servizio principale di Office 365.

Dopo avere ottenuto il certificato X.509, avviare il modulo dei Microsoft Online Services (fare clic su **Start**, selezionare **Tutti i programmi**, fare clic su **Microsoft Online Services** e quindi su **Modulo dei Microsoft Online Services per Windows PowerShell**). Dopo aver aperto il modulo, digitare quanto segue per importare il modulo dei Microsoft Online Windows PowerShell contenente i cmdlet da utilizzare per la gestione dei nomi del servizio principale:

    Import-Module MSOnlineExtended

Dopo avere importato il modulo, digitare il comando seguente e premere Invio, per connettersi a Office 365:

    Connect-MsolService

A questo punto, viene visualizzata una finestra di dialogo delle credenziali. Digitare il nome utente e la password di Office 365 nella finestra di dialogo, quindi scegliere OK.

Quando si è connessi a Office 365, è possibile eseguire il comando seguente per ottenere le informazioni relative ai nomi del servizio principale:

    Get-MsolServicePrincipal

Si dovrebbero ottenere informazioni simili alle seguenti, per tutti i nomi del servizio principale:

    ExtensionData        : System.Runtime.Serialization.ExtensionDataObject
    AccountEnabled       : True
    Addresses            : {}
    AppPrincipalId       : 00000004-0000-0ff1-ce00-000000000000
    DisplayName          : Microsoft Lync Server
    ObjectId             : aada5fbd-c0ae-442a-8c0b-36fec40602e2
    ServicePrincipalName : LyncServer/litwareinc.com
    TrustedForDelegation : True

Il passaggio successivo consiste nell'importazione, codifica e assegnazione del certificato X.509. Per importare e codificare il certificato, utilizzare i seguenti comandi di Windows PowerShell, assicurandosi di specificare il percorso completo del file .CER durante la selezione del metodo di importazione:

    $certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $certificate.Import("C:\Certificates\Office365.cer")
    $binaryValue = $certificate.GetRawCertData()
    $credentialsValue = [System.Convert]::ToBase64String($binaryValue)

Dopo che il certificato è stato importato e codificato, è possibile assegnarlo ai nomi del servizio principale di Office 365. Per farlo, è necessario per prima cosa utilizzare Get-MsolServicePrincipal per recuperare il valore della proprietà AppPrincipalId per i nomi del servizio principale di Lync Server e Microsoft Exchange. Il valore della proprietà AppPrincipalId viene utilizzato per identificare i nome del servizio principale assegnato al certificato. Quando si ha a disposizione il valore della proprietà AppPrincipalId per Lync Server 2013, utilizzare il comando seguente per assegnare il certificato alla versione Office 365 di Lync Server (le proprietà StartDate e EndDate devono corrispondere al periodo di validità del certificato):

    New-MsolServicePrincipalCredential -AppPrincipalId 00000004-0000-0ff1-ce00-000000000000 -Type Asymmetric -Usage Verify -Value $credentialsValue -StartDate 6/1/2012 -EndDate 5/31/2013

A questo punto è necessario ripetere il comando, questa volta utilizzando il valore della proprietà AppPrincipalId per Exchange 2013.

Se successivamente si ha bisogno di eliminare il certificato, è possibile farlo recuperando il KeyId per il certificato:

    Get-MsolServicePrincipalCredential -AppPrincipalId 00000004-0000-0ff1-ce00-000000000000

Il comando restituisce dati simili ai seguenti:

    Type      : Asymmetric
    Value     : 
    KeyId     : bc2795f3-2387-4543-a95d-f92c85c7a1b0
    StartDate : 6/1/2012 8:00:00 AM
    EndDate   : 5/31/2013 8:00:00 AM
    Usage     : Verify

È possibile eliminare il certificato utilizzando un comando simile al seguente:

    Remove-MsolServicePrincipalCredential -AppPrincipalId 00000004-0000-0ff1-ce00-000000000000 -KeyId bc2795f3-2387-4543-a95d-f92c85c7a1b0

Oltre ad assegnare il certificato, è necessario configurare il nome del servizio principale di Exchange Online e la versione locale di Lync Server 2013 come nome del servizio principale di Office 365. A tale scopo, è possibile eseguire i due comandi seguenti:

    Set-MSOLServicePrincipal -AppPrincipalID 00000002-0000-0ff1-ce00-000000000000 -AccountEnabled $true
    
    $lyncSP = Get-MSOLServicePrincipal -AppPrincipalID 00000004-0000-0ff1-ce00-000000000000
    $lyncSP.ServicePrincipalNames.Add("00000004-0000-0ff1-ce00-000000000000/lync.contoso.com")
    Set-MSOLServicePrincipal -AppPrincipalID 00000004-0000-0ff1-ce00-000000000000 -ServicePrincipalNames $lyncSP.ServicePrincipalNames

