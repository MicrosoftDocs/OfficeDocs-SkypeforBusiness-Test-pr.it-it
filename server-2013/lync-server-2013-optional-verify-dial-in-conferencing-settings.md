---
title: 'Lync Server 2013: (Facoltativo) Verificare le impostazioni delle conferenze telefoniche con accesso esterno'
TOCTitle: (Facoltativo) Verificare le impostazioni delle conferenze telefoniche con accesso esterno
ms:assetid: a85efdda-97b0-4f3b-bd26-04416bee8ef5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412789(v=OCS.15)
ms:contentKeyID: 49301595
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (Facoltativo) Verificare le impostazioni delle conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2010-11-02_

Come verifica finale della configurazione delle conferenze telefoniche con accesso esterno, è possibile cercare dial plan con un'area di conferenza telefonica con accesso esterno non utilizzata da alcun numero di accesso e numeri di telefono per i quali non è specificata un'area di conferenza telefonica con accesso esterno. Questo passaggio è facoltativo.

## Per trovare dial plan con un'area di conferenza telefonica con accesso esterno non utilizzata da alcun numero di accesso

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente al prompt:
    
        Get-CsDialinConferencingAccessNumber -EmptyRegion
    
    Questo cmdlet restituisce tutti i dial plan con un'area di conferenza telefonica con accesso esterno non utilizzata da alcun numero di accesso.

## Per trovare numeri di accesso senza aree assegnate

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente al prompt:
    
        Get-CsDialinConferencingAccessNumber -Region NULL
    
    Questo cmdlet restituisce tutti i numeri di accesso per conferenze telefoniche con accesso esterno non associati ad alcuna area.

