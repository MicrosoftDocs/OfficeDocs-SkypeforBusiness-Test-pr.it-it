---
title: 'Lync Server 2013: Configurare le schede di rete'
TOCTitle: Configurare le schede di rete
ms:assetid: 6519ed80-020f-47a3-851c-03dea5eac5d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429707(v=OCS.15)
ms:contentKeyID: 49300793
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le schede di rete in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

È necessario assegnare uno o più indirizzi IP alla scheda di rete esterna e almeno un indirizzo IP alla scheda di rete interna.

Nelle procedure seguenti, il server che esegue Forefront Threat Management Gateway (TMG) 2010 dispone di due schede di rete:

  - Una scheda di rete pubblica, o esterna, per i client che tentano di connettersi al sito Web, in genere tramite Internet.

  - Un'interfaccia di rete privata, o interna, per i server interni che eseguono Lync Server e che ospitano servizi Web.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>In modo analogo a quanto avviene per i server perimetrali, il gateway predefinito viene impostato solo sulla scheda di rete esterna. Il gateway predefinito sarà l'indirizzo IP del router o del firewall esposto verso l'esterno che indirizza il traffico verso Internet. Per il traffico destinato dal proxy inverso alla scheda di rete interna, è necessario utilizzare route statiche persistenti (come il comando route in Windows Server) per tutte le subnet che contengono i server a cui fanno riferimento le regole di pubblicazione Web. L'impostazione di una route persistente non trasforma il computer in un router. Se l'inoltro IP non è abilitato, il computer viene utilizzato solamente per dirigere all'interfaccia appropriata il traffico specifico destinato a un'altra rete. Si tratta essenzialmente di impostare due gateway: uno come gateway predefinito che punta alle reti esterne e uno per il traffico destinato all'interfaccia interna e a un router o a un'altra rete.<br />
La creazione di route persistenti per tutte le subnet, tuttavia, potrebbe non essere necessaria se i router della rete sono configurati per riepilogare le route. Creare una route persistente verso la rete in cui è stato definito il router e utilizzare il router come gateway predefinito. Se non si è sicuri della configurazione della rete e sono necessarie istruzioni sulle route persistenti che è necessario creare, rivolgersi ai tecnici di rete aziendali.<br />
Il proxy inverso deve essere in grado di risolvere i record host DNS (A) per il Server Director o il Front End Server interno e i nomi FQDN del pool dell'hop successivo utilizzati nelle regole di pubblicazione Web. Come per i server perimetrali, per motivi di sicurezza è consigliabile non consentire ai server proxy inversi di accedere a un server DNS posizionato nella rete interna. Ciò significa che sono necessari server DNS nel perimetro oppure voci di file HOSTS nel proxy inverso per la risoluzione di ognuno di questi FQDN nell'indirizzo IP interno dei server.</td>
</tr>
</tbody>
</table>


## Per configurare le schede di rete nel computer proxy inverso

1.  Nel server Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2 che opera come proxy inverso, aprire **Modifica impostazioni scheda** . A tale scopo, fare clic sul pulsante **Start** , scegliere **Pannello di controllo** , **Centro connessioni di rete e condivisione** e quindi fare clic su **Modifica impostazioni scheda** .

2.  Fare clic con il pulsante destro del mouse sulla connessione di rete esterna che si desidera utilizzare per l'interfaccia interna e quindi scegliere **Proprietà** .

3.  Nella pagina **Proprietà** fare clic sulla scheda **Rete** , selezionare **Protocollo Internet versione 4 (TCP/IPv4)** nell'elenco **La connessione utilizza gli elementi seguenti** e quindi fare clic su **Proprietà** .

4.  Nella pagina **Proprietà TCP/IP** configurare gli indirizzi IP in base alla subnet di rete a cui è collegata la scheda di rete.
    

    > [!NOTE]
    > Se il proxy inverso è già stato utilizzato da altre applicazioni che utilizzano HTTPS/443, come per la pubblicazione di Outlook Web Access, è necessario aggiungere un altro indirizzo IP in modo da poter pubblicare i servizi Web di Lync Server 2013 su HTTPS/443 senza interferire con le regole esistenti e i listener Web. In alternativa, è necessario sostituire il certificato esistente con uno che aggiunge i nuovi nomi FQDN esterni al nome alternativo soggetto.



5.  Fare clic su **OK** e quindi nuovamente su **OK** .

6.  In **Connessioni di rete** fare clic con il pulsante destro del mouse sulla connessione di rete interna che si desidera utilizzare per l'interfaccia interna e quindi scegliere **Proprietà** .

7.  Ripetere i passaggi da 3 a 5 per configurare la connessione di rete interna.

