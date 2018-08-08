---
title: "Lync Server 2013: Abilita utenti di Lync per il controllo chiamate remote"
TOCTitle: Abilitare gli utenti di Lync per il controllo delle chiamate remote
ms:assetid: f39bc10d-034c-4875-a0b8-554e1109e7e6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615048(v=OCS.15)
ms:contentKeyID: 49302449
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare gli utenti di Lync per il controllo delle chiamate remote in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

È possibile configurare il controllo delle chiamate remote per gli utenti di Lync utilizzando criteri di provisioning di tipo in-band basati su server. Per gestire le impostazioni del provisioning di tipo in-band, utilizzare il Pannello di controllo di Lync Server oppure l'interfaccia della riga di comando di Lync Server Management Shell. Questi strumenti sostituiscono lo snap-in Strumentazione gestione Windows (WMI) utilizzato per gestire le impostazioni di Criteri di gruppo nelle versioni precedenti.

Se si preferisce consentire agli utenti di configurare le rispettive impostazioni di controllo delle chiamate remote in Lync, è possibile configurare tali impostazioni per gli utenti nel server senza specificare i valori **URI server linea** e **URI linea**. Assicurarsi di comunicare i valori **URI server linea** e **URI linea** appropriati per gli utenti e fornire agli utenti le istruzioni per configurare queste impostazioni. Per la procedura di configurazione manuale del controllo delle chiamate remote in Lync Server, vedere "Impostare i numeri e le opzioni dei telefoni" all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=210132> nella documentazione client di Lync sul sito Web di Microsoft Office.

Se si dispone di una distribuzione esistente di Communications Server 2007 R2 o Communications Server 2007, nei client Communicator 2007 R2 e Communicator 2007 si continuerà a utilizzare i criteri di gruppo durante la migrazione affiancata. Se tuttavia si desidera trasferire le impostazioni dei criteri nei client Lync, è necessario configurare le impostazioni di provisioning di tipo in-band equivalenti di Lync Server.


> [!NOTE]
> Per abilitare il controllo delle chiamate remote per un utente, è necessario fornire all'utente sia un URI linea che un URI server linea. Come descritto in <A href="lync-server-2013-deployment-tasks-for-remote-call-control.md">Attività di distribuzione per il controllo delle chiamate remote in Lync Server 2013</A>, verificare di utilizzare la sintassi richiesta dal gateway per queste impostazioni.<BR>Verificare che il dominio nell'URI server linea sia uguale al dominio di destinazione specificato nel parametro MatchUri durante la configurazione della route statica del gateway.<BR>L'URI linea specifica il numero di telefono assegnato all'utente in formato E.164, con il prefisso "TEL:" (ad esempio tel:+14255550150). Per configurare un interno, il formato è tel:+14255550150;ext=111. Se l'URI linea dell'utente era stato configurato in precedenza e il valore non è stato modificato, non è necessario specificare l'URI linea quando si abilita il controllo delle chiamate remote per l'utente.



## Per abilitare il controllo delle chiamate remote per utenti con Lync abilitato utilizzando Management Shell

1.  Accedere a un computer in cui è installato Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins o come un ruolo di controllo di accesso basato sui ruoli a cui è stato assegnato il cmdlet **Set-CsUser**.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Per utilizzare il cmdlet **Set-CsUser** per configurare il controllo delle chiamate remote per un utente esistente con Lync abilitato, effettuare le operazioni seguenti:
    
        Set-CsUser -Identity <User ID> -EnterpriseVoiceEnabled $false -LineServerUri <SIP URI of the SIP/CSTA gateway> -LineUri <TEL URI of the user> -RemoteCallControlTelephonyEnabled $true
    
    Ad esempio:
    
        Set-CsUser -Identity "Katie Jordan" -EnterpriseVoiceEnabled $false -LineServerUri sip:rccgateway@contoso.net -LineUri tel:+14255550150 -RemoteCallControlTelephonyEnabled $true

## Per configurare gli utenti per il controllo delle chiamate remote utilizzando il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti** .

4.  Nella casella **Cerca utenti** digitare interamente (o la parte iniziale) di nome visualizzato, nome, cognome, nome account SAM (Security Accounts Manager), indirizzo SIP o URI (Uniform Resource Identifier) linea dell'account utente desiderato, quindi fare clic su **Trova** .

5.  Nella tabella fare clic sull'account utente da modificare.

6.  Scegliere **Modifica** dal menu **Modifica** .

7.  In **Telefonia** effettuare una delle operazioni seguenti:
    
      - Per abilitare il controllo delle chiamate remote in modo da consentire all'utente di controllare il telefono PBX (Private Branch Exchange) da Lync 2013 per effettuare chiamate audio da PC a PC e chiamate da PC a telefono, fare clic su **Controllo delle chiamate remote** . In **URI linea** specificare il numero di telefono dell'utente. In **URI server linea** specificare l'URI SIP del gateway SIP/CSTA.
    
      - Per abilitare il controllo delle chiamate remote, ma disabilitare le chiamate audio da PC a PC e consentire solo all'utente di controllare il telefono PBX da Lync 2013 per effettuare chiamate da PC a telefono, fare clic su **Solo controllo delle chiamate remote** . In **URI linea** specificare il numero di telefono dell'utente. In **URI server linea** specificare l'URI SIP del gateway SIP/CSTA.

8.  Al termine, fare clic su **Commit** .

