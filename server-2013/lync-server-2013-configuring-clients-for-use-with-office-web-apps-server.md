---
title: "Lync Server 2013: Configura i client per utilizzo con Office Web Apps Server"
TOCTitle: Configurazione dei client per l'utilizzo con Office Web Apps Server
ms:assetid: e5eaead7-0b32-42fb-97eb-ca203af59a9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205339(v=OCS.15)
ms:contentKeyID: 49302283
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei client di Lync Server 2013 per l'utilizzo con Office Web Apps Server

 

_**Ultima modifica dell'argomento:** 2013-02-25_

Se si desidera che gli utenti possano usufruire di tutte le funzionalità del server Office Web App, è necessario eseguire l'aggiornamento a Microsoft Lync 2013. Solo gli utenti di Lync 2013 potranno eseguire operazioni come scorrere le diapositive di PowerPoint in modo indipendente rispetto alla presentazione di PowerPoint in corso. (Ciò significa che gli utenti potranno esaminare qualsiasi diapositiva nella presentazione in qualsiasi momento, senza interferire in alcun modo con la presentazione effettiva.) Gli utenti che non dispongono di Lync 2013 saranno comunque in grado di partecipare a conferenze online e visualizzare la presentazione di PowerPoint, ma non potranno scorrere in modo indipendente le diapositive, visualizzare le transizioni delle diapositive o guardare i video incorporati.

Si noti che queste funzionalità saranno sempre disponibili per gli utenti di Lync 2013, anche se il relatore esegue la presentazione di PowerPoint da Microsoft Lync 2010. Se una presentazione di PowerPoint è ospitata da un utente che esegue Lync 2010, Lync Server 2013 si coordinerà con il server Office Web Apps per assicurarsi che gli utenti di Lync 2013 possano visualizzare la versione della presentazione per il server Office Web Apps. Il server Office Web Apps non rende disponibili i servizi di PowerPoint per gli utenti che eseguono client diversi da Lync 2013. Questi utenti potranno invece connettersi al servizio del server per conferenze e visualizzare le presentazioni di PowerPoint con le stesse modalità valide in Microsoft Lync Server 2010. Ciò significa anche che tali utenti avranno accesso solo alle funzionalità più limitate offerte da Lync Server 2010.

Sebbene non siano richiesti interventi di configurazione dei client specifici per il server Office Web Apps (a parte l'aggiornamento a Lync 2013), è consigliabile che i partecipanti alla conferenza eseguano l'aggiornamento a Internet Explorer 9. Anche se le conferenze sono accessibili tramite Internet Explorer 8, per l'utilizzo di questo Web browser sono previste alcune limitazioni. Gli utenti di Internet Explorer 8, ad esempio, non potranno specificare dimensioni personalizzate per il ridimensionamento della finestra di condivisione di PowerPoint, ma dovranno utilizzare una delle tre dimensioni predefinite. Con Internet Explorer 8, inoltre, non sarà possibile riprodurre file multimediali.

