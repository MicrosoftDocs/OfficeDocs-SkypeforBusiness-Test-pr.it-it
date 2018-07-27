---
title: Configurazione di DNS per l'individuazione automatica
TOCTitle: Configurazione di DNS per l'individuazione automatica
ms:assetid: f07a634c-3cf3-4958-8556-84596319ef54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945656(v=OCS.15)
ms:contentKeyID: 52062470
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di DNS per l'individuazione automatica

 

_**Ultima modifica dell'argomento:** 2012-12-12_

Per supportare l'individuazione automatica per client di Lync, è necessario creare i record DNS (Domain Name System) seguenti:

  - Un record DNS interno per supportare i client di Lync che effettuano la connessione dall'interno della rete dell'organizzazione

  - Un record DNS esterno, o pubblico, per supportare i client di Lync che effettuano la connessione da Internet

È necessario creare un record DNS interno e un record DNS esterno per ogni dominio SIP.

I record DNS possono essere record A (host) o record CNAME, in base alla possibilità di creare nuovi certificati con nomi soggetto alternativi (SAN) aggiuntivi. Se non si è in grado di richiedere e distribuire un nuovo certificato esterno (pubblico) con SAN lyncdiscover.\<nome dominio\> SAN, utilizzare la procedura per l'uso della porta HTTP/TCP 80. Nelle procedure riportate di seguito viene descritto come creare record DNS interni ed esterni.

## Per creare record CNAME DNS

1.  Eseguire l'accesso a un server DNS come indicato di seguito:
    
      - Per creare un record DNS interno, eseguire l'accesso a un server DNS della rete come membro del gruppo Domain Admins o DnsAdmins.
    
      - Per creare un record DNS esterno, connettersi al provider DNS pubblico.

2.  Aprire lo snap-in amministrativo DNS. A tale scopo, fare clic sul pulsante **Start**, scegliere **Strumenti di amministrazione** e quindi fare clic su **DNS**.

3.  Eseguire una delle operazioni seguenti:
    
      - Per un record DNS interno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio Active Directory, ad esempio contoso.local.
        

        > [!NOTE]
        > Si tratta del dominio Active Directory in cui sono installati il pool di server Lync Server 2013Server Director e il pool Front End.

    
      - Per un record DNS esterno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.

4.  Verificare che esista un record host A per il pool di server Director, come indicato di seguito:
    
      - Per un record DNS interno, deve esistere un record host A per il nome di dominio completo (FQDN) dei servizi Web interni del pool di server Director, ad esempio lyncwebdir01.contoso.local.
    
      - Per un record DNS esterno, deve esistere un record host A per l'FQDN dei servizi Web esterni del pool di server Director, ad esempio lyncwebextdir.contoso.com.

5.  Verificare che esista un record host A per il pool Front End, come indicato di seguito:
    
      - Per un record DNS interno, deve esistere un record host A per l'FQDN dei servizi Web interni del pool Front End, ad esempio lyncwebpool01.contoso.local.
    
      - Per un record DNS esterno, deve esistere un record host A per l'FQDN dei servizi Web esterni del pool Front End, ad esempio lyncwebextpool01.contoso.com.

6.  Per un record DNS interno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.
    

    > [!NOTE]
    > Se si desidera creare un record DNS esterno, l'espansione di <STRONG>Zone di ricerca diretta</STRONG> per il dominio SIP è stata già eseguita al passaggio 3.



7.  Fare clic con il pulsante destro del mouse sul nome del dominio SIP e quindi scegliere **Nuovo alias (CNAME)**.

8.  In **Nome alias** digitare uno dei nomi seguenti:
    
      - Per un record DNS interno, digitare lyncdiscoverinternal come nome host per l'URL del servizio di individuazione automatica interno.
    
      - Per un record DNS esterno, digitare lyncdiscover come nome host per l'URL del servizio di individuazione automatica esterno.

9.  In **Nome di dominio completo (FQDN) per host destinazione** eseguire una delle operazioni seguenti:
    
      - Per un record DNS interno, digitare o selezionare l'FQDN dei servizi Web interni del pool di server Director, ad esempio lyncwebdir01.contoso.local, e quindi fare clic su **OK**.
    
      - Per un record DNS esterno, digitare o selezionare l'FQDN dei servizi Web esterni del pool di server Director, ad esempio lyncwebextdir.contoso.com, e quindi fare clic su **OK**.
    

    > [!NOTE]
    > Se non si utilizza un Server Director, utilizzare l'FQDN dei servizi Web interni ed esterni del pool Front End oppure, nel caso di un server singolo, l'FQDN del Front End Server o del server Standard Edition.

    
    > [!IMPORTANT]  
    > È necessario creare un nuovo record CNAME di individuazione automatica nella zona di ricerca diretta di ogni dominio SIP supportato nell'ambiente Lync Server 2013.

## Per creare record A DNS

1.  Eseguire l'accesso a un server DNS come indicato di seguito:
    
      - Per creare un record DNS interno, eseguire l'accesso a un server DNS della rete come membro del gruppo Domain Admins o DnsAdmins.
    
      - Per creare un record DNS esterno, connettersi al provider DNS pubblico o a un server DNS esterno.

2.  Aprire lo snap-in amministrativo DNS. A tale scopo, fare clic sul pulsante **Start**, scegliere **Strumenti di amministrazione** e quindi fare clic su **DNS**.

3.  Eseguire una delle operazioni seguenti:
    
      - Per un record DNS interno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio Active Directory, ad esempio contoso.local.
        

        > [!NOTE]
        > Si tratta del dominio Active Directory in cui sono installati il pool di server Lync Server 2013Server Director e il pool Front End.

    
      - Per un record DNS esterno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.

4.  Verificare che esista un record host A (per IPv6, AAAA) per il pool di server Director, come indicato di seguito:
    
      - Per un record DNS interno, deve esistere un record host A (per IPv6, AAAA) per l'FQDN dei servizi Web interni del pool di server Director, ad esempio lyncwebdir01.contoso.local.
    
      - Per un record DNS esterno, deve esistere un record host A (per IPv6, AAAA) per l'FQDN dei servizi Web interni del pool di server Director, ad esempio lyncwebextdir.contoso.com.

5.  Verificare che esista un record host A (per IPv6, AAAA) per il pool Front End, come indicato di seguito:
    
      - Per un record DNS interno, deve esistere un record host A (per IPv6, AAAA) per l'FQDN dei servizi Web interni del pool Front End, ad esempio lyncwebpool01.contoso.local.
    
      - Per un record DNS esterno, deve esistere un record host A per l'FQDN dei servizi Web esterni del pool Front End, ad esempio lyncwebextpool01.contoso.com.

6.  Per un record DNS interno, nell'albero della console del server DNS espandere **Zone di ricerca diretta** per il dominio SIP, ad esempio contoso.com.
    

    > [!NOTE]
    > Se si desidera creare un record DNS esterno, l'espansione di <STRONG>Zone di ricerca diretta</STRONG> per il dominio SIP è stata già eseguita al passaggio 3.



7.  Fare clic con il pulsante destro del mouse sul nome del dominio SIP e quindi scegliere **Nuovo host (A o AAAA)**.

8.  In **Nome** digitare il nome host come indicato di seguito:
    
      - Per un record DNS interno, digitare lyncdiscoverinternal come nome host per l'URL del servizio di individuazione automatica interno.
    
      - Per un record DNS esterno, digitare lyncdiscover come nome host per l'URL del servizio di individuazione automatica esterno.
    

    > [!NOTE]
    > Il nome di dominio viene dedotto in base alla zona in cui è definito il record e non è necessario pertanto immetterlo come parte del record A.



9.  In **Indirizzo IP** digitare l'indirizzo IP come indicato di seguito:
    
      - Per un record DNS interno, digitare l'indirizzo IP dei servizi Web interni del Server Director oppure, se si utilizza un dispositivo o un sistema di bilanciamento del carico, digitare l'IP virtuale del dispositivo o del sistema di bilanciamento del carico di Server Director.
        

        > [!NOTE]
        > Se non si utilizza un Server Director, digitare l'indirizzo IP del Front End Server o del server Standard Edition oppure, se si utilizza un dispositivo o un sistema di bilanciamento del carico, digitare l'IP virtuale del dispositivo o del sistema di bilanciamento del carico del pool Front End.

    
      - Per un record DNS esterno, digitare l'indirizzo IP esterno o pubblico del proxy inverso.

10. Fare clic su **Aggiungi host** e quindi su **OK**.

11. Per creare un record A aggiuntivo, ripetere i passaggi da 8 a 10.
    
    > [!IMPORTANT]  
    > È necessario creare un nuovo record lyncdiscover e record A lyncdiscoverinternal nell'area di ricerca diretta di ogni dominio SIP supportato nell'ambiente di Lync Server 2013.

12. Dopo aver terminato di creare i record A (per IPv6, AAAA), fare clic su **Fine**.

