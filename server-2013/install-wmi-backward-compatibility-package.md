---
title: Installare il pacchetto di compatibilità con le versioni precedenti di WMI
TOCTitle: Installare il pacchetto di compatibilità con le versioni precedenti di WMI
ms:assetid: 38797fbd-06a0-4008-b099-158e7b5d7703
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204816(v=OCS.15)
ms:contentKeyID: 49300205
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare il pacchetto di compatibilità con le versioni precedenti di WMI

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Se si prova ad eseguire l'unione guidata del Generatore di topologie senza installare il pacchetto di compatibilità con le versioni precedenti di WMI, verrà visualizzato l'errore seguente:

![Messaggio di errore WMI](images/JJ204816.a007d2f2-fc85-430c-91eb-382b032469af(OCS.15).jpg "Messaggio di errore WMI")

Se si prova ad eseguire il cmdlet **Merge-CsLegacytopology** senza installare il pacchetto di compatibilità con le versioni precedenti di WMI, verrà visualizzato l'errore seguente:

![Errore del provider WMI in Windows PowerShell](images/JJ204816.c510824e-1807-4c7e-bb28-c6cfea2eac1d(OCS.15).jpg "Errore del provider WMI in Windows PowerShell")

Per installare il pacchetto di compatibilità con le versioni precedenti di WMI

1.  Nel supporto di installazione passare a \\SETUP\\AMD64\\SETUP\\OCSWMIBC.MSI.

2.  Installare OCSWMIBC.MSI.
    
    > [!important]  
    > OCSWMIBC.msi deve essere installato nel computer in cui viene eseguita l'unione guidata del Generatore di topologie. Si consiglia tuttavia di installare OCSWMIBC.msi in tutti i Front End Server della topologia.    
    > [!important]  
    > OCSWMIBC.msi può essere installato in qualsiasi computer del dominio in cui siano installati i componenti di base di Lync Server 2013 e Lync Server 2013 Management Shell e che disponga di accesso alla topologia Office Communications Server 2007 R2 (provider WMI per Active Directory Domain Services (AD DS) e SQL Server).
