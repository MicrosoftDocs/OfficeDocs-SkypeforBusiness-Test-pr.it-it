---
title: 'Lync Server 2013: Configurare dial plan per le conferenze telefoniche con accesso esterno'
TOCTitle: Configurare dial plan per le conferenze telefoniche con accesso esterno
ms:assetid: a3e0958e-384f-43e5-b4c9-686b6ecac7ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412768(v=OCS.15)
ms:contentKeyID: 49301536
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare dial plan per le conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-25_

Quando si distribuisce la funzionalità di conferenza telefonica con accesso esterno, è necessario creare o modificare uno o più dial plan per il routing dei numeri di telefono di accesso esterno. Verificare che almeno una regola di normalizzazione in ogni dial plan converta i numeri di telefono interni in numeri di telefono completi in formato E.164. Gli utenti delle conferenze telefoniche con accesso esterno partecipano alle conferenze come utenti Enterprise autenticati immettendo il PIN e il numero di telefono personali. È necessaria una regola di normalizzazione per convertire i numeri interni in numeri di telefono completi in modo che gli utenti possano essere autenticati quando immettono solo un numero di telefono interno.

Per impostare dial plan per conferenze telefoniche con accesso esterno eseguire le operazioni seguenti:

  - Indipendentemente dal fatto che VoIP aziendale sia distribuito, modificare il dial plan globale per aggiungere un'area di conferenza telefonica con accesso esterno e assicurarsi che sia presente una regola di normalizzazione che converta con precisione i numeri di accesso esterno. Per istruzioni dettagliate, vedere [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md).

  - Se VoIP aziendale non è distribuito, creare dial plan per i numeri di accesso di conferenza telefonica con accesso esterno. Assicurarsi di includere un'area di conferenza telefonica con accesso esterno. Per istruzioni dettagliate, vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md).

  - Se VoIP aziendale è distribuito, modificare i dial plan di VoIP aziendale in base alle esigenze includendo le aree e utilizzando regole di normalizzazione appropriate per i numeri di accesso esterno. Per istruzioni dettagliate, vedere [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md). È inoltre possibile creare dial plan dedicati da utilizzare solo per i numeri di accesso esterno. Per istruzioni dettagliate, vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md).

Per informazioni dettagliate sulla pianificazione delle aree, vedere [Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-dial-in-conferencing-requirements.md) nella documentazione relativa alla pianificazione.

## Argomenti della sezione

  - [Visualizzazione delle informazioni sul dial plan](lync-server-2013-view-dial-plan-information.md)

  - [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)

  - [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md)

  - [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md)

