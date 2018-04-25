---
title: 'Lync Server 2013: Elenco di controllo di distribuzione per i trunk SIP'
TOCTitle: Elenco di controllo di distribuzione per i trunk SIP
ms:assetid: 94f4f03e-19d5-4198-92be-e4076dbb959a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398755(v=OCS.15)
ms:contentKeyID: 49301368
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per i trunk SIP per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Prima di distribuire un trunk SIP, è necessario scambiare con il provider del servizio alcune informazioni di connessione di base sui rispettivi endpoint di trunk SIP.

Ottenere le informazioni seguenti per ogni gateway ITSP (Internet Telephony Service Provider, provider di servizi di telefonia Internet) al quale si eseguirà la connessione:

  - Indirizzo IP

  - Nome di dominio completo (FQDN)


> [!NOTE]
> Il provider di servizi potrebbe chiedere di eseguire la connessione a più gateway ITSP. In tal caso, è necessario configurare una connessione tra ogni gateway ITSP e ogni Mediation Server del pool.



Le informazioni fornite al provider di servizi variano in base al tipo di connessione trunk SIP:

  - Per le connessioni MPLS (Multiprotocol Label Switching) o a reti private, fornire all'ITSP l'indirizzo IP instradabile pubblicamente del router nella rete perimetrale, denominata anche DMZ o subnet schermata. Verificare che il gateway o il Session Border Controller dell'ITSP sia in grado di raggiungere tale indirizzo. Fornire inoltre all'ITSP il nome di dominio completo (FQDN) del Mediation Server.

  - Per le connessioni VPN, fornire all'ITSP l'indirizzo IP del server VPN.

## Considerazioni sui certificati

Per determinare se è necessario un certificato per il trunking SIP, verificare i protocolli supportati con l'ITSP:

1.  Se l'ITSP supporta solo TCP, non è necessario un certificato.

2.  Se supporta TLS, l'ITSP dovrà fornire un certificato.


> [!NOTE]
> Il protocollo SIP funziona in combinazione con RTP o SRTP, i protocolli che gestiscono gli effettivi dati vocali nelle chiamate VoIP.



## Processo di distribuzione

Per implementare il lato Lync Server di una connessione trunk SIP, eseguire la procedura seguente:

1.  Utilizzando il Lync Server  Generatore di topologie, creare e configurare la topologia del dominio SIP. Per informazioni dettagliate, vedere " [Definire e configurare una topologia in Generatore di topologie per Lync Server 2013](lync-server-2013-define-and-configure-a-topology-in-topology-builder.md)" nella documentazione relativa alla distribuzione.

2.  Utilizzando il Pannello di controllo di Lync Server, configurare il routing vocale per il nuovo dominio SIP. Per informazioni dettagliate, vedere " [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md)" nella documentazione relativa alla distribuzione.

3.  Testare la connettività utilizzando il cmdlet **Test-CsPstnOutboundCall**. Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell o la Guida di Lync Server Management Shell.

