---
title: Modificare l'URL dei servizi Web in Lync Server 2013
TOCTitle: Modificare l'URL dei servizi Web in Lync Server 2013
ms:assetid: 4cee37c0-3b99-4207-997f-bf4229d760c0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520992(v=OCS.15)
ms:contentKeyID: 49300471
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare l'URL dei servizi Web in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-07_

Quando si impostano i pool Front End e i Server Standard, si ha la possibilità di configurare il nome di dominio completo (FQDN) di una Web farm esterna e le porte associate. Se tale URL non è stato configurato durante l'esecuzione della Distribuzione guidata di Lync Server, sarà necessario configurare manualmente queste impostazioni. Un amministratore in genere non ha necessità di modificare tali impostazioni, dal momento che si tratta delle porte consigliate e predefinite.


> [!NOTE]
> La cattura di schermata seguente è stata ottenuta durante la configurazione di un server Standard Edition, pertanto l'opzione Sostituisci FQDN è disabilitata. Tale opzione è abilitata quando si configura un server Enterprise Edition in un pool Front End.



![Modificare le impostazioni dei pool per i servizi Web](images/Gg520992.fbdf5cc9-479a-463f-bb1d-53575ecdfc9d(OCS.15).jpg "Modificare le impostazioni dei pool per i servizi Web")

## Per configurare Servizi Web

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

3.  In Generatore di topologie selezionare il nome del pool nell'albero della console in **Standard Edition Front End Server**, **Pool Enterprise Edition Front End** e **Pool di server Director**. Fare clic con il pulsante destro del mouse sul nome, scegliere **Modifica proprietà** e quindi fare clic su **Servizi Web**.

4.  Aggiungere o modificare l'FQDN di **Servizi Web esterni** e quindi fare clic su **OK**.
    

    > [!WARNING]
    > Se si hanno più pool Front End o Front End Server, l'FQDN di Servizi Web esterni deve essere univoco. Ad esempio, se si definisce l'FQDN di Servizi Web esterni di un Front End Server come <STRONG>pool01.contoso.com</STRONG>, non si può usare <STRONG>pool01.contoso.com</STRONG> per un altro pool Front End o Front End Server. Se si distribuiscono anche Director, l'FQDN di Servizi Web esterni definito per un Server Director o un pool di server Director deve essere diverso da quello di qualsiasi altro Server Director o pool di server Director, così come da qualsiasi altro pool Front End o Front End Server.



5.  Verificare che le porte di attesa e pubblicate siano configurate correttamente per l'ambiente.

6.  Ripetere questi passaggi per tutti i server Standard Edition, i pool Front End e i pool di server Director nell'ambiente.

7.  Nell'albero della console fare clic su **Lync Server 2013** e quindi fare clic su **Pubblica topologia** nel riquadro **Azioni**.

Per la configurazione delle porte di attesa e pubblicate è necessario tenere conto di alcuni requisiti:

  - Le porte di attesa visualizzate sono quelle configurate per Internet Information Server (IIS) in ogni Front End Server.

  - Le porte di attesa interne ed esterne devono essere diverse per IIS. Per le porte di attesa esterne, queste sono in genere le stesse perché una rappresenta il dispositivo di bilanciamento del carico hardware per il traffico Web interno e una rappresenta il server proxy inverso per il traffico Web esterno.

  - È possibile forzare i Servizi Web interni in un pool Front End, Server Director o pool di server Director e definire un FQDN personalizzato.
    

    > [!WARNING]
    > Se si decide di forzare i Servizi Web interni con un FQDN personalizzato, ogni FQDN deve essere diverso da quello di tutti gli altri pool Front End, Server Director o pool di server Director.



  - Le porte pubblicate devono essere configurate nel proxy inverso o nel dispositivo di bilanciamento del carico hardware come porte di attesa.

  - Per un pool Front End (non mostrato nell'esempio, l'FQDN del pool SIP interno deve essere diverso dall'FQDN dei Servizi Web interni, perché il traffico Web arriva attraverso il dispositivo di bilanciamento del carico hardware e il traffico del pool SIP interno passa attraverso il servizio di bilanciamento del carico DNS. Questo requisito deve essere soddisfatto.

  - In una distribuzione di Lync Server Standard Edition non è necessario o non è consentito l'override di un FQDN di Servizi Web interni, perché questo server non può essere sottoposto a bilanciamento del carico.

  - Se nell'ambiente si utilizza un dispositivo di bilanciamento del carico hardware sia per il traffico SIP interno che per il traffico Web, Generatore di topologie non è in grado di effettuare la distinzione.
    
    I nomi di dominio completo (FQDN) dei Servizi Web devono essere facilmente distinguibili; in tal modo si garantirà che gli URL reindirizzino i client al server appropriato. Se ad esempio si dispone di due FQDN, è possibile assegnare a uno il nome riunione.contoso.com e all'altro conferenza.contoso.com. La presenza di due FQDN con nomi simili, ad esempio riunione1.contoso.com e riunione2.contoso.com, potrebbe causare problemi di reindirizzamento.

I servizi Web esterni operano in combinazione con un proxy inverso nella rete perimetrale, che usa questi servizi Web per consentire ai client l'accesso esterno a Microsoft Lync Server. I nomi FQDN qui configurati vengono inviati ai client all'accesso e vengono usati per attivare una connessione HTTPS al proxy inverso in caso di connessione remota. Il server proxy inverso inoltra l'FQDN del servizio Web esterno a un dispositivo di bilanciamento del carico hardware interno o direttamente al pool. Il proxy inverso deve essere in grado di risolvere l'FQDN dei servizi Web esterni nell'indirizzo IP del server Web interno. L'FQDN dei servizi Web esterni deve essere risolvibile nella rete Internet pubblica.

Se il server interno è un server Standard Edition, l'FQDN interno è l'FQDN di server Standard Edition. Se il server interno è un pool Front End, l'FQDN è un IP virtuale (VIP) dello strumento di bilanciamento del carico hardware che gestisce il bilanciamento del carico dei server della Web farm interna. È necessario un dispositivo di bilanciamento del carico hardware in un pool Front End con più di un server Enterprise Edition. Non è invece necessario per un server Standard Edition o un singolo Enterprise Edition Front End Server.

