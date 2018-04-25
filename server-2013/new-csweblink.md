---
title: New-CsWebLink
TOCTitle: New-CsWebLink
ms:assetid: f5c19896-4ce0-42cd-a934-30b1cdc64e3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690053(v=OCS.15)
ms:contentKeyID: 49302494
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebLink

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo collegamento Web che punta al servizio di individuazione automatica. Questo servizio consente ad applicazioni client come Lync Web App o Lync Mobile di individuare risorse chiave come ad esempio il pool principale di un utente o l'URL per partecipare a una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    New-CsWebLink -Href <String> -Token <String>

## Esempi

## ESEMPIO 1

I comandi illustrati nell'esempio 1 consentono di aggiungere un nuovo URL di individuazione automatica (http://LyncDiscover.fabrikam.com) alle impostazioni di configurazione del servizio di individuazione automatica assegnate al sito Redmond. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsWebLink** per creare un nuovo URL di individuazione automatica. Tale URL viene archiviato in una variabile denominata $Link1. Viene quindi utilizzato il cmdlet **Set-CsAutoDiscoverConfiguration** per aggiungere il nuovo URL agli URL già assegnati a queste impostazioni. Questa operazione viene effettuata utilizzando il parametro WebLinks e il valore di parametro @{Add=$Link1}.

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1}

## ESEMPIO 2

I comandi nell'esempio 2 assegnano una coppia di URL di individuazione automatica ((http://LyncDiscover.fabrikam.com e http://LyncDiscoverInternal.fabrikam.com) alle impostazioni di configurazione del servizio di individuazione automatica assegnate al sito Redmond. Per eseguire questa operazione, nei primi due comandi viene utilizzato il cmdlet **New-CsWebLink** per creare i due nuovi URL di individuazione automatica. I nuovi URL creati vengono quindi archiviati in variabili denominate $Link1 e $Link2. Dopo la creazione dei due URL, nel terzo comando viene utilizzato il cmdlet **Set-CsAutoDiscoverConfiguration** per assegnare i due URL al sito Redmond. A tale scopo, viene incluso il parametro WebLinks insieme al valore di parametro @{Add=$Link1,$Link2}. Questa sintassi comporta che i valori archiviati nelle variabili $Link1 e $Link2 vengano aggiunti alla proprietà WebLinks delle impostazioni.

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    $Link2 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscoverInternal.fabrikam.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1,$Link2}

## Descrizione dettagliata

Per un utilizzo ottimale di Lync Server nelle applicazioni client, è necessario che tali applicazioni conoscano il percorso dei componenti chiave di Lync Server. Gli utenti autenticati, ad esempio, devono essere in grado di individuare il proprio pool principale. Dopotutto possono essere autenticati solo da tale pool. Analogamente, gli utenti non autenticati devono essere in grado di eseguire operazioni come l'individuazione dell'URL utilizzato per partecipare a una conferenza.

Se tutti gli utenti hanno eseguito l'accesso all'interno del firewall dell'organizzazione, l'individuazione di tali percorsi è relativamente semplice. Questa operazione tuttavia si complica quando gli utenti accedono al sistema dall'esterno utilizzando Lync Mobile o Lync Web App.

Questa situazione si verifica in modo particolare in scenari di dominio diviso, in cui alcuni utenti di un'organizzazione dispongono di account nella versione locale di Lync Server, mentre altri dispongono di account in Microsoft Office 365. In questi casi, gli account utente possono trovarsi in foreste di Active Directory diverse e questo può rivelarsi problematico. Se, ad esempio, un utente degli Stati Uniti accede dall'Europa, il sistema deve essere in grado di riconoscere la relativa foresta e quindi associare la richiesta di accesso al pool appropriato.

Il servizio di individuazione automatica è stato introdotto nella versione di Lync Server di novembre 2011 per ovviare a questi problemi. Quando un'applicazione client tenta di accedere a Lync Server, il servizio di individuazione automatica analizza l'indirizzo SIP del client e quindi reindirizza la richiesta al pool appropriato. Le applicazioni client si connettono al servizio di individuazione automatica inviando una richiesta HTTP a un URL di individuazione automatica. Per il corretto funzionamento del servizio di individuazione automatica, è necessario che questi URL siano configurati dagli amministratori. Oltre a configurare gli URL, gli amministratori devono anche creare record DNS corrispondenti a tali URL.

Gli URL di individuazione automatica vengono assegnati alle impostazioni di configurazione del servizio di individuazione automatica. Queste impostazioni a loro volta possono essere applicate all'ambito globale o all'ambito del sito. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni. A tale raccolta tuttavia non viene assegnato alcun URL di individuazione automatica. Se una singola raccolta di impostazioni di individuazione automatica non soddisfa le proprie esigenze, è possibile utilizzare il cmdlet **New-CsAutoDiscoverConfiguration** per creare ulteriori impostazioni di configurazione nell'ambito del sito.

La gestione delle impostazioni di configurazione del servizio di individuazione automatica implica in genere l'aggiunta degli URL di individuazione automatica. Tali URL devono essere creati mediante il cmdlet **New-CsWebLink**. L'URL risultante viene archiviato in una variabile e quindi aggiunto a una raccolta di impostazioni di configurazione del servizio di individuazione automatica. Gli URL di individuazione automatica sono basati sui domini SIP utilizzati nell'organizzazione. Gli amministratori solitamente creano un URL destinato all'utilizzo da parte degli utenti all'esterno del firewall dell'organizzazione (ad esempio, http://LyncDiscover.litwareinc.com) e un secondo URL (ad esempio, http://LyncDiscoverInternal.litwareinc.com) per gli utenti all'interno del firewall.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsWebLink** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Href</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio di individuazione automatica. Ad esempio:</p>
<p>–Href &quot;http://LyncDiscover.fabrikam.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Token</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco da assegnare all'URL. Ad esempio:</p>
<p>-Token &quot;Fabrikam&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsWebLink** non accetta input da pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.WebLink.WebLink

