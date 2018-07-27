---
title: 'Lync Server 2013: Configurazione della federazione di Lync'
TOCTitle: Configurazione della federazione di Lync
ms:assetid: 374ddc43-26f9-499d-be68-a5158adfa49c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204800(v=OCS.15)
ms:contentKeyID: 49300185
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della federazione di Lync in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Se il server o i server perimetrali sono già stati distribuiti, l'aggiunta delle funzionalità degli scenari federati è un'operazione semplice. Se i server perimetrali non sono stati impostati, è necessario prima eseguire questa operazione. Per informazioni dettagliate, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md) nella documentazione relativa alla pianificazione e [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione.


> [!NOTE]
> Se si intende configurare una combinazione di federazione XMPP, Lync o connettività di messaggistica istantanea, è possibile effettuare la distribuzione contemporaneamente o un componente alla volta. Se si configurano le opzioni attraverso il Generatore di topologie e Lync Server Management Shell, eseguire la Distribuzione guidata nel server perimetrale dopo avere configurato le opzioni per uno, due o tutti e tre i tipi di federazione. In questo modo si ridurrà il numero di passaggi necessari.



## Configurazione della federazione Lync nel Generatore di topologie e nella Distribuzione guidata

1.  In un server Front End aprire il Generatore di topologie. Espandere Pool di server perimetrali e quindi fare clic con il pulsante destro del mouse sul server perimetrale o sul pool di server perimetrali. Scegliere Modifica proprietà.

2.  In Modifica proprietà, nella scheda Generale, selezionare Abilita federazione per pool di server perimetrali (porta 5061). Fare clic su OK.

3.  Fare clic su Azione, selezionare Topologia, quindi Pubblica. Quando viene richiesto, in Pubblicare la topologia fare clic su Avanti. Dopo il completamento della pubblicazione fare clic su Fine.

4.  Nel server perimetrale aprire la Distribuzione guidata di Lync Server. Fare clic su Installa o aggiorna il sistema Lync Server e quindi su Installazione o rimozione componenti di Lync Server. Fare clic su Riesegui.

5.  In Installazione componenti di Lync Server fare clic su Avanti. Nella schermata di riepilogo verranno visualizzate le azioni in esecuzione. Al termine della distribuzione, fare clic su Visualizza log per visualizzare i file di log disponibili. Fare clic su Fine per completare la distribuzione.
    
    > [!IMPORTANT]  
    > È possibile selezionare questa opzione, tuttavia solo un pool di server perimetrali o un server perimetrale dell'organizzazione può essere pubblicato esternamente per la federazione. Tutto l'accesso da parte di utenti federati, inclusi gli utenti di messaggistica istantanea pubblica, passa per lo stesso pool di server perimetrali o server perimetrale singolo. Se, ad esempio, la distribuzione include un pool di server perimetrali o un singolo server perimetrale distribuito a New York e uno distribuito a Londra e si abilita il supporto per la federazione nel pool di server perimetrali o nel server perimetrale di New York, il traffico dei segnali per gli utenti federati passerà per il pool di server perimetrali o il singolo server perimetrale di New York. Ciò vale anche per le comunicazioni con gli utenti di Londra, anche se un utente interno di Londra che chiami un utente federato di Londra utilizzerà il pool o il server perimetrale di Londra per il traffico audio/video.

## Configurazione della federazione con i partner

1.  Per configurare correttamente una federazione con un altro Microsoft Lync Server 2013, Lync Server 2010, Office Communications Server 2007 R2, o Office Communicator 2007, selezionare il tipo di federazione nella tabella seguente e definire i record DNS SRV, l'host DNS (A o AAAA per IPv6) e configurare i criteri applicabili al tipo di federazione:
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Tipo di federazione</th>
    <th>Record DNS</th>
    <th>Definizione criterio</th>
    <th>Note</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Dominio partner individuato</p></td>
    <td><p>Configurare il record SRV di format _sipfederationtls._tcp.&lt;nome dominio esterno&gt;In cui il valore della porta per il record SRV è TCP 5061 e l' <strong>Host che offre questo servizio</strong> è definito come sip. &lt;nome dominio esterno&gt;, ovvero l'FQDN del servizio Access Edge. Vedere <a href="lync-server-2013-configure-dns-for-edge-support.md">Configurare DNS per il supporto dei componenti perimetrali in Lync Server 2013</a> per informazioni dettagliate sulla creazione del record SRV</p></td>
    <td><ul>    
> 
> <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></li>    
> 
> 
> <li><p><a href="lync-server-2013-enable-or-disable-discovery-of-federation-partners.md">Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013</a></p></li>    </ul></td>
    <td><p>Nelle versioni precedenti si fa riferimento a questo tipo di federazione come alla <strong>Federazione avanzata aperta</strong>. Questo tipo di federazione richiede la creazione del record SRV e ha lo scopo di consentire agli altri partner di individuare la federazione.</p></td>
    </tr>
    <tr class="even">
    <td><p>Dominio partner consentito</p></td>
    <td><p>Configurare il record SRV di format _sipfederationtls._tcp.&lt;nome dominio esterno&gt;In cui il valore della porta per il record SRV è TCP 5061 e l' <strong>Host che offre questo servizio</strong> è definito come sip. &lt;nome dominio esterno&gt;, ovvero l'FQDN del servizio Access Edge. Vedere <a href="lync-server-2013-configure-dns-for-edge-support.md">Configurare DNS per il supporto dei componenti perimetrali in Lync Server 2013</a> per informazioni dettagliate sulla creazione del record SRV</p></td>
    <td><ul>    
> 
> 
> <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></li>    </ul></td>
    <td><p>Nelle versioni precedenti si fa riferimento a questo tipo di federazione come alla <strong>Federazione avanzata</strong>. Per questo tipo di federazione la creazione del record SRV è facoltativa e ha lo scopo di consentire agli altri partner di individuare la federazione. Si tratta pertanto di un tipo <strong>Federazione avanzata aperta</strong> o <strong>Dominio partner individuato</strong></p></td>
    </tr>
    <tr class="odd">
    <td><p>Server partner consentito</p></td>
    <td><p>Configurare il nome di dominio SIP e l'FQDN del server perimetrale partner come partner della federazione nei criteri</p></td>
    <td><ul>    
> <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></li>    
> 
> <li><p><a href="lync-server-2013-configure-support-for-allowed-external-domains.md">Configurare il supporto per i domini esterni consentiti in Lync Server 2013</a></p></li>    
> 
> 
> <li><p><a href="lync-server-2013-configure-support-for-blocked-external-domains.md">Configurare il supporto per i domini esterni bloccati in Lync Server 2013</a></p></li>    </ul></td>
    <td><p>Questo tipo di federazione è la definizione di una relazione uno a uno e non consente l'individuazione di altri partner della federazione. Ogni partner della federazione viene configurato esplicitamente. Nelle versioni precedenti questa funzionalità è denominata <strong>Federazione diretta</strong></p></td>
    </tr>
    <tr class="even">
    <td><p>Provider di hosting e Provider di servizi di messaggistica istantanea pubblici</p></td>
    <td><p>Per questo tipo di federazione non sono definiti requisiti DNS specifici</p></td>
    <td><ul>    
> <li><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></li>    
> 
> <li><p><a href="lync-server-2013-create-or-edit-public-sip-federated-providers.md">Creare o modificare provider federati SIP pubblici in Lync Server 2013</a></p></li>    
> 
> 
> <li><p><a href="lync-server-2013-create-or-edit-hosted-sip-federated-providers.md">Creare o modificare provider federati SIP ospitati in Lync Server 2013</a></p></li>    </ul></td>
    <td><p>Questo tipo di federazione definisce servizi e provider di hosting che si desidera configurare per gli utenti. Tra gli usi più comuni è inclusa la configurazione per i provider di servizi di messaggistica istantanea pubblici come Windows Live Messenger, Yahoo! e AOL, nonché provider di hosting come Lync Online e Office 365</p>
    <div class="alert">
    > [!IMPORTANT]  
    > <ul>    
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>    
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>    
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>    </ul>

    </div></td>
    </tr>
    </tbody>
    </table>


2.  Definire e configurare qualsiasi host DNS richiesto (A o AAAA per IPv6) e record DNS SRV

3.  Definire e configurare i criteri usando il Pannello di controllo di Lync Server oppure Lync Server Management Shell e i cmdlet appropriati. Per informazioni dettagliate sui cmdlet Lync Server Management Shell, vedere [Cmdlet per la federazione e l'accesso esterno in Lync Server 2013](https://docs.microsoft.com/en-us/powershell/module/skype/)
    

    > [!NOTE]
    > In Lync Room System (LRS) non viene visualizzato il pulsante Partecipa per le riunioni inviate da organizzatori in partner Lync federati. Per consentire la visualizzazione di un collegamento per partecipare alla riunione in LRS, l'organizzazione mittente deve abilitare TNEF mediante il seguente cmdlet:<BR><BR><CODE>New-RemoteDomain -DomainName Contoso.com -Name Contoso</CODE><BR><CODE>Set-RemoteDomain -Identity Contoso -TNEFEnabled $true</CODE><BR>Si noti che questo cmdlet non è specifico di LRS. In questo caso i collegamenti per la partecipazione non verranno visualizzati neanche in Outlook e Lync in quanto le proprietà MAPI non vengono trasportate; nel caso di Outlook, tuttavia, l'utente può aprire l'invito alla riunione e fare clic sull'URL della riunione. Quando TNEFEnabled è impostato su True, le proprietà MAPI, tra cui OnlineMeetingExternalLink, non vengono rimosse e il pulsante Partecipa verrà visualizzato nel promemoria.



## Vedere anche

#### Ulteriori risorse

[Pianificazione per SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-planning-for-sip-xmpp-federation-and-public-instant-messaging.md)  
[Gestione della federazione e dell'accesso esterno a Lync Server 2013](lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md)

