---
title: "Lync Server 2013: Esegue migrazione utenti nell'archivio contatti unificato"
TOCTitle: Eseguire la migrazione degli utenti nell'archivio contatti unificato
ms:assetid: 215a8ec1-d63e-4fdf-b73d-75aeb9dddb43
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204737(v=OCS.15)
ms:contentKeyID: 49299913
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione degli utenti nell'archivio contatti unificato in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-15_

I contatti di un utente vengono migrati automaticamente al server di Exchange 2013 se:

  - All'utente sono stati assegnati servizi utente per cui UcsAllowed è impostato su True.

  - Gli è stata fornita una cassetta postale di Exchange 2013 e se a tale cassetta ha effettuato l'accesso almeno una volta.

  - Effettua l'accesso utilizzando un rich-client Lync 2013.

Se l'utente effettua l'accesso con un client Lync 2010 o precedente o se non è connesso a un server di Exchange 2013, i criteri dei servizi utente vengono ignorati e i contatti dell'utente rimangono in Lync Server.

È possibile stabilire se i contatti di un utente sono stati migrati usando uno dei metodi seguenti:

  - Verificare la chiave del Registro di sistema seguente nel computer client:
    
    HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\15.0\\Lync\\\<SIP URL\>\\UCS
    
    Se i contatti dell'utente sono archiviati in Exchange 2013, questa chiave contiene un valore InUCSMode pari a 2165.

  - Eseguire il cmdlet **Test-CsUnifiedContactStore**. Sulla riga di comando di Lync Server Management Shell digitare:
    
        Test-CsUnifiedContactStore -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetFqdn "atl-cs-001.litwareinc.com"
    
    Se **Test-CsUnifiedContactStore** ha esito positivo, i contatti dell'utente sono stati migrati nell'archivio contatti unificato.

