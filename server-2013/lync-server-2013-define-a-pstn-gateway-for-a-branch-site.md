---
title: 'Lync Server 2013: Definire un gateway PSTN per un sito di succursale'
TOCTitle: Definire un gateway PSTN per un sito di succursale
ms:assetid: 87be2fe2-1d56-4062-b430-439d4536414c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398689(v=OCS.15)
ms:contentKeyID: 49301222
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire un gateway PSTN per un sito di succursale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Eseguire questa procedura nel sito centrale, che contiene almeno un pool Front End o Server Standard Edition.

> [!important]  
> Prima di eseguire la procedura, è necessario che vengano soddisfatte le condizioni seguenti:<ul>
> 
> <li><p>Il Lync Server 2013  software di comunicazione deve essere configurato nel sito centrale.</p></li>
> 
> 
> <li><p>Mediation Server deve essere distribuito nel sito centrale.</p></li></ul>


## Per definire un gateway PSTN

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server** e quindi **Generatore di topologie di Lync Server** .

2.  Nell'albero della console espandere il sito centrale, espandere **Siti di succursale** e quindi espandere il nome del sito derivato per il quale si desidera definire un gateway PSTN. Espandere quindi **Componenti condivisi** .

3.  Fare clic con il pulsante destro del mouse su **Gateway PSTN** e quindi scegliere **Nuovo gateway IP/PSTN** .

4.  Nella finestra di dialogo **Definisci nuovo gateway IP/PSTN** fare clic su **FQDN gateway o indirizzo IP** e quindi digitare il nome di dominio completo (FQDN) o l'indirizzo IP del gateway che si sta distribuendo nel sito derivato.

5.  Fare clic su **Porta di attesa per gateway IP/PSTN** e quindi accettare i valori predefiniti.

6.  Nell'elenco **Protocollo trasporto SIP** fare clic sul protocollo di trasporto utilizzato dal gateway e quindi su **OK** .
    

    > [!NOTE]
    > Per motivi di sicurezza, è consigliabile utilizzare un gateway PSTN che supporti TLS (Transport Layer Security).



> [!tip]  
> Utilizzare il cmdlet <strong>Set-CsPstnGateway</strong> per modificare le proprietà di un gateway PSTN. Per informazioni dettagliate, vedere <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPstnGateway">Set-CsPstnGateway</a> nella guida di Lync Server Management Shell.

**Passaggio successivo** per la resilienza dei siti derivati: [Configurazione degli utenti per la resilienza dei siti di succursale in Lync Server 2013](lync-server-2013-configuring-users-for-branch-site-resiliency.md)

## Vedere anche

#### Concetti

[Opzioni di distribuzione di gateway PSTN in Lync Server 2013](lync-server-2013-pstn-gateway-deployment-options.md)

