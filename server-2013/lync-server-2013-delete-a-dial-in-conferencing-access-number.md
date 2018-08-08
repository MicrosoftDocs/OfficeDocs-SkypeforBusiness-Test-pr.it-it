---
title: "Lync Server 2013: Elimina numero accesso per conference call"
TOCTitle: "Lync Server 2013: Elimina numero accesso per conference call"
ms:assetid: 199c5d9c-0489-4ad5-a7f1-ca59fe0e6ac7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520956(v=OCS.15)
ms:contentKeyID: 49299826
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un numero di accesso per una conferenza telefonica con accesso esterno

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Eseguire questa procedura per eliminare un numero di accesso alle conferenze telefoniche con accesso esterno.

## Per eliminare un numero di accesso alle conferenze telefoniche con accesso esterno

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Numero di accesso esterno**.

4.  Nella pagina fare clic sul numero di accesso esterno che si desidera eliminare nell'elenco, fare clic su **Modifica** e quindi su **Elimina**.

5.  Fare clic su **OK**.

## Rimozione dei numeri di accesso esterno tramite cmdlet di Windows PowerShell

I numeri di accesso alle conferenze telefoniche con accesso esterno possono anche essere eliminati utilizzando Windows PowerShell e il cmdlet **Remove-CsDialInConferencingAccessNumber**. È possibile eseguire il cmdlet sia in Lync Server 2013 Management Shell che in una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Rimozione di un numero specifico di accesso alla conferenza telefonica con accesso esterno

  - Questo comando consente di eliminare il numero di accesso alla conferenza telefonica con accesso esterno con Identity sip:RedmondDialInAccess@litwareinc.com:
    
        Remove-CsDialInConferencingAccessNumber -Identity "sip:RedmondDialInAccess@litwareinc.com"

## Rimozione di tutti i numeri di accesso alla conferenza telefonica con accesso esterno assegnati a una specifica area

  - Questo comando consente di eliminare tutti i numeri di accesso alla conferenza telefonica con accesso esterno associati all'area Northwest:
    
        Get-CsDialInConferencingAccessNumber -Region "Northwest" | Remove-CsDialInConferencingAccessNumber

## Rimozione di numeri di accesso alla conferenza telefonica con accesso esterno in base alla lingua principale

  - Questo comando consente di eliminare tutti i numeri di accesso alla conferenza telefonica con accesso esterno che utilizzano l'italiano come lingua principale:
    
        Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -eq "it-IT"} | Remove-CsDialInConferencingAccessNumber

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Remove-CsDialInConferencingAccessNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsDialInConferencingAccessNumber).

