---
title: "Lync Server 2013: Crea criteri di routing VoIP per utenti di succursali"
TOCTitle: >
  Creare i criteri di routing VoIP per gli utenti di succursali
ms:assetid: 10deca9f-f870-4a42-b25d-e4fc53108658
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398196(v=OCS.15)
ms:contentKeyID: 49299711
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare i criteri di routing VoIP per gli utenti di succursali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-23_

È consigliabile creare un criterio VoIP (Voice Over IP) distinto per gli utenti dei siti derivati. In tale criterio devono essere incluse le route per uscire dal gateway della Survivable Branch Appliance o dal gateway esterno del Survivable Branch Server, nonché le route di riserva per uscire da un gateway del sito centrale. Indipendentemente dalla posizione presso cui è registrato l'utente, ovvero il registrar della Survivable Branch Appliance o del Survivable Branch Server oppure nel cluster del registrar di riserva presso il sito centrale, il criterio VoIP dell'utente viene sempre applicato.

## Per configurare i criteri di routing VoIP per gli utenti dei siti di succursale

1.  Creare un dial plan a livello utente e assegnarlo agli utenti dei siti di succursale. Vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md) nella documentazione relativa alle operazioni.

2.  Assegnare regole di normalizzazione corrispondenti alle abitudini degli utenti del sito in relazione alla composizione dei numeri di telefono. Se l'utente del Survivable Branch Appliance o del Survivable Branch Server esegue il failover sul pool di registrazione di backup del sito centrale, sarà valido lo stesso dial plan. Vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md) nella documentazione relativa alle operazioni.

3.  Configurare una route vocale che esca dal gateway del Survivable Branch Appliance o dal gateway esterno del Survivable Branch Server. Vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md) nella documentazione relativa alle operazioni.

4.  Impostare sul gateway del Survivable Branch Appliance o del Survivable Branch Server una route di chiamata di riserva che punti al pool di registrazione di riserva (collocato con il Mediation Server) nel sito centrale. Vedere la documentazione del fornitore del Survivable Branch Appliance o del Survivable Branch Server.
    

    > [!NOTE]
    > Tale impostazione della route di chiamata di riserva assicura il funzionamento delle chiamate in ingresso per l'utente del sito di succursale quando il Survivable Branch Appliance o il Survivable Branch Server non è disponibile, ad esempio perché è inattivo per attività di manutenzione. Se la funzione di registrazione e il Mediation Server nel Survivable Branch Appliance o nel Survivable Branch Server non sono disponibili e l'utente è registrato nel pool di registrazione di riserva presso il sito centrale, le chiamate in ingresso potranno comunque essere instradate all'utente.



**Passaggio successivo** : [Configurare le impostazioni di rerouting della segreteria telefonica in Lync Server 2013](lync-server-2013-configure-voice-mail-rerouting-settings.md)

