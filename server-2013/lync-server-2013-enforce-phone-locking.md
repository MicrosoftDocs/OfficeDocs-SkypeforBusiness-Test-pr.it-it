---
title: Applicare il blocco del telefono
TOCTitle: Applicare il blocco del telefono
ms:assetid: 1f89298b-aea9-4952-93ca-0270b565792b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520963(v=OCS.15)
ms:contentKeyID: 49299892
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applicare il blocco del telefono

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile bloccare i dispositivi Lync Phone Edition per motivi di sicurezza. Se si applica il blocco telefono, il dispositivo in cui è in esecuzione Lync Phone Edition si blocca dopo un periodo di tempo configurato dall'utente. Quando un telefono viene bloccato, un utente può eseguire le chiamate ma non può accedere alle informazioni sul calendario e i contatti, la segreteria telefonica e i log di chiamata o utilizzare la ricerca. Per sbloccare il telefono, l'utente immette un PIN.

Per applicare un blocco telefono, abilitarlo e configurarlo utilizzando il Pannello di controllo di Lync Server o i cmdlet PowerShell di Lync Server. È possibile applicare il blocco telefono globalmente o solo nel sito in cui è configurato.

## Per configurare e applicare il blocco telefono

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Fare clic su **Client** e quindi su **Configurazione dispositivo**.

4.  Nell'elenco delle configurazioni dei dispositivi nella scheda **Configurazione dispositivo** fare doppio clic sulla configurazione per cui si desidera modificare le impostazioni di blocco del telefono.

5.  Nella finestra di dialogo **Modifica configurazione dispositivo** verificare che la casella di controllo **Applica blocco dispositivo** sia selezionata.

6.  In **Lunghezza minima PIN** accettare il valore predefinito per il numero minimo di cifre che lo sblocco del PIN deve contenere o specificare un nuovo valore. L'intervallo di valori per la lunghezza del PIN è compreso tra quattro e quindici cifre. La lunghezza predefinita è di sei cifre.

7.  In **Timeout blocco telefono** accettare il valore predefinito per l'intervallo di tempo minimo che deve trascorrere prima che il telefono si blocchi o specificare un nuovo valore. L'intervallo per il timeout è compreso tra 0 e 60 minuti. Il valore predefinito è 10 minuti. Immettere il valore nel formato HH.MM.SS.

8.  Fare clic su **Commit**.

## Applicazione del blocco telefono utilizzando i cmdlet Windows PowerShell

Il blocco telefono può essere attivato utilizzando il cmdlet Set-CsUCPhoneConfiguration che può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare il blocco telefono

  - Il comando seguente attiva il blocco telefono per il sito di Redmond. Per disattivare il blocco telefono, impostare la proprietà EnforcePhoneLock su False ($False).
    
        Set-CsUCPhoneConfiguration -Identity" site:Redmond" -EnforcePhoneLock $True

## Per abilitare il blocco telefono e modificare il timeout blocco telefono

  - Questo comando attiva il blocco telefono e imposta il relativo timeout su 30 minuti.
    
        Set-CsUCPhoneConfiguration -Identity" site:Redmond" -EnforcePhoneLock $True -PhoneLockTimeout "00:30:00"

## Per abilitare il blocco telefono nell'intera organizzazione

  - In questo esempio il blocco telefono viene attivato su tutte le impostazioni di configurazione dei telefoni UC in uso nell'organizzazione.
    
        Get-CsUCPhoneConfiguration | Set-CsUCPhoneConfiguration  -EnforcePhoneLock $True

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md).

## Vedere anche

#### Concetti

[Gestione dell'autenticazione di Lync Server 2013](lync-server-2013-managing-lync-server-authentication.md)  

#### Ulteriori risorse

[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

