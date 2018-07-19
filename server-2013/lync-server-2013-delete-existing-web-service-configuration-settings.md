---
title: Eliminare le impostazioni di configurazione del servizio Web esistente
TOCTitle: Eliminare le impostazioni di configurazione del servizio Web esistente
ms:assetid: c2b96f4c-4b07-48e6-9ca6-55bc0e0cf5a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182582(v=OCS.15)
ms:contentKeyID: 49301877
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare le impostazioni di configurazione del servizio Web esistente

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Eseguire la procedura seguente per eliminare criteri del servizio Web.

## Per eliminare criteri del servizio Web

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza** e quindi su **Servizio Web**.

4.  Nella pagina **Servizio Web** digitare il nome dei criteri che si desidera eliminare nel campo di ricerca, per intero o in parte.

5.  Nell'elenco dei criteri fare clic sui criteri desiderati, fare clic su **Modifica** e quindi su **Elimina**.

6.  Fare clic su **OK**.

## Eliminazione delle impostazioni di configurazione di nuovi servizi Web mediante i cmdlet di Lync Server Management Shell

È inoltre possibile eliminare le impostazioni di configurazione di servizi Web utilizzando Lync Server Management Shell e il cmdlet **Remove-CsWebServiceConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per eliminare una raccolta specifica di impostazioni di configurazione di servizi Web

  - Con il comando seguente vengono rimosse le impostazioni di sicurezza di servizi Web applicate al sito Redmond:
    
        Remove-CsWebServiceConfiguration -Identity "site:Redmond"

## Per eliminare tutte le impostazioni di configurazione di servizi Web applicate nell'ambito del sito

  - Con il comando seguente vengono rimosse tutte le impostazioni di sicurezza di servizi Web applicate nell'ambito del servizio:
    
        Get-CsWebServiceConfiguration -Filter "service:*" | Remove-CsWebServiceConfiguration

## Per eliminare tutte le impostazioni di configurazione di servizi Web che consentono l'autenticazione basata sui certificati

  - Con il comando seguente vengono rimosse tutte le impostazioni di sicurezza di servizi Web che consentono l'utilizzo dell'autenticazione basata sui certificati:
    
        Get-CsWebServiceConfiguration | Where-Object {$_.UseCertificateAuth -eq $True} | Remove-CsWebServiceConfiguration

Per informazioni dettagliate, vedere [Remove-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsWebServiceConfiguration).

## Vedere anche

#### Ulteriori risorse

[Configurazione della sicurezza](lync-server-2013-configuring-authentication-in-the-lync-server-control-panel.md)

