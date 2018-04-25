---
title: "Lync Server 2013: Abilitare o disabilitare l'accesso degli utenti remoti"
TOCTitle: Abilitare o disabilitare l'accesso degli utenti remoti
ms:assetid: cd9d3ddc-4839-457a-86d9-b15413e74002
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182586(v=OCS.15)
ms:contentKeyID: 49301998
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Gli utenti remoti sono utenti dell'organizzazione che dispongono di un'identità Active Directory permanente nell'organizzazione. Gli utenti remoti spesso accedono a Lync Server dall'esterno della rete utilizzando una rete privata virtuale (VPN) quando non sono connessi alla rete dell'organizzazione. Tra gli utenti remoti sono inclusi i dipendenti che lavorano dalla propria abitazione o in viaggio e altri lavoratori remoti, ad esempio fornitori considerati attendibili a cui sono state concesse credenziali aziendali. Se si abilita l'accesso degli utenti remoti, gli utenti remoti supportati si connetteranno da Internet e non dovranno utilizzare una rete VPN per collaborare con gli utenti interni che utilizzano Lync Server.

Per supportare l'accesso degli utenti remoti, è necessario abilitarlo. Quando si abilita l'accesso degli utenti remoti, tale impostazione si applica all'intera organizzazione. Se successivamente si desidera impedire, in modo temporaneo o permanente, l'accesso degli utenti remoti, è possibile disabilitarlo per l'organizzazione. Attenersi alla procedura descritta in questa sezione per abilitare o disabilitare l'accesso degli utenti remoti per l'organizzazione.


> [!NOTE]
> Abilitando l'accesso degli utenti remoti, si specifica soltanto che i server che eseguono il servizio Access Edge supportano le comunicazioni con gli utenti remoti, ma questi ultimi non possono utilizzare la messaggistica istantanea o partecipare a conferenze nell'organizzazione finché non si configura almeno un criterio per la gestione dell'utilizzo dell'accesso degli utenti remoti. Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto. Per informazioni dettagliate sulla configurazione dei criteri per l'utilizzo dell'accesso degli utenti remoti, vedere <A href="lync-server-2013-configure-policies-to-control-remote-user-access.md">Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013</A>.



## Per abilitare o disabilitare l'accesso degli utenti remoti per l'organizzazione

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Federazione e accesso esterno** e quindi su **Configurazione Access Edge** .

4.  Nella pagina **Configurazione Access Edge** fare clic su **Globale** , fare clic su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica configurazione Access Edge** eseguire una delle operazioni seguenti:
    
      - Per abilitare l'accesso degli utenti remoti per l'organizzazione, selezionare la casella di controllo **Abilita accesso remoto utenti** .
    
      - Per disabilitare l'accesso degli utenti remoti per l'organizzazione, deselezionare la casella di controllo **Abilita accesso remoto utenti** .

6.  Fare clic su **Commit** .

Per consentire agli utenti remoti di accedere ai server che eseguono Lync Server è inoltre necessario configurare almeno un criterio di accesso esterno per il supporto dell'accesso degli utenti remoti. Per informazioni dettagliate, vedere [Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-configure-policies-to-control-remote-user-access.md) nella documentazione relativa alla distribuzione e nella documentazione relativa alle operazioni.

## Abilitazione o disabilitazione dell'accesso degli utenti remoti tramite i cmdlet di Windows PowerShell

L'accesso degli utenti remoti può essere gestito mediante Windows PowerShell e il cmdlet Set-CsAccessEdgeConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare l'accesso degli utenti remoti

  - Per abilitare l'accesso degli utenti remoti, impostare il valore della proprietà **AllowOutsideUsers** su True ($True):
    
        Set-CsAccessEdgeConfiguration -AllowOutsideUsers $True

## Per disabilitare l'accesso degli utenti remoti

  - Per disabilitare l'accesso degli utenti remoti, impostare il valore della proprietà **AllowOutsideUsers** su False ($False):
    
        Set-CsAccessEdgeConfiguration -AllowOutsideUsers $False

