---
title: >
  Lync Server 2013: Configurare criteri per controllare l'accesso degli utenti pubblici
TOCTitle: Configurare criteri per controllare l'accesso degli utenti pubblici
ms:assetid: 090aea0f-ef0b-49da-9c80-02d9279f2fa6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520946(v=OCS.15)
ms:contentKeyID: 49299608
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-07_

La connettività per messaggistica istantanea pubblica consente agli utenti nell'organizzazione di utilizzare la messaggistica istantanea per comunicare con utenti di servizi di messaggistica istantanea forniti da provider di servizi di messaggistica istantanea pubblica, inclusi la rete Windows Live di servizi Internet, Yahoo\! e AOL. È possibile configurare uno o più criteri di accesso per gli utenti esterni per controllare se gli utenti pubblici possono o meno collaborare con utenti interni di Lync Server. La connettività per messaggistica istantanea pubblica è una funzionalità aggiuntiva che si basa sulla configurazione della distribuzione e degli utenti. Dipende inoltre dal provisioning del servizio da parte del provider di servizi di messaggistica istantanea pubblica. Per informazioni su come eseguire il provisioning dell'ambiente per l'utilizzo dei provider pubblici, vedere la guida al provisioning della connettività di messaggistica istantanea pubblica per Microsoft Lync Server, Office Communications Server e Live Communications Server all'indirizzo <http://go.microsoft.com/fwlink/?linkid=269821>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
<li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
<li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Per accedere al sito di provisioning di connettività per messaggistica istantanea pubblica di Microsoft Lync Server, utilizzare il collegamento seguente: <http://go.microsoft.com/fwlink/?linkid=212638>

Per controllare l'accesso degli utenti pubblici, è possibile configurare criteri a livello globale, di sito e di utente. Per informazioni dettagliate sui tipi di criteri che è possibile configurare, vedere [Configurazione del supporto per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-configuring-support-for-external-user-access.md) nella documentazione relativa alla distribuzione o alla pianificazione. Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto.

In caso di inviti alle sessioni di messaggistica istantanea, la risposta dipende dal software client. La richiesta viene accettata a meno che i mittenti esterni non siano esplicitamente bloccati da una regola configurata dall'utente, ovvero le impostazioni negli elenchi **Consenti** e **Blocca** del client dell'utente. Gli inviti alle sessioni di messaggistica istantanea possono inoltre essere bloccati se un utente sceglie di bloccare tutti i messaggi istantanei provenienti da utenti non inclusi nel proprio elenco **Consenti** .


> [!NOTE]
> È possibile configurare criteri per il controllo dell'accesso degli utenti pubblici anche se non è stata abilitata la federazione per l'organizzazione. I criteri configurati, tuttavia, verranno applicati solo dopo l'abilitazione della federazione per l'organizzazione. Per informazioni dettagliate sull'abilitazione della federazione, vedere <A href="lync-server-2013-enable-or-disable-remote-user-access.md">Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013</A> nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni. Se inoltre si specificano criteri utente per il controllo dell'accesso degli utenti pubblici, i criteri verranno applicati solo agli utenti abilitati per Lync Server e configurati per l'utilizzo dei criteri. Per informazioni dettagliate su come specificare gli utenti pubblici autorizzati ad accedere a Lync Server, vedere <A href="lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md">Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013</A> nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.



Eseguire la procedura seguente per configurare i criteri per il supporto dell'accesso da parte di utenti di uno o più provider di servizi di messaggistica istantanea pubblica.

## Per configurare criteri di accesso esterno per il supporto dell'accesso degli utenti pubblici

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e quindi su **Criteri di accesso esterno** .

4.  Nella pagina **Criteri di accesso esterno** eseguire una delle operazioni seguenti:
    
      - Per configurare i criteri globali per il supporto dell'accesso degli utenti pubblici, fare clic sui criteri globali, su **Modifica** e quindi su **Mostra dettagli** .
    
      - Per creare nuovi criteri di sito, fare clic su **Nuovo** e quindi su **Criteri sito** . In **Seleziona un sito** fare clic sul sito appropriato nell'elenco e quindi fare clic su **OK** .
    
      - Per creare nuovi criteri utente, fare clic su **Nuovo** e quindi su **Criteri utente** . In **Nuovi criteri di accesso esterno** creare un nome univoco nel campo **Nome** che indichi lo scopo dei criteri, ad esempio **AbilitaUtentiPubblici** per criteri utente che abilitano le comunicazioni per gli utenti pubblici.
    
      - Per modificare criteri esistenti, fare clic sui criteri appropriati indicati nella tabella, fare clic su **Modifica** e quindi fare clic su **Mostra dettagli** .

5.  (Facoltativo) Se si desidera aggiungere o modificare una descrizione, specificare le informazioni per i criteri in **Descrizione** .

6.  Eseguire una delle operazioni seguenti:
    
      - Per abilitare l'accesso degli utenti pubblici per i criteri, selezionare la casella di controllo **Abilita comunicazioni con utenti pubblici** .
    
      - Per disabilitare l'accesso degli utenti pubblici per i criteri, deselezionare la casella di controllo **Abilita comunicazioni con utenti pubblici** .

7.  Fare clic su **Commit** .

Per abilitare l'accesso degli utenti pubblici, è necessario abilitare anche il supporto della federazione nell'organizzazione. Per informazioni dettagliate, vedere [Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md).

Se si tratta di criteri utente è inoltre necessario applicarli agli utenti pubblici ai quali si desidera permettere di collaborare con utenti pubblici. Per informazioni dettagliate, vedere [Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md).

## Vedere anche

#### Attività

[Creare o modificare provider federati SIP pubblici in Lync Server 2013](lync-server-2013-create-or-edit-public-sip-federated-providers.md)  

#### Ulteriori risorse

[Gestire i provider federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)

