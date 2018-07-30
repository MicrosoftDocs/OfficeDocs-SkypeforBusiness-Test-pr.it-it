---
title: 'Lync Server 2013: Configurare il controllo di ammissione di chiamata'
TOCTitle: Configurare il controllo di ammissione di chiamata
ms:assetid: ce3e6e71-1e33-4cff-849a-c0468e61fef6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398870(v=OCS.15)
ms:contentKeyID: 49302020
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il controllo di ammissione di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Il servizio Controllo di ammissione di chiamata è una soluzione che determina se è possibile stabilire una sessione in tempo reale in base alla larghezza di banda disponibile per evitare di fornire una qualità audio/video scadente per gli utenti su reti congestionate. Questo servizio controlla il traffico in tempo reale solo per audio e video e non ha effetto sul traffico di dati. Controllo di ammissione di chiamata può instradare la chiamata attraverso un percorso Internet qualora la larghezza di banda del percorso WAN predefinito non sia sufficiente. Per informazioni dettagliate, vedere [Pianificazione del servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-planning-for-call-admission-control.md) nella documentazione relativa alla pianificazione.

In questa sezione è contenuto un set di procedure di esempio che illustrano in che modo distribuire e gestire Controllo di ammissione di chiamata nella rete.

> [!IMPORTANT]  
> Prima di distribuire il servizio Controllo di ammissione di chiamata, è necessario raccogliere tutte le informazioni necessarie per la topologia di rete aziendale, come descritto in <a href="lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md">Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013</a> nella documentazione relativa alla pianificazione. Verificare inoltre che i componenti di Controllo di ammissione di chiamata siano stati installati e attivati, come descritto in <a href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013</a> nella documentazione relativa alla distribuzione.


> [!NOTE]
> Tutti gli esempi di distribuzione e gestione di Controllo di ammissione di chiamata in questa sezione vengono eseguiti tramite Lync Server Management Shell. In alternativa, è anche possibile fare riferimento alla sezione relativa alla configurazione di rete del Pannello di controllo di Lync Server per la gestione di questo servizio.



## Argomenti della sezione

  - [Configurare le aree di rete per il servizio Controllo di ammissione di chiamata](lync-server-2013-configure-network-regions-for-cac.md)

  - [Creare profili di criteri di larghezza di banda](lync-server-2013-create-bandwidth-policy-profiles.md)

  - [Configurare siti di rete per il servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-configure-network-sites-for-cac.md)

  - [Associare subnet a siti di rete per il servizio Controllo di ammissione di chiamata](lync-server-2013-associate-subnets-with-network-sites-for-cac.md)

  - [Creare collegamenti di aree di rete](lync-server-2013-create-network-region-links.md)

  - [Creare route tra aree di rete](lync-server-2013;-create-network-interregion-routes.md)

  - [Creare criteri intrasito di rete in Lync Server 2013](lync-server-2013-create-network-intersite-policies.md)

  - [Abilitare il servizio Controllo di ammissione di chiamata](lync-server-2013-enable-call-admission-control.md)

  - [Elenco di controllo per la distribuzione del servizio Controllo di ammissione di chiamata](lync-server-2013-call-admission-control-deployment-checklist.md)

