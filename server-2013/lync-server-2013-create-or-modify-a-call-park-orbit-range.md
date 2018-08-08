---
title: "Lync Server 2013: Crea/modifica intervalli di codici orbit del parcheggio"
TOCTitle: Creare o modificare un intervallo di codici orbit del parcheggio di chiamata
ms:assetid: 549ec118-eee5-4333-9416-80929ec057e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398361(v=OCS.15)
ms:contentKeyID: 49300542
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per creare o modificare un intervallo orbit del parcheggio di chiamata, usare una delle procedure seguenti.

## Per creare o modificare un intervallo di numeri per il parcheggio di chiamata tramite Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Funzionalità vocali** e quindi su **Parcheggio di chiamata** .

4.  Nella pagina **Parcheggio di chiamata** effettuare una delle operazioni seguenti:
    
      - Per creare un nuovo intervallo orbit, fare clic su **Nuovo** . In **Nome** digitare un nome per identificare l'intervallo di numeri.
        

        > [!NOTE]
        > Dopo l'esecuzione del commit dell'intervallo orbit nel database non sarà possibile modificare il nome.

    
      - Per modificare un intervallo orbit esistente, digitarne il nome, per intero o in parte, nel campo di ricerca. Nell'elenco dei codici orbit risultante fare clic sul codice desiderato, fare clic su **Modifica** e quindi su **Mostra dettagli** .

5.  Nel primo campo **Intervallo numeri** digitare il numero iniziale dell'intervallo di estensioni per i codici orbit di parcheggio di chiamata e nel secondo campo **Intervallo numeri** digitare il numero finale dell'intervallo.
    

    > [!NOTE]
    > <UL>
    > <LI>
    > <P>Il numero iniziale dell'intervallo deve essere minore o uguale al numero finale dell'intervallo stesso.</P>
    > <LI>
    > <P>Il valore del numero iniziale dell'intervallo deve avere la stessa lunghezza del numero finale.</P>
    > <LI>
    > <P>L'intervallo di codici orbit deve essere univoco e non può sovrapporsi ad altri intervalli.</P>
    > <LI>
    > <P>Se l'intervallo di codici orbit inizia con il carattere * o #, l'intervallo deve essere maggiore di 100.</P>
    > <LI>
    > <P>I valori validi devono corrispondere all'espressione regolare ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8}). In pratica, il valore deve essere una stringa che inizia con il carattere * o # oppure con un numero tra 1 e 9 (il primo carattere non può essere uno zero). Se il primo carattere è * o #, il carattere successivo deve essere un numero tra 1 e 9 (non può essere uno zero). I caratteri successivi possono corrispondere a qualsiasi numero tra 0 e 9, con un massimo di sette caratteri aggiuntivi. Ad esempio, "#6000", "*92000", "*95551212" e "915551212". Se il primo carattere non è * o #, il primo carattere deve essere un numero tra 1 e 9 (non può essere zero), seguito da al massimo otto caratteri, ognuno di loro un numero compreso tra 0 e 9 (ad esempio "915551212", "41212", "300").</P>
    > <LI>
    > <P>Non è possibile definire più di 50.000 codici orbit in totale per ogni pool. Ogni intervallo di codici orbit include in genere 100 codici o meno, ma può essere molto più esteso a condizione che includa meno di 10.000 codici orbit. Anziché specificare il numero iniziale "7000000" e il numero finale "8000000", ad esempio, valutare la possibilità di specificare il numero iniziale "7000000" e il numero finale "7000100".</P></LI></UL>



6.  In **FQDN del server di destinazione** fare clic sul nome di dominio completo o l'ID del servizio dell'applicazione che ospita l' applicazione Parcheggio di chiamata. Tutte le chiamate parcheggiate nei numeri entro l'intervallo specificato dal numero iniziale e quello finale nell'intervallo di codici orbit saranno instradate a questo server o pool.

7.  Fare clic su **Commit** .

## Per creare o modificare un intervallo di numeri per il parcheggio di chiamata tramite Windows PowerShell

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Usare **New-CsCallParkOrbit** per creare un nuovo intervallo di numeri orbit. Usare **Set-CsCallParkOrbit** per modificare un intervallo di numeri orbit esistente.
    
    Nella riga di comando digitare il comando seguente:
    
        New-CsCallParkOrbit -Identity <name of orbit range> -NumberRangeStart <first number in orbit range> -NumberRangeEnd <last number in orbit range> -CallParkService <FQDN or service ID of the Application service that hosts the Call Park application>
    
    Ad esempio:
    
        New-CsCallParkOrbit -Identity "Redmond orbit 1" -NumberRangeStart 100 -NumberRangeEnd 199 -CallParkService redmond-applicationserver-1
    
    L'esempio seguente mostra come modificare i numeri di un intervallo orbit esistente.
    
        Set-CsCallParkOrbit -Identity "Redmond orbit 1" -NumberRangeStart 500 -NumberRangeEnd 699

## Vedere anche

#### Attività

[Eliminare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-delete-a-call-park-orbit-range.md)  

#### Ulteriori risorse

[New-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCallParkOrbit)  
[Set-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkOrbit)

