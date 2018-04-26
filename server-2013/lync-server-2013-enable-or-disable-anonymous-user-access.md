---
title: "Lync Server 2013: Abilitare o disabilitare l'accesso degli utenti anonimi"
TOCTitle: Abilitare o disabilitare l'accesso degli utenti anonimi
ms:assetid: f10c19e6-b6f9-4d26-9923-0165f36e4af8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619192(v=OCS.15)
ms:contentKeyID: 49302433
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare l'accesso degli utenti anonimi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Gli utenti anonimi sono utenti che non dispongono di un account utente in Servizi di dominio Active Directory dell'organizzazione o in un dominio federato supportato, ma possono essere invitati a partecipare in remoto a una conferenza locale. Consentendo la partecipazione anonima alle riunioni, si consente agli utenti anonimi, ovvero agli utenti la cui identità viene verificata solo mediante la chiave riunione o conferenza, di partecipare alle riunioni. A tale scopo, è necessario abilitare la partecipazione anonima per la propria organizzazione.

Se successivamente si desidera impedire temporaneamente o definitivamente l'accesso da parte di utenti anonimi, è possibile disabilitarlo per l'organizzazione. Eseguire la procedura illustrata in questa sezione per abilitare o disabilitare l'accesso utente anonimo per la propria organizzazione.


> [!NOTE]
> Abilitando l'accesso utente anonimo per l'organizzazione, si specifica solo che i server che eseguono il servizio Access Edge supportano l'accesso da parte di utenti anonimi. Tali utenti non possono partecipare alle riunioni dell'organizzazione finché non viene configurato e applicato almeno un criterio di conferenza a uno o più utenti o gruppi di utenti. Gli unici utenti che possono invitare utenti anonimi alle riunioni sono quelli a cui è stato assegnato il criterio di conferenza configurato per supportare l'invito di utenti anonimi. Per informazioni dettagliate sulla configurazione di criteri di conferenza per supportare l'invito di utenti anonimi, vedere <A href="lync-server-2013-conferencing-policies.md">Criteri conferenza in Lync Server 2013</A>.



## Per abilitare o disabilitare l'accesso utente anonimo per l'organizzazione

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e quindi su **Configurazione Access Edge** .

4.  Nella pagina **Configurazione Access Edge** fare clic su **Globale** , fare clic su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica configurazione Access Edge** eseguire una delle operazioni seguenti:
    
      - Per abilitare l'accesso utente anonimo per l'organizzazione, selezionare la casella di controllo **Abilita comunicazioni con utenti anonimi** .
    
      - Per disabilitare l'accesso utente anonimo per l'organizzazione, deselezionare la casella di controllo **Abilita comunicazioni con utenti anonimi** .

6.  Fare clic su **Commit** .

## Abilitazione o disabilitazione dell'accesso degli utenti anonimi tramite i cmdlet di Windows PowerShell

È anche possibile gestire l'accesso utente anonimo utilizzando Windows PowerShell e il cmdlet **Set-CsAccessEdgeConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare l'accesso degli utenti anonimi

  - Per abilitare l'accesso utente anonimo, impostare il valore della proprietà **AllowAnonymousUsers** su True ($True):
    
        Set-CsAccessEdgeConfiguration -AllowAnonymousUsers $True

## Per disabilitare l'accesso degli utenti anonimi

  - Per disabilitare l'accesso utente anonimo, impostare il valore della proprietà **AllowAnonymousUsers** su False ($False):
    
        Set-CsAccessEdgeConfiguration -AllowAnonymousUsers $False

## Vedere anche

#### Concetti

[Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013](lync-server-2013-conferencing-policy-settings-reference.md)

