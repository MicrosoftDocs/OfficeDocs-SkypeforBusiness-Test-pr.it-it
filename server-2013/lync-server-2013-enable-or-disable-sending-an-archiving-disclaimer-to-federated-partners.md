---
title: "Lync Server 2013: Abilita/disab. invio dichiaraz. di non responsab. relativa a archiviaz. ai partner federati"
TOCTitle: Abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati
ms:assetid: c8e9a2fa-9dc1-4e4d-919f-56ece8004864
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182584(v=OCS.15)
ms:contentKeyID: 49301932
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Al momento della distribuzione dei server perimetrali e dell'abilitazione della federazione per l'organizzazione, dovrebbe essere stato specificato se inviare automaticamente la dichiarazione di non responsabilità relativa all'archiviazione ai partner federati. Se si archiviano le comunicazioni esterne, è consigliabile abilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione. Utilizzare la procedura descritta in questo argomento per modificare tale configurazione.


> [!NOTE]
> Nella procedura che segue si presuppone che sia stata già abilitata la federazione per l'organizzazione. Per informazioni dettagliate sull'abilitazione della federazione, vedere <A href="lync-server-2013-enable-or-disable-remote-user-access.md">Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013</A> nella documentazione relativa alla distribuzione o alle operazioni.



## Per abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e su **Configurazione Access Edge** .

4.  Nella scheda **Configurazione Access Edge** fare clic su **Globale** , quindi su **Modifica** e infine su **Mostra dettagli** .

5.  In **Modifica configurazione Access Edge** , in **Abilita comunicazioni con utenti federati** , selezionare o deselezionare la casella di controllo **Invia dichiarazione di non responsabilità relativa all'archiviazione ai partner federati** per abilitare o disabilitare l'invio automatico della dichiarazione di non responsabilità relativa all'archiviazione.

6.  Fare clic su **Commit** .

Per consentire agli utenti federati di collaborare con gli utenti della distribuzione di Lync Server 2013, è necessario inoltre aver configurato almeno un criterio di accesso esterno per il supporto dell'accesso degli utenti federati. Per informazioni dettagliate, vedere [Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md) nella documentazione relativa alla distribuzione o alle operazioni. Per informazioni dettagliate sul controllo dell'accesso per domini federati specifici, vedere [Configurare il supporto per i domini esterni consentiti in Lync Server 2013](lync-server-2013-configure-support-for-allowed-external-domains.md) nella documentazione relativa alla distribuzione o alle operazioni.

## Abilitazione o disabilitazione della dichiarazione di non responsabilità relativa all'archiviazione tramite i cmdlet di Windows PowerShell

L'utilizzo della dichiarazione di non responsabilità relativa all'archiviazione può essere gestito inoltre tramite Windows PowerShell e il cmdlet Set-CsAccessEdgeConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare la dichiarazione di non responsabilità relativa all'archiviazione

  - Per abilitare la dichiarazione di non responsabilità relativa all'archiviazione, impostare il valore della proprietà **EnableArchivingDisclaimer** su True ($True):
    
        Set-CsAccessEdgeConfiguration -EnableArchivingDisclaimer $True

## Per disabilitare la dichiarazione di non responsabilità relativa all'archiviazione

  - Per disabilitare la dichiarazione di non responsabilità relativa all'archiviazione, impostare il valore della proprietà **EnableArchivingDisclaimer** su False ($False):
    
        Set-CsAccessEdgeConfiguration -EnableArchivingDisclaimer $False

