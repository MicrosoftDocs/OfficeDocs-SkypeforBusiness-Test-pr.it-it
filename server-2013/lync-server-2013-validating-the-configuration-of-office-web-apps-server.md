---
title: Convalida della configurazione di Office Web Apps Server in Lync Server 2013
TOCTitle: Convalida della configurazione di Office Web Apps Server
ms:assetid: f6e8ecbf-305d-4a13-92d0-b61dbd82b0ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205393(v=OCS.15)
ms:contentKeyID: 49302509
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Convalida della configurazione di Office Web Apps Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-04-22_

Dopo che Office Web Apps Server è stato aggiunto alla topologia e che la topologia è stata pubblicata, dovrebbero essere visualizzati due nuovi eventi nel registro eventi di Lync Server. In primo luogo, viene aggiunto un evento LS Data MCU (ID evento 41034). L'evento segnalerà che Office Web Apps Server è stato individuato:

**Individuazione WAC Web Conferencing Server completata. Il contenuto PowerPoint è abilitato.**

Inoltre, dovrebbe essere visualizzato un altro evento LS Data MCU (ID evento 41032) che restituisce gli URL di Office Web Apps Server. Ad esempio, dovrebbe essere visualizzato un evento simile al seguente:

**L'individuazione WAC Web Conferencing Server è stata completata.**

**Pagina del relatore interno WAC: https://atl-officewebapps-001.litwareinc.com/m/Presenter.aspx?a=0\&embed=**

**Pagina del partecipante interno WAC: https://atl-officewebapps-001.litwareinc.com/m/ParticipantFrame.aspx?a=0\&embed=true&=**

**Pagina del relatore esterno WAC:: https://atl-officewebapps-001.litwareinc.com/m/Presenter.aspx?a=0\&embed**

**Pagina del partecipante esterno WAC: https://atl-officewebapps-001.litwareinc.com/m/ParticipantFrame.aspx?a=0\&embed=true&**

Se viene visualizzato un evento LS Data MCU con ID evento 41033, l'individuazione di Office Web Apps Server ha avuto esito negativo. In tal caso, Microsoft Lync Server 2013 eseguirà tutti i tentativi possibili per individuare il server Office Web Apps Server recentemente configurato. Se è impossibile eseguire il processo di individuazione, è necessario rimuovere Office Web Apps Server dal documento relativo alla topologia, pubblicare la topologia aggiornata e quindi tentare di aggiungere di nuovo Office Web Apps Server alla topologia dopo avere risolto i problemi di connettività.

Se Office Web Apps Server è configurato correttamente ed è stato riconosciuto dal processo di individuazione, è possibile verificare il corretto funzionamento di Office Web Apps Server condividendo una presentazione di PowerPoint tra una coppia di client Microsoft Lync 2013. Se l'utente A può caricare e visualizzare la presentazione di PowerPoint e l'utente B può partecipare alla riunione e visualizzare la presentazione, Office Web Apps Server funziona correttamente.

Anche se Office Web Apps Server sembra configurato correttamente, si potrebbe ricevere il messaggio di errore "Alcune funzionalità di condivisione non sono disponibili a causa di problemi di connettività del server" quando si tenta di condividere una presentazione di PowerPoint. Se si riceve questo messaggio di errore, riavviare i Front End Server associati al nuovo Office Web Apps Server.

