---
title: "Lync Server 2013: Crea/modif. interv. di numeri per risp. a chiamate di gruppo"
TOCTitle: "Lync Server 2013: Crea/modif. interv. di numeri per risp. a chiamate di gruppo"
ms:assetid: 4b442b98-df6b-4e50-8254-b3be9cde21dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945627(v=OCS.15)
ms:contentKeyID: 52062146
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un intervallo di numeri per la risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Utilizzare la procedura seguente per creare o modificare un intervallo di numeri per la risposta alle chiamate di gruppo nella tabella dei codici orbit del parcheggio di chiamata.


> [!NOTE]
> È necessario utilizzare Lync Server Management Shell per creare, modificare, rimuovere e visualizzare gli intervalli di numeri per la risposta alle chiamate di gruppo nella tabella dei codici orbit del parcheggio di chiamata. Gli intervalli di numeri per la risposta alle chiamate di gruppo non sono disponibili nel Pannello di controllo di Lync Server.



> [!IMPORTANT]  
> All'intervallo di numeri per la risposta alle chiamate di gruppo deve essere assegnato il tipo GroupPickup. Gli utenti sono abilitati per la risposta alle chiamate di gruppo solo se il numero di gruppo a cui sono assegnati è di tipo GroupPickup.

Gli intervalli di numeri per la risposta alle chiamate di gruppo devono rispettare le regole seguenti:

  - Il numero iniziale dell'intervallo deve essere minore o uguale al numero finale dell'intervallo stesso.

  - Il valore del numero iniziale dell'intervallo deve avere la stessa lunghezza del numero finale.

  - L'intervallo di numeri deve essere univoco e non può sovrapporsi ad altri intervalli.

  - Se l'intervallo di numeri inizia con il carattere \* o \#, l'intervallo deve essere maggiore di 100.

  - I valori validi devono corrispondere all'espressione regolare (\[\\\*|\#\]?\[1-9\]\\d{0,7})|(\[1-9\]\\d{0,8}). In pratica, il valore deve essere una stringa che inizia con il carattere \* o \# oppure con un numero tra 1 e 9 (il primo carattere non può essere uno zero). Se il primo carattere è \* o \#, il carattere successivo deve essere un numero tra 1 e 9 (non può essere uno zero). I caratteri successivi possono corrispondere a qualsiasi numero tra 0 e 9, con un massimo di sette caratteri aggiuntivi. Ad esempio, "\#6000", "\*92000", "\*95551212" e "915551212". Se il primo carattere non è \* o \#, il primo carattere deve essere un numero tra 1 e 9 (non può essere zero), seguito al massimo da otto caratteri, ognuno di loro un numero compreso tra 0 e 9 (ad esempio "915551212", "41212", "300").

## Per creare o modificare un intervallo di numeri per la risposta alle chiamate di gruppo

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Utilizzare **New-CsCallParkOrbit** per creare un nuovo intervallo di numeri per la risposta alle chiamate di gruppo. Utilizzare **Set-CsCallParkOrbit** per modificare un intervallo esistente.
    
    Nella riga di comando, eseguire:
    
        New-CsCallParkOrbit -Identity <name of call pickup group range> -NumberRangeStart <first number in range> -NumberRangeEnd <last number in range> -CallParkService <FQDN or service ID of the Application service that hosts the Call Park application> -Type GroupPickup
    
    Ad esempio:
    
        New-CsCallParkOrbit -Identity "Redmond call pickup" -NumberRangeStart 100 -NumberRangeEnd 199 -CallParkService redmond-applicationserver-1 -Type GroupPickup
    
    L'esempio seguente mostra come modificare un intervallo di numeri da codici orbit del parcheggio di chiamata a numeri per la risposta alle chiamate di gruppo.
    
        Set-CsCallParkOrbit -Identity "Redmond call pickup" -Type GroupPickup
    
    > [!IMPORTANT]  
    > Utilizzare questo cmdlet per modificare il tipo assegnato agli intervalli di numeri solo se il tipo inizialmente specificato non è corretto e l'intervallo di numeri non è ancora in uso. Se di cambia il tipo dell'intervallo di numeri da CallPark a GroupPickup o viceversa e l'intervallo di numeri è già in uso, il parcheggio di chiamata o la risposta alle chiamate di gruppo non funzionerà più per tale intervallo. Ad esempio, se si cambia il tipo di un intervallo di numeri da CallPark a GroupPickup, l'applicazione Parcheggio di chiamata non potrà più utilizzare l'intervallo di codici orbit per il parcheggio delle chiamate.

## Vedere anche

#### Attività

[Eliminare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-delete-a-call-park-orbit-range.md)  

#### Ulteriori risorse

[New-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCallParkOrbit)  
[Set-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkOrbit)

