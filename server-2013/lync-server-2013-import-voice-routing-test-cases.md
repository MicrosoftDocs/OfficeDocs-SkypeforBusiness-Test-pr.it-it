---
title: 'Lync Server 2013: Importare test case di routing vocale'
TOCTitle: Importare test case di routing vocale
ms:assetid: 6546e24c-9ad2-428b-92b2-63948ed0f884
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398460(v=OCS.15)
ms:contentKeyID: 49300799
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Importare test case di routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

I test case rappresentano un modo per verificare le route vocali nell'organizzazione. È possibile definire elementi come il numero da chiamare e i criteri dial plan e vocali da utilizzare, quindi Lync Server 2013 può verificare che in tali condizioni il numero specificato possa essere correttamente instradato alla rete PSTN.

I test case, che possono essere creati con il Pannello di controllo di Lync Server, vengono in genere salvati solo nel server in cui il test case viene creato ed eseguito in origine. È comunque possibile esportarli come file XML (con estensione vtest) per poi importarli in altri server. Ciò consente di eseguire gli stessi test in computer diversi in punti diversi della topologia.

## Per importare un test case di routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** .

4.  Scegliere **Importa test case** dal menu **Azioni** .

5.  Trovare il file del test case che si desidera importare (con estensione vtest) e quindi fare clic su **Apri** .

6.  Fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Tutte le volte che si importa un file vtest, è necessario utilizzare il comando <STRONG>Salva tutto</STRONG> per pubblicare il test case. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Esportare test case di routing vocale in Lync Server 2013](lync-server-2013-export-voice-routing-test-cases.md)

