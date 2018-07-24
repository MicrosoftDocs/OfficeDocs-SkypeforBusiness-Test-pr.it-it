---
title: 'Lync Server 2013: Configurazione delle notifiche push'
TOCTitle: Configurazione delle notifiche push
ms:assetid: d77f2c06-0fe6-45d5-8f08-808ab871b3e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690047(v=OCS.15)
ms:contentKeyID: 49302123
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle notifiche push in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-12_

Le notifiche Push, sotto forma di riquadri, icone o avvisi, possono essere inviate a un dispositivo mobile anche se l'applicazione mobile è inattiva. Le notifiche Push avvisano gli utenti in caso di inviti a sessioni di messaggistica istantanea nuovi o senza risposta e di messaggi in segreteria telefonica. Lync Server 2013 Mobility Service invia le notifiche a un servizio notifica Push Lync Server basato sul cloud, che quindi le invia al servizio notifica Push Apple (APNS) (per un dispositivo Apple che esegue il client Lync 2010 Mobile) o al servizio notifica Push Microsoft (per un dispositivo Windows Phone che esegue il client Lync 2010 Mobile o Lync 2013 Mobile).

> [!important]  
> Se si utilizza Windows Phone con il client Lync 2010 Mobile o Lync 2013 Mobile, la notifica Push è una considerazione importante.<br />Se si utilizza Lync 2010 Mobile su dispositivi Apple, la notifica Push è una considerazione importante.<br />Se si utilizza Lync 2013 Mobile su dispositivi Apple, la notifica Push non è più necessaria.

Per configurare la topologia in modo da supportare le notifiche push, eseguire le operazioni seguenti:

  - Se l'ambiente include un server perimetraleLync Server 2010 o Lync Server 2013, è necessario aggiungere un nuovo provider di hosting, Microsoft Lync Online, e quindi impostare una federazione del provider di hosting tra l'organizzazione e Lync Online.

  - Se l'ambiente include un Office Communications Server 2007 R2server perimetrale, è necessario configurare una federazione SIP diretta con push.lync.com.
    

    > [!NOTE]
    > Push.lync.com è un dominio di Microsoft Office 365 per il servizio notifica Push.



  - Per abilitare le notifiche push, è necessario eseguire il cmdlet **Set-CsPushNotificationConfiguration**. Per impostazione predefinita, le notifiche push sono disattivate.

  - Testare la configurazione della federazione e le notifiche push.

## Per configurare le notifiche Push con il server perimetraleLync Server 2013 o Lync Server 2010

1.  Accedere a un computer in cui sono installati Lync Server Management Shell e Ocscore come membro del gruppo RtcUniversalServerAdmins.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Aggiungere un provider di hosting online Lync Server. Nella riga di comando digitare:
    
        New-CsHostingProvider -Identity <unique identifier for Lync Online hosting provider> -Enabled $True -ProxyFqdn <FQDN for the Access Server used by the hosting provider> -VerificationLevel UseSourceVerification
    
    Ad esempio:
    
        New-CsHostingProvider -Identity "LyncOnline" -Enabled $True -ProxyFqdn "sipfed.online.lync.com" -VerificationLevel UseSourceVerification
    

    > [!NOTE]
    > Non è possibile impostare più di una relazione federativa con un singolo provider di hosting. Ossia, se è già stato impostato un provider di hosting che ha una relazione federativa con sipfed.online.lync.com, non aggiungere un altro provider di hosting, neanche se l'identità del provider di hosting è diversa da LyncOnline.



4.  Impostare la federazione del provider di hosting tra l'organizzazione e il servizio notifica Push in Lync Online. Nella riga di comando digitare:
    
        New-CsAllowedDomain -Identity "push.lync.com"

## Per configurare le notifiche Push con il server perimetraleOffice Communications Server 2007 R2

1.  accedere al server perimetrale come membro del gruppo RtcUniversalServerAdmins.

2.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **Gestione computer** .

3.  Nell'albero della console espandere **Servizi e applicazioni** , fare clic con il pulsante destro del mouse su **Microsoft Office Communications Server 2007 R2** e quindi scegliere **Proprietà** .

4.  Nella scheda **Consenti** fare clic su **Aggiungi** .

5.  Nella finestra di dialogo **Aggiungi partner federato** eseguire le operazioni seguenti:
    
      - In **Nome dominio partner federato** digitare **push.lync.com** .
    
      - In **Access Edge Server partner federato** digitare **sipfed.online.lync.com**.
    
      - Fare clic su **OK** .

## Per abilitare le notifiche push

1.  Accedere al computer in cui sono installati Lync Server Management Shell e Ocscore come membro del ruolo CsAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Abilitare le notifiche push. Nella riga di comando digitare:
    
        Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $True -EnableMicrosoftPushNotificationService $True

4.  Abilitare la federazione. Nella riga di comando digitare:
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $True

## Per testare la federazione e le notifiche push

1.  Accedere al computer in cui sono installati Lync Server Management Shell e Ocscore come membro del ruolo CsAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Testare la configurazione della federazione. Nella riga di comando digitare:
    
        Test-CsFederatedPartner -TargetFqdn <FQDN of Access Edge server used for federated SIP traffic> -Domain <FQDN of federated domain> -ProxyFqdn <FQDN of the Access Edge server used by the federated organization>
    
    Ad esempio:
    
        Test-CsFederatedPartner -TargetFqdn accessproxy.contoso.com -Domain push.lync.com -ProxyFqdn sipfed.online.lync.com

4.  Testare le notifiche push. Nella riga di comando digitare:
    
        Test-CsMcxPushNotification -AccessEdgeFqdn <Access Edge service FQDN>
    
    Ad esempio:
    
        Test-CsMcxPushNotification -AccessEdgeFqdn accessproxy.contoso.com

## Vedere anche

#### Ulteriori risorse

[Test-CsFederatedPartner](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsFederatedPartner)  
[Test-CsMcxPushNotification](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsMcxPushNotification)

