---
title: "Lync Server 2013: Creare un Record DNS SRV per l'integrazione con la messaggistica unificata di Exchange ospitata"
TOCTitle: Creare un Record DNS SRV per l'integrazione con la messaggistica unificata di Exchange ospitata
ms:assetid: 8ea590ae-58ea-4ca5-9853-e0708b3ea760
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh500728(v=OCS.15)
ms:contentKeyID: 49301288
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un Record DNS SRV per l'integrazione con la messaggistica unificata di Exchange ospitata

 

_**Ultima modifica dell'argomento:** 2013-02-20_

In questo argomento viene descritto come configurare il record DNS (Domain Name System) SRV necessario per un  server perimetrale di Lync Server 2013 per eseguire il routing a un servizio di Exchange ospitato, ad esempio Microsoft Exchange Online.

## Per creare un record DNS SRV esterno per il servizio di Exchange ospitato

1.  Accedere al DNS esterno come membro del gruppo DnsAdmins.

2.  Fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **DNS** .

3.  Nell'albero della console per il dominio SIP espandere **Zone di ricerca diretta** e quindi selezionare il SIP in cui verrà installato Lync Server 2013.
    
    > [!IMPORTANT]  
    > È necessario creare il record DNS SRV nel dominio SIP in cui Lync Server è o verrà installato. Quando si crea il record SRV, l'FQDN utilizzato per il campo Host che offre questo servizio deve essere l'FQDN esterno del pool di server perimetrali. Ad esempio, se l'FQDN esterno del pool di server perimetrali è edge01.contoso.net, immettere tale valore. Deve inoltre trovarsi nello stesso dominio del record DNS degli host (A).

4.  Fare clic con il pulsante destro del mouse sul dominio selezionato e quindi scegliere **Altri nuovi record** .

5.  In **Tipo record di risorse** fare clic su **Posizione servizio (SRV)** , quindi su **Crea record** .

6.  In **Nuovo record di risorse** fare clic su **Servizio** e quindi digitare **\_sipfederationtls** .

7.  Fare clic su **Protocollo** , quindi digitare **\_tcp** .

8.  Fare clic su **Numero porta** , quindi digitare **5061** .

9.  Fare clic su **Host che offre questo servizio** e quindi digitare il nome di dominio completo (FQDN) del pool di server perimetrali di Lync Server 2013 che fornisce accesso al sistema Lync Server 2013 per i client esterni attendibili.
    

    > [!NOTE]
    > È inoltre necessario configurare il dominio come autorevole e accettato nelle impostazioni di Exchange Online. Per informazioni dettagliate, vedere Creare domini accettati all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=229762">http://go.microsoft.com/fwlink/p/?linkId=229762</A>.



10. Scegliere **OK** , quindi su **Fine** .

## Per verificare che il record DNS SRV sia stato creato correttamente

1.  Eseguire l'accesso a un computer client nel dominio.

2.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui** .

3.  Eseguire il comando seguente al prompt:
    
        nslookup <FQDN Lync Edge Pool>

4.  Verificare di ricevere una risposta che si risolve nell'indirizzo IP appropriato per l'FQDN.

## Vedere anche

#### Concetti

[Creare record DNS per server proxy inversi in Lync Server 2013](lync-server-2013-create-dns-records-for-reverse-proxy-servers.md)

