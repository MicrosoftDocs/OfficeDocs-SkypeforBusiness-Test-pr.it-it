---
title: Configurazione delle versioni client supportate
TOCTitle: Configurazione delle versioni client supportate
ms:assetid: aebf7b48-9aa2-4a06-adc5-0c9d11b6358d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412832(v=OCS.15)
ms:contentKeyID: 49301667
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle versioni client supportate

 

_**Ultima modifica dell'argomento:** 2012-12-14_

In Lync Server 2013 è possibile impostare criteri di versione client per specificare le versioni dei client supportati nel proprio ambiente. È inoltre possibile utilizzare la configurazione della versione client globale per specificare un'azione predefinita per i client che non dispongono già di criteri di versione definiti e che pertanto non sono esplicitamente supportati o esclusi.

È inoltre possibile utilizzare i criteri di versione client per gestire gli aggiornamenti client. Quando si impostano i criteri di versione client e si utilizzano le opzioni **Consenti e aggiorna** e **Blocca e aggiorna**, i client riceveranno il software aggiornato da Windows Server Update Service, se si utilizza tale servizio, o da Microsoft Update.

## Impostazioni dei criteri di versione client

In base ai criteri di versione client predefiniti, tutti i client devono eseguire Lync o Microsoft Office Communicator 2007 R2. Se i client nell'ambiente corrente eseguono versioni precedenti di Communicator, può essere necessario riconfigurare le regole Versione client per impedire il blocco o l'aggiornamento imprevisto dei client e dei dispositivi quando si connettono a Lync Server 2013. È possibile modificare la regola predefinita oppure aggiungere una regola più in alto nell'elenco Criteri versione client per ignorare la regola predefinita. Inoltre, con il rilascio di aggiornamenti cumulativi (UC), è necessario configurare i criteri di versione client per richiedere gli aggiornamenti più recenti.

