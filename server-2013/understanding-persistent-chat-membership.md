---
title: Informazioni sull'appartenenza di Chat persistente
TOCTitle: Informazioni sull'appartenenza di Chat persistente
ms:assetid: 900392d6-6e9f-4dae-93d6-39d7474409ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398730(v=OCS.15)
ms:contentKeyID: 49301310
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Informazioni sull'appartenenza di Chat persistente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

L'accesso utente alle chat room di Chat persistente viene gestito in base all'appartenenza; gli utenti devono essere membri di una chat room per poter inviare e leggere messaggi. Solo i **relatori** con un'affiliazione designata alle chat room possono utilizzare la **pubblicazione nelle sale auditorium**. Un auditorium è un tipo di chat room (l'altro è **normale**), in cui solo i relatori possono pubblicare e in cui tutti possono leggere.

Inoltre, le chat room Chat persistente funzionano in base alle regole di una categoria. Per dettagli sulle categorie, vedere [Gestione di categorie, chat room e componenti aggiuntivi in Lync Server 2013](lync-server-2013-managing-categories-rooms-and-add-ins.md) e le sezioni relative al funzionamento degli ambiti delle categorie e alle strategie per le categorie più avanti in questo argomento.

Un amministratore di Chat persistente può creare e gestire categorie di chat room. Nell'ambito della creazione e della gestione di categorie di chat room, l'amministratore di Chat persistente può configurare entità (gruppi, contenitori e utenti di Servizi di dominio Active Directory) con accesso a membri o creatori di chat room di una particolare categoria.

## Servizi di dominio Active Directory e Chat persistente

server Chat persistente si basa su Active Directory per il pool di utenti Chat persistente interni. Dopo aver installato Chat persistente (client), è possibile aggiungere domini di utenti e gruppi di utenti alla categoria di chat room. È quindi possibile aggiungere questi utenti e gruppi all'appartenenza delle categorie di chat room.

> [!IMPORTANT]  
> È necessario assicurarsi che non vi siano nomi di utenti duplicati che desiderano apportare modifiche alle proprie chat room di Chat persistente. Se sono presenti nomi duplicati, modificarli per consentire agli utenti di apportare le modifiche. Se un utente ha nomi duplicati in Active Directory e tenta di apportare modifiche nelle chat room viene visualizzato un messaggio di errore che richiede all'utente di contattare l'amministratore.

## Funzionamento degli ambiti delle categorie

Una categoria specifica tutti gli utenti e gruppi che possono essere membri in un elenco di appartenenza di una chat room Chat persistente in base alla proprietà **AllowedMembers**. Se ad esempio si imposta la proprietà **AllowedMembers** della categoria su contoso.com, è possibile aggiungere qualsiasi gruppo o utente a *Contoso* come membro delle chat room della categoria. Se si imposta la proprietà **AllowedMembers** di una categoria su *Vendite* solo i gruppi e gli utenti di questa lista di distribuzione potranno essere aggiunti come membri delle chat room della categoria. Analogamente la proprietà **Creators** consente di controllare chi può creare le chat room nella categoria. Dopo aver creato una chat room, chiunque appartenga al gruppo di **AllowedMembers** può essere designato come **responsabile** per la gestione delle chat room (ad esempio, modifiche e approvazioni alle appartenenze).

La definizione di **AllowedMembers** e **Creators** per una categoria ha i vantaggi seguenti:

  - Tutte le chat room nella categoria sono vincolate da restrizioni impostate a livello di categoria. È possibile usare questo aspetto per isolare le chat room in base ai criteri di accesso e alle esigenze aziendali.

  - Un utente incluso nell'elenco **Creator** può creare nuove chat room nella categoria. Se si desidera implementare un sistema in cui un numero limitato di persone dell'organizzazione può creare chat room, questo controllo può essere usato per soddisfare tale requisito.

## Strategie per le categorie di chat room

I membri **AllowedMembers** di una categoria devono essere tutti gli utenti che useranno le chat room di Chat persistente della categoria. A seconda dei requisiti di protezione dei dati aziendali e di verifica del livello appropriato di accesso, è possibile definire una o più categorie per specificare chi può cercare e partecipare alle chat room. Se si vuole consentire solo a un determinato set di utenti (un helpdesk centrale o solo i dipendenti a tempo pieno) di creare chat room, è possibile limitare l'ambito di utenti **Creator** di una categoria in modo conseguente.

Le categorie possono essere inoltre usate per creare barriere etiche, le quali impediscono conflitti di interesse in un'organizzazione. Un amministratore può ad esempio creare chat room in una categoria solo per operatori di borsa mentre un'altra categoria può essere riservata agli analisti.


> [!NOTE]
> In Lync Server 2013, server Chat persistente, non sono supportati gli utenti federati. Se sono presenti chat di utenti federati in versioni precedenti di server Chat persistente, ne verrà eseguita la migrazione. Gli utenti federati vengono aggiunti come entità disabilitate.



## Limitazione dei membri a gruppi di utenti

Quando si aggiunge un dominio all'ambito della categoria radice, i gruppi di utenti i cui oggetti gruppo sono inclusi in tale dominio vengono resi disponibili per essere specificati come membri delle chat room nella categoria in questione.

Come regola generale, è consigliabile usare contenitori Active Directory, quali domini e unità organizzative, per definire i membri **AllowedMembers** e **Creators** di una categoria. È possibile aggiungere oggetti di qualsiasi dominio a un elenco **AllowedMembers** o **Creators**. Solo gli oggetti negli elenchi **AllowedMembers** e **Creators** possono essere aggiunti alle chat room nella categoria.

