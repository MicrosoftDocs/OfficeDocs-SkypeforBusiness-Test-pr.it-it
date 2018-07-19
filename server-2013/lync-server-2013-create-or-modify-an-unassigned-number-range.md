---
title: 'Lync Server 2013: Creare o modificare un intervallo di numeri non assegnati'
TOCTitle: Creare o modificare un intervallo di numeri non assegnati
ms:assetid: a102b226-0460-4d5c-82f9-79b8444fa958
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412748(v=OCS.15)
ms:contentKeyID: 49301506
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un intervallo di numeri non assegnati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per configurare gli intervalli di numeri non assegnati per l' applicazione Annuncio, eseguire le procedure illustrate di seguito.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima di configurare la tabella dei numeri non assegnati è necessario che sia definito almeno un annuncio o che sia impostato un Operatore automatico messaggistica unificata di Exchange.</td>
</tr>
</tbody>
</table>


## Per utilizzare il Pannello di controllo di Lync Server per configurare i numeri di telefono non assegnati

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Funzionalità vocali** e quindi su **Numero non assegnato** .

4.  Nella pagina **Numero non assegnato** eseguire una delle operazioni seguenti:
    
      - Per creare un nuovo intervallo di numeri, fare clic su **Nuovo** . In **Nome** digitare un nome che identifichi l'intervallo di numeri.
        

        > [!NOTE]
        > Dopo l'esecuzione del commit del nuovo intervallo di numeri non assegnati nel database non sarà possibile modificare il nome.

    
      - Per modificare un intervallo di numeri esistente, digitare tutto o una parte del nome dell'intervallo di numeri nel campo di ricerca. Nell'elenco di intervalli di numeri risultante fare clic sul nome desiderato, su **Modifica** e quindi su **Mostra dettagli** .

5.  Nel primo campo **Intervallo numeri** digitare il numero iniziale dell'intervallo e nel secondo campo **Intervallo numeri** digitare il numero finale.
    

    > [!NOTE]
    > <UL>
    > <LI>
    > <P>Il numero iniziale dell'intervallo deve essere minore o uguale al numero finale dell'intervallo stesso.</P>
    > <LI>
    > <P>Se il numero iniziale o il numero finale dell'intervallo include un numero di interno, devono includerlo entrambi. Il numero di interno deve essere lo stesso per ambedue.</P>
    > <LI>
    > <P>Il numero deve corrispondere all'espressione regolare (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Ciò significa che il numero può iniziare con la stringa tel: (se questa non viene specificata, verrà aggiunta automaticamente), un segno più (+) e una cifra compresa tra 1 e 9. Il numero di telefono può contenere fino a 17 cifre e può essere seguito da un interno nel formato ;ext= seguito dal numero dell'interno.</P></LI></UL>



6.  In **Servizio Annuncio** eseguire una delle operazioni seguenti:
    
      - Fare clic su **Annuncio** .
    
      - Fare clic su **Messaggistica unificata di Exchange** .

7.  Se nel passaggio precedente si è fatto clic su **Annuncio** , eseguire le operazioni seguenti:
    
    1.  In **FQDN del server di destinazione** fare clic su **Seleziona** , sull'ID del servizio applicazione che esegue l' applicazione Annuncio che gestirà le chiamate in arrivo destinate all'intervallo di numero non assegnati e quindi su **OK** .
    
    2.  In **Annuncio** fare clic sull'annuncio da riprodurre per l'intervallo di numeri non assegnati.

8.  Se nel passaggio precedente si è fatto clic su **Messaggistica unificata di Exchange** , in **Numero di telefono operatore automatico** fare clic su **Seleziona** , quindi sul numero di telefono da utilizzare per l'intervallo di numeri non assegnati e quindi fare clic su **OK** .

9.  Fare clic su **OK** .

10. Nella pagina **Numero non assegnato** verificare che gli intervalli di numeri non assegnati siano disposti nell'ordine desiderato. Per modificare la posizione di un intervallo nella tabella, fare clic su uno o più nomi consecutivi nell'elenco di intervalli e quindi fare clic sulla freccia in su o sulla freccia in giù.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server esegue una ricerca all'interno della tabella dei numeri non assegnati dall'inizio alla fine e utilizza il primo intervallo che corrisponde al numero non assegnato. Se vi sono intervalli che si sovrappongono e per un intervallo è specificata un'azione da eseguire come ultimo tentativo, verificare che tale intervallo si trovi alla fine dell'elenco.</td>
    </tr>
    </tbody>
    </table>


11. Quando gli intervalli di numeri non assegnati si trovano nell'ordine desiderato, fare clic su **Salva tutto** .

## Per utilizzare il Windows PowerShell per configurare i numeri di telefono non assegnati

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Utilizzare **New-CsUnassignedNumber** per creare un nuovo intervallo di numeri non assegnati. Utilizzare **Set-CsUnassignedNumber** per modificare un intervallo di numeri non assegnati esistente.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se vi sono intervalli che si sovrappongono e si desidera che gli intervalli vengano applicati in un ordine specifico, includere il parametro Priority. Alla chiamata verrà applicato l'intervallo con la priorità più alta.</td>
    </tr>
    </tbody>
    </table>
    
    Nella riga di comando eseguire una delle operazioni seguenti:
    
      - Per creare un intervallo di numeri per un servizio Annuncio, eseguire quanto segue:
        
            New-CsUnassignedNumber -Identity <unique identifier for unassigned number range> -NumberRangeStart <first number in range> -NumberRangeEnd <last number in range> -AnnouncementName <announcement name> -AnnouncementService <FQDN or service ID of the Announcement service>
    
      - Per creare un intervallo di numeri per l'Operatore automatico messaggistica unificata di Exchange, eseguire quanto segue:
        
            New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <phone number> -Identity <unique identifier for unassigned number range> -NumberRangeStart <first number in range> -NumberRangeEnd <last number in range>
    
    Ad esempio:
    
        New-CsUnassignedNumber -Identity "Unassigned range 1" -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100" -AnnouncementName "Welcome Announcement" -AnnouncementService ApplicationServer:Redmond.contoso.com
    
    Oppure
    
        New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber "+12065551234" -Identity "Unassigned range 1" -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100"
    
    Nell'esempio seguente viene illustrato come modificare i numeri di un intervallo di numeri non assegnati esistente:
    
        Set-CsUnassignedNumber -Identity "Unassigned range 1" -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## Vedere anche

#### Attività

[Eliminare un intervallo di numeri non assegnati](lync-server-2013-delete-an-unassigned-number-range.md)  

#### Ulteriori risorse

[New-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsUnassignedNumber)  
[Set-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUnassignedNumber)  
[Get-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUnassignedNumber)

