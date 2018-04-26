---
title: 'Lync Server 2013: Gestione di oggetti contatto di Exchange ospitati'
TOCTitle: Gestione di oggetti contatto di Exchange ospitati
ms:assetid: eead9d76-bc4f-4c1c-9779-683cb7a88410
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412978(v=OCS.15)
ms:contentKeyID: 49302389
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione di oggetti contatto di Exchange ospitati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-25_

È necessario configurare un oggetto contatto per ogni numero di operatore automatico e per ogni numero di accesso sottoscrittore per una distribuzione su più computer.

Per l'integrazione con la messaggistica unificata di Exchange ospitata, non è possibile utilizzare ocsumutil.exe per gestire oggetti contatto, perché questa utilità dipende dalle impostazioni di Active Directory della messaggistica unificata di Exchange. Nelle distribuzioni tra più uffici, Lync Server 2013 e la messaggistica unificata di Exchange ospitata vengono installati in foreste separate senza relazione di trust. Per motivi di sicurezza, gli amministratori di Lync Server 2013 non dispongono di accesso diretto alle impostazioni di Active Directory della messaggistica unificata di Exchange. Di conseguenza, Lync Server 2013 prevede un modello diverso per la gestione degli oggetti contatto in uno *spazio di indirizzi SIP condiviso* accessibile sia a Lync Server 2013 sia al servizio di messaggistica unificata di Exchange ospitato.

## Flusso di lavoro degli oggetti contatto ospitati

Di seguito sono riportate le operazioni generali per collaborare con l'amministratore del tenant di Exchange condiviso nella gestione degli oggetti contatto:

1.  L'amministratore di Exchange richiede i numero di telefono per gli oggetti contatto di accesso di sottoscrittori e di operatore automatico della messaggistica unificata di Exchange.

2.  L'amministratore di Lync Server 2013 crea un oggetto contatto per ogni numero di telefono e assegna a ognuno di essi un criterio di segreteria telefonica ospitata.

3.  L'amministratore di Lync Server 2013 fornisce i numeri di telefono all'amministratore di Exchange.

4.  L'amministratore di Exchange assegna i numeri di telefono ai dial plan della messaggistica unificata di Exchange per operatori automatici e per l'accesso di sottoscrittori.


> [!NOTE]
> Non è necessario configurare impostazioni di dial plan di Lync Server 2013 per gli oggetti contatto come invece è richiesto per le installazioni locali.



## Configurazione di oggetti contatto ospitati


> [!NOTE]
> Per poter abilitare gli oggetti contatto di Lync Server 2013 per la messaggistica unificata di Exchange ospitata, è necessario distribuire criteri di segreteria telefonica ospitata applicabili, che possono essere ad ambito globale, a livello di sito o per utente, purché siano applicabili all'oggetto contatto da abilitare. Per informazioni dettagliate, vedere <A href="lync-server-2013-hosted-voice-mail-policies.md">Criteri di segreteria telefonica ospitata in Lync Server 2013</A>.



Per configurare oggetti contatto di accesso dei sottoscrittori e di operatori automatici ospitati in una distribuzione tra più uffici, è necessario utilizzare i cmdlet seguenti:

  - **New-CsExUmContact** crea un nuovo oggetto contatto per la messaggistica unificata ospitata.

  - **Set-CsExUmContact** modifica un contatto oggetto esistente per la messaggistica unificata di Exchange ospitata.

Nell'esempio seguente viene creato un oggetto contatto di operatore automatico:

    New-CsExUmContact -SipAddress sip:exumaa1@fabrikam.com -RegistrarPool RedmondPool.litwareinc.com -OU "OU=ExUmContacts,DC=litwareinc,DC=com" -DisplayNumber 2065559876 -AutoAttendant $True

In questo esempio viene creato un nuovo oggetto contatto della messaggistica unificata di Exchange, con l'indirizzo SIP sip:exumaa1@fabrikam.com. Il nome del pool in cui è in esecuzione il servizio Registrazione avanzata di Lync Server 2013 è RedmondPool.litwareinc.com. L'unità organizzativa in cui verranno archiviate queste informazioni è OU=ExUmContacts,DC=litwareinc,DC=com. Il numero di telefono dell'oggetto contatto è 2065554567. Il parametro facoltativo -AutoAttendant $True specifica che si tratta di un oggetto contatto di operatore automatico. Se il parametro -AutoAttendant è impostato su False (impostazione predefinita) specifica un oggetto contatto di accesso di sottoscrittori.

Per informazioni dettagliate sui cmdlet New-CsExUmContact e Set-CsExUmContact, vedere la documentazione di Lync Server Management Shell.

