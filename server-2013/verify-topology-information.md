---
title: Verificare le informazioni sulla topologia
TOCTitle: Verificare le informazioni sulla topologia
ms:assetid: aa4c424e-f87c-4be6-8df6-a0cd193b11fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205151(v=OCS.15)
ms:contentKeyID: 49301614
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare le informazioni sulla topologia

 

_**Ultima modifica dell'argomento:** 2012-09-26_

Il primo passaggio per verificare che l'unione sia stata eseguita correttamente consiste nel visualizzare le informazioni della topologia di Office Communications Server 2007 R2 unite a Lync Server 2013. Nel nodo **BackCompatSite** in Generatore di topologie viene visualizzato il nome di dominio completo (FQDN) di ogni server e pool di Office Communications Server 2007 R2 che è stato unito.

## Per visualizzare BackCompatSite in Generatore di topologie

1.  Nell'ambiente Office Communications Server 2007 R2 aprire lo strumento di amministrazione di Office Communications Server 2007 R2 e prendere nota degli FQDN dei pool e dei server legacy.

2.  Nell'ambiente Lync Server 2013 aprire Generatore di topologie e quindi espandere il nodo **BackCompatSite** .

3.  Verificare che siano visualizzati gli FQDN dei pool e dei server da unire.
    

    > [!NOTE]
    > In <STRONG>BackCompatSite</STRONG> non viene visualizzata alcuna informazione per i ruoli del server collocati in un Front End Server o in un server Standard Edition. Vengono visualizzati solo i ruoli del server necessari per l'interoperabilità tra Office Communications Server 2007 R2 e Lync Server 2013.



![Finestra di dialogo per BackCompatSite in Generatore di topologie](images/JJ205243.62751c76-f018-4c6d-bb48-c61ef8974d31(OCS.15).jpg "Finestra di dialogo per BackCompatSite in Generatore di topologie")

Per visualizzare la topologia unita, è anche possibile utilizzare il Pannello di controllo di Lync Server 2013. Nel Pannello di controllo di Lync Server 2013 sono indicati l'FQDN di ogni server e di ogni pool e il nome del sito della topologia unita. Il nome del **Sito** dei server uniti è **BackCompatSite** .

## Per visualizzare la topologia unita nel Pannello di controllo di Lync Server 2013

1.  Aprire il Pannello di controllo di Lync Server 2013.

2.  Fare clic su **Topologia** .

3.  Nella scheda **Stato** verificare che i server e i pool uniti siano visualizzati cercando **BackCompatSite** nella colonna **Sito** .

![Pannello di controllo di Lync Server con unione di topologie](images/JJ205151.f986ddd4-2040-454d-9389-7f6154b59cc9(OCS.15).jpg "Pannello di controllo di Lync Server con unione di topologie")

Per visualizzare altri dettagli su un pool unito, utilizzare il cmdlet **Get-CsPool** . Oltre alle informazioni disponibili in Generatore di topologie e nel Pannello di controllo di Lync Server 2013, questo cmdlet visualizza i servizi eseguiti nel pool di Lync Server 2013.


> [!NOTE]
> Quando si pubblica la topologia dopo l'esecuzione della procedura di unione guidata in Generatore di topologie, le directory conferenze vengono unite a Lync Server 2013. Per verificare le directory conferenze è possibile eseguire il cmdlet <STRONG>Get-CsConferenceDirectory</STRONG>.



## Per visualizzare i servizi in un pool unito

1.  Aprire Lync Server 2013 Management Shell.

2.  Nella riga di comando digitare quanto segue:
    
        Get-CsPool [-Identity <FQDN of the pool>]
    
    Ad esempio:
    
        Get-CsPool -Identity pool02.contoso.net

## Per verificare le directory conferenze unite

1.  Aprire Lync Server 2013 Management Shell.

2.  Nella riga di comando digitare quanto segue:
    
        Get-CsConferenceDirectory

3.  Verificare che tutte le directory conferenze per il pool o il server sottoposte a unione si trovino ora in Lync Server 2013.

