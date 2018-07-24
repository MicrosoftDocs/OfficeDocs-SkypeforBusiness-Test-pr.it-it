---
title: Abilitare l'integrazione di Exchange 2013 Outlook Web App e della messaggistica istantanea
TOCTitle: Abilitare l'integrazione di Exchange 2013 Outlook Web App e della messaggistica istantanea
ms:assetid: 44d08cf0-b17d-46e1-a4f0-fcc2fe96a958
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204857(v=OCS.15)
ms:contentKeyID: 49300371
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare l'integrazione di Exchange 2013 Outlook Web App e della messaggistica istantanea

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Per abilitare l'integrazione di Exchange 2013 Outlook Web Access (OWA) e della messaggistica istantanea con Lync Server 2013, è necessario aggiungere il server Accesso client (CAS) di Exchange 2013 alla topologia di Lync Server 2013 come server applicazioni attendibili.

## Per creare un pool di applicazioni attendibili

1.  Avviare Lync Server 2013 Management Shell.

2.  Eseguire il cmdlet seguente:
    
        Get-CsSite
    
    Verrà restituito l'ID sito per il nome del sito in cui si sta creando il pool. Per informazioni dettagliate, vedere [Get-CsSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsSite) nella documentazione di Lync Server 2013 Management Shell.

3.  Eseguire il cmdlet seguente:
    
        New-CsTrustedApplicationPool -Identity <E14 CAS FQDN> -ThrottleAsServer $true -TreatAsAuthenticated $true -ComputerFQDN <E14 CAS FQDN> -Site <Site> -Registrar <Pool FQDN in the site> -RequiresReplication $false
    
    Per informazioni dettagliate, vedere [New-CsTrustedApplicationPool](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsTrustedApplicationPool) nella documentazione di Lync Server 2013 Management Shell.
    
    Il nome di dominio completo (FQDN) del server di Exchange deve essere configurato come nome oggetto (SN) del certificato Exchange OWA o come nome alternativo del soggetto (SAN).
    
    In Exchange OWA verificare anche che il nome FQDN del pool sia attendibile.
    
    > [!important]  
    > Se il server CAS <em>non</em> è collocato nello stesso server che esegue la messaggistica unificata di Exchange 2013, ignorare i passaggi rimanenti di questa procedura ed eseguire direttamente la procedura &quot;Creare un'applicazione attendibile per il server CAS di Exchange 2013&quot; più avanti in questo argomento. Se il server CAS è collocato nello stesso server che esegue la messaggistica unificata di Exchange 2013, completare i passaggi di questa procedura e non eseguire la procedura &quot;Creare un'applicazione attendibile per il server CAS Exchange 2013&quot;.

4.  Eseguire **Enable-CsTopology** .

5.  Aprire il Generatore di topologie e scaricare la topologia esistente.

6.  Nel riquadro di sinistra espandere l'albero finché non si raggiunge **Server applicazioni attendibili** .

7.  Espandere il nodo **Server applicazioni attendibili** .

8.  Verrà ora visualizzato il server CAS di Exchange 2013 elencato come server applicazioni attendibili.

## Per creare un'applicazione attendibile per il server CAS di Exchange 2013

1.  Avviare Lync Server 2013 Management Shell.

2.  Se il server CAS *non* è collocato nello stesso server che esegue la messaggistica unificata di Exchange 2013, eseguire il cmdlet seguente:
    
        New-CsTrustedApplication -ApplicationId <AppID String> -TrustedApplicationPoolFqdn <E14 CAS FQDN> -Port <available port number>
    
    Per informazioni dettagliate, vedere l'argomento [New-CsTrustedApplication](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsTrustedApplication) nella documentazione di Lync Server 2013 Management Shell.

3.  Eseguire **Enable-CsTopology** .

4.  Nel riquadro di sinistra del Generatore di topologie espandere l'albero finché non si raggiunge **Server applicazioni attendibili** .

5.  Espandere il nodo **Server applicazioni attendibili** .

6.  Verrà ora visualizzato il server CAS di Exchange 2013 elencato come server applicazioni attendibili.

