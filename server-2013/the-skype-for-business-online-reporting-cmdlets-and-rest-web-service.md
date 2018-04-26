---
title: 'Lync Online: cmdlet per la creazione di report di Lync Online e servizio Web REST'
TOCTitle: Cmdlet per la creazione di report di Lync Online e servizio Web REST
ms:assetid: cadd73a7-c08a-4102-b73a-ccb3ad4987bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362845(v=OCS.15)
ms:contentKeyID: 56269979
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet per la creazione di report di Lync Online e servizio Web REST

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Insieme alle funzionalità per la creazione di report, Skype for Business online offre l'accesso a cinque cmdlet di Windows PowerShell che facilitano la generazione dei report stessi e possono essere usati dagli amministratori per restituire dati di reporting personalizzati. Skype for Business online include anche il servizio REST (Representational State Transfer), che può essere usato dagli sviluppatori per recuperare informazioni di reporting personalizzate.

I cmdlet per la creazione di report disponibili per gli amministratori includono:

  - Get-CsActiveUserReport, che fornisce informazioni sul numero di utenti attivi (ossia gli utenti che hanno effettuato l'accesso a Skype for Business online e hanno partecipato ad almeno una conferenza o a una sessione di comunicazione peer-to-peer).

  - Get-CsAVConferenceTimeReport, che fornisce informazioni sulla quantità di tempo (in minuti) impiegata dagli utenti in audioconferenze o videoconferenze.

  - Get-CsConferenceReport, che fornisce informazioni sul numero e il tipo di conferenze a cui gli utenti hanno partecipato.

  - Get-CsP2PAVTimeReport, che fornisce informazioni sulla quantità di tempo (in minuti) impiegata dagli utenti in sessioni peer-to-peer con caratteristiche audio e/o video.

  - Get-CsP2PSessionReport, che fornisce informazioni sul numero e il tipo di sessioni peer-to-peer a cui gli utenti hanno partecipato.

Gli amministratori usano per lo più i report disponibili nell'interfaccia di amministrazione di Office 365: si tratta di report generati automaticamente che forniscono una rappresentazione grafica dei dati spesso più facile da interpretare rispetto ai valori numerici non elaborati restituiti dai cmdlet per la creazione di report. Tuttavia, gli amministratori che hanno familiarità con Windows PowerShell possono usare i cmdlet per la creazione di report per restituire dati che non vengono resi tempestivamente disponibili dai report di Lync Online. Ad esempio, i cmdlet per la creazione di report restituiscono informazioni sulla durata delle sessioni (la durata in minuti di ogni sessione). Le durate delle sessioni individuali non vengono restituite dai report di Lync Online. Allo stesso modo, in visualizzazione giornaliera i report di Lync Online visualizzano informazioni solo per i 14 giorni precedenti. Se si ha bisogno di analizzare i totali giornalieri di un altro giorno (ad esempio un giorno di quattro mesi fa), è possibile farlo mediante i cmdlet per la creazione di report.

Gli amministratori possono inoltre consultare l'articolo [Usare Excel per recuperare dati di report Office 365](http://technet.microsoft.com/it-it/library/dn781442.aspx), in cui viene spiegato come usare la funzionalità di recupero dati OData in Microsoft Excel per creare report di Office 365 personalizzati. I report personalizzati consentono di stabilire la tipologia e la quantità dei dati restituiti dal servizio di creazione report di Office 365. I report personalizzati consentono inoltre di specificare la modalità di ordinamento e raggruppamento dei dati, nonché di accedere alle informazioni non disponibili nell'interfaccia di amministrazione di Office 365.

Gli amministratori con esperienza di sviluppo possono usare il servizio Web REST per ottenere informazioni non visualizzate nell'interfaccia di amministrazione di Skype for Business online. Il servizio REST è simile al servizio SOAP, in quanto entrambi consentono di trasferire dati XML tra un client e un server. Il servizio REST, tuttavia, presenta almeno due vantaggi rispetto al servizio SOAP. Per prima cosa, REST esegue i trasferimenti di dati XML mediante un formato standard noto come ATOM Syndication Format, mentre SOAP usa un formato non standard. Inoltre, REST supporta il trasferimento dei dati attraverso reti che bloccano i verbi HTTP diversi da GET e POST.

## Vedere anche

#### Concetti

[Creazione di report di Lync Online](https://technet.microsoft.com/it-it/library/dn362827\(v=ocs.15\))  

#### Ulteriori risorse

[Servizio Web gestione rapporti di Office 365](http://msdn.microsoft.com/en-us/library/office/jj984325.aspx)  
[Informazioni sul servizio Web gestione rapporti di Office 365](http://msdn.microsoft.com/en-us/library/office/jj984321.aspx)  
[Cmdlet di gestione rapporti di Exchange Online](http://technet.microsoft.com/en-us/library/jj200780\(v=exchg.150\).aspx)  
[Usare Excel per recuperare dati di report Office 365](http://technet.microsoft.com/it-it/library/dn781442.aspx)

