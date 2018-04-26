---
title: 'Lync Server 2013: Gestione di utenti di Exchange ospitati'
TOCTitle: Gestione di utenti di Exchange ospitati
ms:assetid: e8723af5-0604-4d7d-bad2-463a9832efb4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399037(v=OCS.15)
ms:contentKeyID: 49302338
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione di utenti di Exchange ospitati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per fornire servizi di segreteria telefonica per gli utenti di Lync Server 2013 le cui cassette postali sono posizionate in un servizio di Exchange ospitato, è necessario abilitare i relativi account utente per la segreteria telefonica ospitata.


> [!NOTE]
> Per poter abilitare un utente di Lync Server 2013 per la segreteria telefonica ospitata, è necessario distribuire criteri di segreteria telefonica ospitata applicabili all'account utente corrispondente. I criteri possono avere ambito globale, a livello di sito o per utente, purché siano applicabili all'utente da abilitare. Per informazioni dettagliate, vedere <A href="lync-server-2013-hosted-voice-mail-policies.md">Criteri di segreteria telefonica ospitata in Lync Server 2013</A>.



## Attributo msExchUCVoiceMailSettings

In Lync Server 2013 è stato introdotto un nuovo attributo utente, denominato **msExchUCVoiceMailSettings**, che viene creato come parte della preparazione dello schema di Active Directory per Lync Server 2013. Questo attributo multivalore contiene le impostazioni della segreteria telefonica condivise da Lync Server 2013 e dal servizio Exchange ospitato.

Il servizio Exchange ospitato può in alcuni casi impostare il valore dell'attributo msExchUCVoiceMailSettings nel processo di abilitazione della messaggistica unificata di Exchange oppure durante il trasferimento di cassette postali in un computer Exchange Server ospitato. Se questo attributo non viene impostato da Exchange, l'amministratore di Lync Server 2013 deve impostarlo eseguendo il cmdlet Set-CsUser, come descritto in precedenza.

Le coppie chiave/valore dell'attributo e i relativi autori sono illustrati nella tabella seguente.

### Coppie chiave/valore dell'attributo msExchUCVoiceMailSettings

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore</th>
<th>Autore</th>
<th>Significato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeHostedVoiceMail=1</p></td>
<td><p>Exchange</p></td>
<td><p>L'utente è stato abilitato per l'accesso alla messaggistica unificata ospitata da Exchange Server. L'applicazione di routing di Messaggistica unificata di Exchange verificherà i criteri di segreteria telefonica ospitata dell'utente per i dettagli di routing.</p></td>
</tr>
<tr class="even">
<td><p>ExchangeHostedVoiceMail=0</p></td>
<td><p>Exchange</p></td>
<td><p>L'utente è stato disabilitato per l'accesso alla messaggistica unificata ospitata da Exchange Server.</p></td>
</tr>
<tr class="odd">
<td><p>CsHostedVoiceMail=1</p></td>
<td><p>Lync Server</p></td>
<td><p>L'utente è stato abilitato per l'accesso alla messaggistica unificata ospitata da Lync Server 2013. L'applicazione di routing ExUM di Lync Server 2013 verificherà i criteri di segreteria telefonica ospitata dell'utente per i dettagli di routing.</p></td>
</tr>
<tr class="even">
<td><p>CsHostedVoiceMail=0</p></td>
<td><p>Lync Server</p></td>
<td><p>L'utente è stato disabilitato per l'accesso alla messaggistica unificata ospitata da Lync Server 2013.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se l'attributo include già valori diversi da una delle coppie chiave/valore di Lync Server 2013 (CSHostedVoiceMail=0 o CSHostedVoiceMail=1), verrà visualizzato un messaggio di avviso indicante che l'attributo potrebbe essere gestito da un'applicazione diversa. Questo messaggio di avviso verrà ad esempio visualizzato se la coppia chiave/valore ExchangeHostedVoiceMail=0 o ExchangeHostedVoiceMail=1 è già presente. In questo caso, è possibile modificare il valore in Active Directory o eseguire il cmdlet seguente per impostarlo su null:<BR>Set-CsUser –identity user –HostedVoicemail $null



## Abilitazione degli utenti per la segreteria telefonica ospitata

Per consentire l'instradamento delle chiamate alla segreteria telefonica di un utente nella messaggistica unificata di Exchange ospitata, è necessario eseguire il cmdlet Set-CsUser per impostare il valore del parametro *HostedVoiceMail* . Questo parametro indica inoltre a Lync Server 2013 di accendere l'indicatore "Chiama segreteria telefonica".

  - Nell'esempio seguente l'account utente di Luisa Cazzaniga viene abilitato per la segreteria telefonica ospitata:
    
        Set-CsUser -Identity "Pilar Ackerman" -HostedVoiceMail $True
    
    Il cmdlet verifica che i criteri di segreteria telefonica ospitata (globali, a livello di sito o per utente) siano applicabili all'utente. Se nessun criterio è applicabile il cmdlet non riesce.

  - Nell'esempio seguente l'account utente di Luisa Cazzaniga viene disabilitato per la segreteria telefonica ospitata:
    
        Set-CsUser -Identity "Pilar Ackerman" -HostedVoiceMail $False
    
    Il cmdlet verifica che nessun criterio di segreteria telefonica ospitata (globali, a livello di sito o per utente) sia applicabile all'utente. Se un criterio è applicabile il cmdlet non riesce.

Per informazioni dettagliate sull'utilizzo del cmdlet Set-CsUser, vedere la documentazione di Lync Server Management Shell.

