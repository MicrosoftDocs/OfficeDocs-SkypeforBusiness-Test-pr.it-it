---
title: 'Lync Server 2013: Creazione di record DNS per il servizio di individuazione automatica'
TOCTitle: Creazione di record DNS per il servizio di individuazione automatica
ms:assetid: 3756ffe4-c6b1-492d-850e-42a832e06567
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690010(v=OCS.15)
ms:contentKeyID: 49300171
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione di record DNS per il servizio di individuazione automatica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-20_

Gli utenti di Lync Mobile dovranno abilitare l'individuazione automatica e parte del processo implica la creazione di alcuni record DNS (Domain Name System). A seconda delle esigenze sono necessari:

  - Un record DNS interno per supportare gli utenti mobili che si connettono dall'interno della rete dell'organizzazione.

  - Un record esterno, o pubblico, per supportare gli utenti di dispositivi mobili che si connettono da Internet

È necessario creare sia un record DNS interno che un record DNS esterno per ogni dominio SIP.

I record DNS creati possono essere record A (host) o record CNAME. Per facilitare l'operazione, nelle procedure riportate di seguito viene descritto in dettaglio come creare questi record DNS interni ed esterni. Se servono altre informazioni sui requisiti DNS per gli utenti mobili, vedere [Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md).

## Creazione di un record CNAME DNS interno

1.  Per creare un record DNS interno, eseguire l'accesso a un server DNS della rete con un account di dominio membro del gruppo Domain Admins o DnsAdmins.

2.  Aprire lo snap-in amministrativo DNS. A tale scopo, fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi fare clic su **DNS** .

3.  Nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio di Active Directory in cui sono installati il pool di server Director e il pool Front End di Lync Server 2013, ad esempio, contoso.local.

4.  Controllare per verificare se esiste un record host A (AAAA per IPv6) per il pool di server Director per un record DNS interno. Dovrebbe esistere un record host A per il nome di dominio completo (FQDN) dei servizi Web interni per il pool di server Director (ad esempio, lyncwebdir01.contoso.local). Se non esiste, è possibile che non si stia utilizzando un pool di server Director e in questo caso sarà necessario usare il nome FQDN del pool Front End oppure l'FQDN di un singolo server, se questa è la configurazione in uso.

5.  Tenendo presente tutto ciò, controllare per verificare se esiste un record host A (AAAA per IPv6) per il pool Front End per un record DNS interno. Dovrebbe esistere un record host A (o AAAA) per il nome di dominio completo (FQDN) dei servizi Web interni per il pool Front End (ad esempio, lyncwebpool01.contoso.local). Se non esiste, è necessario prendere nota dell'FQDN del Front End Server o del server Standard Edition.

6.  Quando sono noti i record host A (o AAAA) esistenti, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.

7.  Fare clic con il pulsante destro del mouse sul nome del dominio SIP e quindi scegliere **Nuovo alias (CNAME)** .

8.  In **Nome alias** digitare lyncdiscoverinternal come nome host per l'URL del servizio di individuazione automatica interno.

9.  In **Nome di dominio completo (FQDN) per host destinazione** digitare o selezionare l'FQDN dei servizi Web interni del pool di server Director, ad esempio lyncwebdir01.contoso.local, quindi fare clic su **OK** .

10. È necessario creare un nuovo record CNAME di individuazione automatica nella zona di ricerca diretta di ogni dominio SIP supportato nell'ambiente Lync Server 2013.

## Creazione di un record CNAME DNS esterno

1.  Per creare un record CNAME DNS esterno sarà necessario connettersi al provider DNS pubblico e quindi seguire le istruzioni. Non possiamo descrivere con precisione la procedura nell'ambiente del provider DNS, perché possono esistere modi diversi per gestire il DNS esterno, ma speriamo che le indicazioni siano di aiuto.

2.  Accedere al provider DNS esterno con un account autorizzato a creare record DNS in tale ambiente.

3.  Dovrebbe esistere già un dominio SIP creato per tale ambiente. Espandere **Zona di ricerca diretta** per il dominio SIP oppure selezionarlo in altro modo, a seconda dell'interfaccia in uso per il DNS esterno.

4.  Dovrebbe essere già visibile un record host A (AAAA per IPv6) per il pool di server Director (ad esempio, lyncwebexdir01.contoso.com), quindi verificare che esista. Se non è disponibile, è possibile che non sia stia utilizzando un pool di server Director. In questo caso, sarà necessario usare l'FQDN del pool Front End oppure del server Front End o del server Standard Edition se si esegue la procedura per un singolo server.

5.  Sarà inoltre necessario verificare che esista un record host A (AAAA per IPv6) per il nome di dominio completo (FDMN) dei servizi Web esterni per il pool Front End (ad esempio, lyncwebextpool01.contoso.com) oppure un FQDN per il server singolo, nel caso non sia disponibile un pool Front End. Come indicato nel passaggio precedente, questo sarà necessario se non esiste un pool di server Director.

6.  A questo punto, nel formato appropriato per il provider DNS esterno, scegliere l'opzione per creare un **Nuovo alias (CNAME)** (potrebbe trattarsi di un'opzione di menu o di un collegamento, a seconda del formato del provider DNS).

7.  Dovrebbe esistere qualcosa di simile a una casella di testo **Nome alias**, come per il DNS interno. È necessario immettere lyncdiscover come nome host per l'URL del servizio di individuazione automatica esterno.

8.  Dovrebbe esistere anche una casella di testo simile a **Nome di dominio completo (FQDN) per host destinazione**, nella quale immettere l'FQDN dei servizi Web esterni per il pool di server Director (ad esempio, lyncwebexdir01.contoso.com). Fare poi clic su OK o eseguire qualsiasi azione prevista dal DNS esterno per confermare la creazione di questa voce. Come indicato nel passaggio 4 di sopra, se non è disponibile un pool di server Director, sarà necessario usare l'FQDN del pool Front End o l'FQDN del server singolo configurati, in modo appropriato.

9.  Sarà necessario creare un nuovo record CNAME di individuazione automatica nella zona di ricerca diretta di ogni dominio SIP supportato nell'ambiente Lync 2013.

## Creazione di un record A DNS interno

1.  Per creare un record DNS interno, eseguire l'accesso a un server DNS della rete con un account di dominio membro del gruppo Domain Admins o DnsAdmins.

2.  Aprire lo snap-in amministrativo DNS. A tale scopo, fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi fare clic su **DNS** .

3.  Per un record DNS interno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio Active Directory, ad esempio contoso.local, in cui sono installati il pool Server Director e il pool Front End di Lync Server 2013.

4.  Controllare per verificare se esiste un record host A (AAAA per IPv6) per il pool di server Director per un record DNS interno. Dovrebbe esistere un record host A per il nome di dominio completo (FQDN) dei servizi Web interni per il pool di server Director (ad esempio, lyncwebdir01.contoso.local). Se non esiste, è possibile che non si stia utilizzando un pool di server Director e in questo caso sarà necessario usare l'indirizzo IP del pool Front End oppure l'indirizzo IP di un singolo server, se questa è la configurazione in uso.

5.  Tenendo presente tutto ciò, controllare per verificare se esiste un record host A (AAAA per IPv6) per il pool Front End per un record DNS interno. Dovrebbe esistere un record host A (o AAAA) per il nome di dominio completo (FQDN) dei servizi Web interni per il pool Front End (ad esempio, lyncwebpool01.contoso.local). Se non esiste, è necessario prendere nota dell'indirizzo IP del Front End Server o del server Standard Edition.

6.  Quando sono noti i record host A (o AAAA) esistenti, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.

7.  Fare clic con il pulsante destro del mouse sul nome del dominio SIP e quindi scegliere **Nuovo host (A o AAAA)** .

8.  In **Nome** digitare lyncdiscoverinternal come nome host per l'URL del servizio di individuazione automatica interno.

9.  In **Indirizzo IP** digitare l'indirizzo IP del Server Director oppure, se si utilizza un sistema di bilanciamento del carico, digitare l'IP virtuale del sistema di bilanciamento del carico di Server Director. Come indicato nel passaggio 4 di sopra, se non si usa un Server Director potrebbe essere necessario immettere l'indirizzo IP del Front End Server o del server Standard Edition. Se invece si usa un sistema di bilanciamento del carico, digitare l'indirizzo IP virtuale del sistema di bilanciamento del carico del pool Front End.

10. Fare clic su **Aggiungi host** e quindi su **OK** .

11. Per creare un record A o AAAA aggiuntivo, ripetere i passaggi da 8 a 10, tenendo presente che sarà necessario creare nuovi record A o AAAA di individuazione automatica nella zona di ricerca diretta di ogni dominio SIP supportato nell'ambiente Lync Server 2013.

12. Dopo aver terminato di creare i record A (per IPv6, AAAA), fare clic su **Fine** .

## Creazione di un record A DNS esterno

1.  Per creare un record DNS, connettersi al provider DNS pubblico e quindi seguire le istruzioni. Non possiamo descrivere con precisione la procedura nell'ambiente del provider DNS, perché possono esistere modi diversi per gestire il DNS esterno, ma speriamo che le indicazioni siano di aiuto.

2.  Sarà necessario eseguire l'accesso con un account autorizzato a creare record DNS in tale ambiente.

3.  Per un record DNS esterno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.

4.  Dovrebbe essere già visibile un record host A (AAAA per IPv6) per il pool di server Director (ad esempio, lyncwebexdir01.contoso.com), quindi verificare che esista e qual è l'indirizzo IP. Se non è disponibile, è possibile che non sia stia utilizzando un pool di server Director. In questo caso, sarà necessario usare l'indirizzo IP del pool Front End oppure del server Front End o del server Standard Edition se si esegue la procedura per un singolo server. Tenere presente che i server potrebbero essere gestiti da un sistema di bilanciamento del carico oppure utilizzare un proxy inverso. Prendere nota degli indirizzi IP per eseguire i passaggi di seguito.

5.  Sarà inoltre necessario verificare che esista un record host A (AAAA per IPv6) per il nome di dominio completo (FDMN) dei servizi Web esterni per il pool Front End (ad esempio, lyncwebextpool01.contoso.com) oppure un indirizzo IP per l'installazione di Lync a server singolo, nel caso non sia disponibile un pool Front End. Come indicato nel passaggio precedente, questo sarà necessario se non esiste un pool di server Director.

6.  A questo punto, nel formato appropriato per il provider DNS esterno, scegliere l'opzione per creare un **Nuovo host (A o AAAA)** (potrebbe trattarsi di un'opzione di menu o di un collegamento, a seconda del formato del provider DNS).

7.  Dovrebbe essere disponibile una posizione in cui immettere un **Nome**. Digitare lyncdiscover come nome host per l'URL del servizio di individuazione automatica esterno.

8.  Dovrebbe esistere anche una casella di testo **Indirizzo IP**, nella quale immettere l'IP del pool di server Director (ad esempio, lyncwebexdir01.contoso.com) o l'IP del sistema di bilanciamento del carico del pool (oppure l'IP di un proxy inverso con la stessa destinazione). Fare poi clic su OK o eseguire qualsiasi azione prevista dal DNS esterno per confermare la creazione di questa voce. Come indicato nel passaggio 4 di sopra, se non è disponibile un pool di server Director, sarà necessario usare l'indirizzo IP del pool Front End o l'indirizzo IP del server singolo configurati, in modo appropriato.

9.  Sarà necessario creare un nuovo record A o AAAA di individuazione automatica nella zona di ricerca diretta di ogni dominio SIP supportato nell'ambiente Lync 2013.

