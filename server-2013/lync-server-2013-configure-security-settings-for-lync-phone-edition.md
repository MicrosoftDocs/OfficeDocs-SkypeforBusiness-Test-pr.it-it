---
title: Configurare le impostazioni di sicurezza per Lync Phone Edition
TOCTitle: Configurare le impostazioni di sicurezza per Lync Phone Edition
ms:assetid: 6e7cec17-8a79-4428-9300-8821256c46cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521014(v=OCS.15)
ms:contentKeyID: 49300920
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le impostazioni di sicurezza per Lync Phone Edition

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Aumentare la protezione dei dispositivi che eseguono Lync Phone Edition attraverso l'impostazione di sicurezza SIP e le impostazioni di blocco telefono.

## Per configurare le impostazioni di sicurezza per Lync Phone Edition

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi su **Configurazione dispositivo**.

4.  Nell'elenco delle configurazioni dei dispositivi nella pagina **Configurazione dispositivo** fare doppio clic sulla configurazione per cui si desidera modificare le impostazioni di sicurezza.

5.  In **Modifica configurazione dispositivo** specificare il livello di sicurezza SIP in **Sicurezza SIP**. Il livello predefinito è **Alto**, che rappresenta anche il livello consigliabile.

6.  In **Modifica configurazione dispositivo**, sotto **Blocco telefono**, selezionare o deselezionare la casella **Applica blocco dispositivo**, selezionata per impostazione predefinita, e specificare la lunghezza minima del PIN (per impostazione predefinita, 6 caratteri), e il periodo di timeout (10 minuti, per impostazione predefinita). È consigliabile utilizzare queste impostazioni predefinite o aumentare la lunghezza del PIN e/o dimunuire il periodo di timeout.
    

    > [!NOTE]
    > Per informazioni dettagliate, vedere <A href="lync-server-2013-enforce-phone-locking.md">Applicare il blocco del telefono</A>.



## Configurare le impostazioni di sicurezza per i telefoni di Lync Phone Edition attraverso i cmdlet di Lync Server Management Shell

È inoltre possibile gestire le impostazioni di sicurezza utilizzando i cmdlet Lync Server Management Shell e **Get-CsUCPhoneConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per modificare la modalità di protezione SIP

  - Questo comando imposta su Media la modalità di protezione SIP (SIPSecurityMode) della raccolta globale di impostazioni del telefono per le comunicazioni unificate. La sicurezza SIP può essere impostata su Bassa o Avanzata (valore predefinito).
    
        Set-CsUCPhoneConfiguration -Identity global -SIPSecurityMode "Medium"

## Per modificare la lunghezza minima del PIN

  - In questo esempio, tutte le impostazioni del telefono per le comunicazioni unificate sono modificate affinché richiedano una lunghezza del PIN di 7 cifre.
    
        Get-CsUCPhoneConfiguration | Set-CsUCPhoneConfiguration -MinPhonePinLength 7

Per ulteriori informazioni, vedere [Get-CsUCPhoneConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUCPhoneConfiguration).

## Vedere anche

#### Concetti

[Gestione dell'autenticazione di Lync Server 2013](lync-server-2013-managing-lync-server-authentication.md)  

#### Ulteriori risorse

[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

