---
title: (Scelta consigliata) Creare le directory conferenze
TOCTitle: (Scelta consigliata) Creare le directory conferenze
ms:assetid: 787f4c94-1c96-468a-a74d-e06b7bd4b8a3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn832056(v=OCS.15)
ms:contentKeyID: 63232648
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (Scelta consigliata) Creare le directory conferenze

 

_**Ultima modifica dell'argomento:** 2014-10-03_

Le directory conferenze gestiscono il mapping tra l'ID riunione alfanumerico utilizzato da un partecipante per accedere a una conferenza mediante Lync 2013 e l'ID conferenza numerico utilizzato da un partecipante di una conferenza telefonica con accesso esterno per accedere alla conferenza. Il formato dell'ID conferenza è il seguente:

    <housekeeping digit (1 digit)><conference directory (usually 1-2 digits)><conference number (variable number of digits><check digit (1 digit)>

La creazione di più directory conferenze assicura che gli ID conferenza rimangano brevi finché non si crea una quantità considerevole di conferenze. In un'organizzazione con un numero tipo di conferenze per utente, è consigliabile creare una directory conferenze per ogni 999 utenti nel pool. Attenendosi a queste indicazioni, gli ID conferenza rimangono in genere brevi. Tuttavia, quando il numero di directory conferenze nei pool supera il 9, la lunghezza degli ID conferenza aumenterà per supportare conferenze aggiuntive.

## Creazione di una directory conferenze

1.  In Lync Server Management Shell digitare il seguente cmdlet:
    
        New-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> -HomePool <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]
    
    Ad esempio, nel modo illustrato di seguito viene creata una directory conferenze con Identity 42, ospitata nel pool atl-cs-001.litwareinc.com:
    
        New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## Vedere anche

#### Concetti

[Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-dial-in-conferencing-requirements.md)  

#### Ulteriori risorse

[New-CsConferenceDirectory](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsConferenceDirectory)

