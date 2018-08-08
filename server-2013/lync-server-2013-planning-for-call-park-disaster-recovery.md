---
title: "Lync Server 2013: Pianifica ripristino di emergenza del parcheggio"
TOCTitle: Pianificazione per il ripristino di emergenza del parcheggio di chiamata
ms:assetid: f7cf3958-177b-4340-a864-35a6f44d6d88
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205395(v=OCS.15)
ms:contentKeyID: 49302507
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione per il ripristino di emergenza del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-30_

In questa sezione vengono descritti alcuni modi per preparare l' applicazione Parcheggio di chiamata per il ripristino di emergenza e alcune considerazioni relative al processo di ripristino di emergenza.

## Preparazione del ripristino di emergenza di Parcheggio di chiamata

Quando si preparano e si eseguono le procedure di ripristino di emergenza, tenere presenti gli aspetti seguenti:

  - Pianificare il ripristino di emergenza in fase di pianificazione della capacità. Per la capacità del ripristino di emergenza, ogni pool in un pool abbinato deve essere in grado di gestire i carichi di lavoro dei servizi di Parcheggio di chiamata in entrambi i pool. Per informazioni dettagliate sulla pianificazione della capacità di Parcheggio di chiamata, vedere [Pianificazione della capacità per il parcheggio di chiamata in Lync Server 2013](lync-server-2013-capacity-planning-for-call-park.md).

  - Durante il ripristino di emergenza gli utenti che sono stati reindirizzati al pool di backup durante il processo di failover, utilizzano il servizio Parcheggio di chiamata nel pool di backup. Pertanto, il supporto per Parcheggio di chiamata durante il ripristino di emergenza richiede che l' applicazione Parcheggio di chiamata venga distribuita e abilitata sia nel pool primario, sia nel pool di backup.

  - È necessario che tutti i pool dispongano di un intervallo valido di numeri di codici orbit per gli utenti che sono ospitati nel pool da utilizzare per il parcheggio delle chiamate.

  - Tenere sempre una copia di backup distinta della musica in attesa personalizzata che è stata caricata per Parcheggio di chiamata. Questi file non vengono inclusi nel backup durante il processo di ripristino di emergenza di Lync Server 2013 e verranno persi se i file caricati nel pool vengono danneggiati o cancellati.

## Parcheggio di chiamata Considerazioni sul ripristino di emergenza

Per ogni pool è possibile definire un solo set di impostazioni di configurazione dell' applicazione Parcheggio di chiamata e un file audio della musica in attesa personalizzata. Queste impostazioni includono la soglia di timeout, la musica in attesa, il numero massimo di tentativi di risposta alle chiamate e l'URI di timeout. Per visualizzare le impostazioni di configurazione, eseguire il cmdlet **Get-CsCpsConfiguration**. Per informazioni dettagliate sul cmdlet **Get-CsCpsConfiguration**, vedere [Get-CsCpsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCpsConfiguration).

Durante il ripristino di emergenza, Parcheggio di chiamata utilizza l' applicazione Parcheggio di chiamata nel pool di backup, pertanto le impostazioni nel pool primario non sono incluse nel backup. Se non è possibile recuperare il pool primario e si distribuisce un nuovo pool per sostituire il pool primario, le impostazioni del pool primario andranno perse e sarà necessario riconfigurare le impostazioni di Parcheggio di chiamata e i file audio della musica in attesa personalizzata nel nuovo pool.

Se si distribuisce un nuovo pool con un altro nome di dominio completo (FQDN) per sostituire il pool primario, è necessario riassegnare al nome di dominio completo (FQDN) del nuovo pool tutti gli intervalli di codici orbit di Parcheggio di chiamata associati al pool primario. Per riassegnare gli intervalli di codici orbit a un nuovo pool, è possibile utilizzare il Pannello di controllo di Lync Server o il cmdlet **Set-CsCallParkOrbit**. Per informazioni dettagliate sul cmdlet **Set-CsCallParkOrbit**, vedere [Set-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkOrbit).

