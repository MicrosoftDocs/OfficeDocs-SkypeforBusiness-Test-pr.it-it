---
title: Connessione dei server Live ID non riuscita
TOCTitle: Connessione dei server Live ID non riuscita
ms:assetid: 701af721-dd6a-4f48-96f9-94e89c644201
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362811(v=OCS.15)
ms:contentKeyID: 56269920
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connessione dei server Live ID non riuscita

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Sono in genere tre i motivi della non riusciuta di un tentativo di connessione, con l'errore riportato di seguito:

    Get-CsWebTicket : Connessione dei server Live ID non riuscita. Verificare che il proxy sia abilitato o che il computer disponga della connessione di rete ai server Live ID.

Spesso questo errore significa che Assistente per l'accesso ai Microsoft Online Services non è in esecuzione. È possibile verificare lo stato di questo servizio eseguendo il comando seguente dal prompt di Windows PowerShell:

    Get-Service "msoidsvc"

Se il servizio non è in esecuzione, avviarlo usando il comando seguente:

    Start-Service "msoidsvc"

Se il servizio è in esecuzione, potrebbero essersi verificati problemi di connessione di rete tra il computer e il server di autenticazione di Microsoft Live ID. Per verificare, aprire Internet Explorer e accedere a <https://login.microsoftonline.com/.> Provare ad accedere a Office 365 da questa pagina. Se l'accesso non riesce, è probabile che ci stiano problemi con la connessione di rete.

Meno frequentemente, può verificarsi che l'URI di connessione per il server di autenticazione di Microsoft Live ID sia stato impostato con un valore errato. Se si è già verificato che l'Assistente per l'accesso è in esecuzione e che non ci sono problemi di rete, questa potrebbe essere la causa del problema. In questo caso, contattare il supporto di Office 365.

## Vedere anche

#### Concetti

[Diagnosi e risoluzione dei problemi di connessione di Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

