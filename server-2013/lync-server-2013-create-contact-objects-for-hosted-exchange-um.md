---
title: 'Lync Server 2013: Creare oggetti contatto per la messaggistica unificata di Exchange ospitata'
TOCTitle: Creare oggetti contatto per la messaggistica unificata di Exchange ospitata
ms:assetid: a39be52f-488a-4523-ad5f-ce1f0d681959
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412765(v=OCS.15)
ms:contentKeyID: 49301533
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare oggetti contatto per la messaggistica unificata di Exchange ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-24_

Nella procedura riportata di seguito viene illustrato come creare oggetti contatto Operatore automatico o Accesso sottoscrittore per la messaggistica unificata di Exchange ospitata.

Per informazioni dettagliate, vedere [Gestione di oggetti contatto di Exchange ospitati in Lync Server 2013](lync-server-2013-hosted-exchange-contact-object-management.md) nella documentazione relativa alla pianificazione.

Per i dettagli sulla configurazione di oggetti contatto, vedere la documentazione di Lync Server Management Shell per i cmdlet seguenti:

  - [New-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsExUmContact)

  - [Set-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExUmContact)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima che sia possibile abilitare gli oggetti contatto di Lync Server 2013 per la messaggistica unificata di Exchange ospitata, è necessario distribuire criteri di segreteria telefonica ospitata applicabili a tali oggetti. Per informazioni dettagliate, vedere <a href="lync-server-2013-hosted-voice-mail-policies.md">Criteri di segreteria telefonica ospitata in Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Per creare oggetti contatto Operatore automatico o Accesso sottoscrittore per la messaggistica unificata di Exchange ospitata

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet New-CsExUmContact per creare gli oggetti contatto necessari per la distribuzione. Ad esempio, per creare un oggetto contatto Operatore automatico e un oggetto contatto Accesso sottoscrittore:
    
        New-CsExUmContact -SipAddress "sip:exumaa1@fabrikam.com" -RegistrarPool "RedmondPool.litwareinc.com" -OU "HostedExUM Integration" -DisplayNumber "+14255550101" -AutoAttendant $True
    
        New-CsExUmContact -SipAddress "sip:exumsa1@fabrikam.com" -RegistrarPool "RedmondPool.litwareinc.com" -OU "HostedExUM Integration" -DisplayNumber "+14255550101"
    
    In questi esempi vengono impostati i parametri seguenti:
    
      - **SipAddress** specifica l'indirizzo SIP dell'oggetto contatto. Deve corrispondere a un indirizzo non ancora utilizzato per la configurazione di un utente o di un oggetto contatto in Servizi di dominio Active Directory. Questo valore deve essere espresso nel formato "sip:\< *SIP address*\>", come illustrato negli esempi precedenti.
    
      - **RegistrarPool** specifica il nome di dominio completo (FQDN) del pool su cui è in esecuzione il servizio di registrazione.
        

        > [!NOTE]
        > Non è possibile spostare oggetti contatto della messaggistica unificata di Exchange in pool che fanno parte di distribuzioni di Lync Server 2013 antecedenti a Lync Server 2013.

    
      - **OU** specifica l'unità organizzativa Active Directory in cui sarà situato l'oggetto contatto.
    
      - **DisplayNumber** specifica il numero di telefono dell'oggetto contatto. Il numero di telefono deve essere univoco per ogni oggetto contatto.
    
      - **AutoAttendant** specifica se l'oggetto contatto è un operatore automatico. La funzionalità Operatore automatico mette a disposizione una serie di istruzioni vocali che consentono ai chiamanti di navigare nel sistema telefonico fino a raggiungere l'interlocutore desiderato. Per questo parametro il valore **$False** (predefinito) indica un oggetto contatto Accesso sottoscrittore.

