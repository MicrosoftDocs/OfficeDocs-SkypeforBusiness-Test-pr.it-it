---
title: Configurazione dell'autenticazione passiva di Lync Server
TOCTitle: Configurazione dell'autenticazione passiva di Lync Server
ms:assetid: 9a904b8d-9fce-4abf-be73-5c8e48cfb53a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308569(v=OCS.15)
ms:contentKeyID: 56269956
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'autenticazione passiva di Lync Server

 

_**Ultima modifica dell'argomento:** 2013-07-11_

Nella sezione seguente viene descritto come configurare Lync Server 2013 con gli aggiornamenti cumulativi di luglio 2013 per supportare l'autenticazione passiva. Dopo l'abilitazione, agli utenti Lync abilitati per l'autenticazione a due fattori verrà richiesto di utilizzare una smart card fisica o virtuale e un PIN valido per effettuare l'accesso con il client Lync 2013 con gli aggiornamenti cumulativi di luglio 2013.


> [!NOTE]
> È consigliabile che i clienti abilitino l'autenticazione passiva per il servizio di registrazione e i servizi Web a livello di servizio. Se l'autenticazione passiva viene abilitata a livello globale, è possibile che si verifichino errori di autenticazione nell'intera organizzazione per gli utenti che non effettuano l'accesso con il client desktop Lync 2013 con gli aggiornamenti cumulativi di luglio 2013.



## Configurazione dei servizi Web

Nei passaggi seguenti viene descritto come creare una configurazione personalizzata dei servizi Web per Director, pool Enterprise e server Standard Edition che saranno abilitati per l'autenticazione passiva.

**Per creare una configurazione personalizzata dei servizi Web**

1.  Accedere al Front End Server di Lync Server 2013 con gli aggiornamenti cumulativi di luglio 2013 utilizzando un account di amministratore Lync.

2.  Avviare Lync Server 2013 Management Shell.

3.  Dalla riga di comando di Lync Server Management Shell creare una nuova configurazione dei servizi Web per ogni Director, pool Enterprise e server Standard Edition che verrà abilitato per l'autenticazione passiva eseguendo il comando seguente:
    
        new-cswebserviceconfiguration -Identity "Service:WebServer:LyncPool01.contoso.com" -UseWsFedPassiveAuth $true -WsFedPassiveMetadataUri https://dc.contoso.com/federationmetadata/2007-06/federationmetadata.xml
    

    > [!WARNING]
    > Il valore per il nome FQDN WsFedPassiveMetadataUri corrisponde al nome del servizio federativo del server ADFS 2.0. Per individuare il valore del nome del servizio federativo, nella console di gestione di ADFS 2.0 fare clic con il pulsante destro del mouse su <STRONG>Service</STRONG> nel riquadro di spostamento e quindi scegliere <STRONG>Edit Federation Service Properties</STRONG>.



4.  Verificare che i valori di UseWsFedPassiveAuth e WsFedPassiveMetadataUri siano stati impostati correttamente eseguendo il comando seguente:
    
        Get-CsWebServiceConfiguration -identity "Service:WebServer:LyncPool01.contoso.com" | format-list UseWsFedPassiveAuth, WsFedPassiveMetadataUri

5.  Per i client, l'autenticazione passiva è il metodo meno preferito per l'autenticazione con webticket. Per tutti i Director, pool Enterprise e server Standard Edition che saranno abilitati per l'autenticazione passiva, è necessario disabilitare tutti gli altri tipi di autenticazione nei servizi Web Lync eseguendo il comando seguente:
    
        Set-CsWebServiceConfiguration -Identity "Service:WebServer:LyncPool01.contoso.com" -UseCertificateAuth $false -UsePinAuth $false -UseWindowsAuth NONE

6.  Verificare che tutti gli altri tipi di autenticazione siano stati correttamente disabilitati eseguendo il comando seguente:
    
        Get-CsWebServiceConfiguration -Identity "Service:WebServer:LyncPool01.contoso.com" | format-list UseCertificateAuth, UsePinAuth, UseWindowsAuth

## Configurazione del proxy

Se l'autenticazione del certificato è disabilitata per i servizi Web Lync, il client Lync utilizzerà un tipo di autenticazione meno preferito, ad esempio Kerberos o NTLM, per autenticarsi per il servizio di registrazione. L'autenticazione del certificato è comunque necessaria per consentire al client Lync di recuperare un webticket, ma è necessario disabilitare Kerberos e NTLM per il servizio di registrazione.

Nei passaggi seguenti viene descritto come creare una configurazione personalizzata del proxy per i pool di server perimetrali, i pool Enterprise e i server Standard Edition che verranno abilitati per l'autenticazione passiva.

**Per creare una configurazione personalizzata del proxy**

1.  Dalla riga di comando di Lync Server Management Shell creare una nuova configurazione del proxy per ogni pool di server perimetrali, pool Enterprise e server Standard Edition di Lync Server 2013 con aggiornamenti cumulativi di luglio 2013 che verranno abilitati per l'autenticazione passiva eseguendo il comando seguente:
    
        New-CsProxyConfiguration -Identity "Service:EdgeServer:EdgePool01.contoso.com" 
        -UseKerberosForClientToProxyAuth $False -UseNtlmForClientToProxyAuth $False
    
        New-CsProxyConfiguration -Identity "Service:Registrar:LyncPool01.contoso.com" 
        -UseKerberosForClientToProxyAuth $False -UseNtlmForClientToProxyAuth $False

2.  Verificare che tutti gli altri tipi di autenticazione proxy siano stati correttamente disabilitati eseguendo il comando seguente:
    
        Get-CsProxyConfiguration -Identity "Service:Registrar:LyncPool01.contoso.com"
         | format-list UseKerberosForClientToProxyAuth, UseNtlmForClientToProxyAuth, UseCertifcateForClientToProxyAuth

