---
title: 'Lync Server 2013: Controllo delle chiamate remote e normalizzazione dei numeri di telefono'
TOCTitle: Controllo delle chiamate remote e normalizzazione dei numeri di telefono
ms:assetid: 291d9e87-4c65-4ea2-888f-517741391de5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558630(v=OCS.15)
ms:contentKeyID: 49299999
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Controllo delle chiamate remote e normalizzazione dei numeri di telefono in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

I client di Lync scaricano le regole di normalizzazione dei numeri di telefono durante il download dei file del servizio Rubrica. Negli scenari con controllo delle chiamate remote le regole di normalizzazione dei numeri di telefono del servizio Rubrica vengono applicate sia alle chiamate in arrivo che alle chiamate in uscita con tale controllo abilitato. Per le chiamate in arrivo dirette a un utente abilitato per l'utilizzo del controllo delle chiamate remote, il numero di telefono del chiamate viene innanzitutto normalizzato nel formato E.164 dal gateway SIP/CSTA o dal centralino (PBX). Quando Lync Server 2013 riceve la chiamata dal gateway, esegue una ricerca inversa da numero (RNL, Reverse Number Lookup) confrontando il numero del chiamante con il numero normalizzato presente nell'elenco Contatti di Microsoft Office Outlook del destinatario della chiamata o nell'elenco indirizzi globale archiviato nel servizio Rubrica. Se tale ricerca trova una corrispondenza, il chiamante viene identificato in base al nome nella notifica della chiamata in arrivo.

Per le chiamate in uscita con controllo delle chiamate remote, prima di instradare la chiamata al gateway SIP/CSTA Lync applica le regole di normalizzazione dei numeri di telefono del servizio Rubrica al numero che è stato composto.

Per informazioni dettagliate sulla creazione delle regole di normalizzazione dei numeri di telefono per il controllo delle chiamate remote, vedere [Dial plan e regole di normalizzazione in Lync Server 2013](lync-server-2013-dial-plans-and-normalization-rules.md) nella documentazione relativa alla pianificazione.

## Migrazione delle regole di normalizzazione dei numeri di telefono

Se si esegue la migrazione di utenti precedentemente abilitati per il controllo delle chiamate remote, vedere gli argomenti seguenti nella documentazione relativa alla migrazione:

  - Per Lync Server 2010, vedere [Eseguire la migrazione della rubrica](migrate-address-book.md) nella documentazione relativa alla migrazione.

  - Per Communications Server 2007 R2, vedere [Eseguire la migrazione della rubrica](migrate-address-book_1.md) nella documentazione relativa alla migrazione.

