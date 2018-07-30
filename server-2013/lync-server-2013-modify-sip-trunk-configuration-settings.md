---
title: Modificare le impostazioni di configurazione dei trunk SIP
TOCTitle: Modificare le impostazioni di configurazione dei trunk SIP
ms:assetid: 7d68b09c-9ea0-43bd-997c-df887869d607
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688104(v=OCS.15)
ms:contentKeyID: 49887621
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare le impostazioni di configurazione dei trunk SIP

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Le impostazioni di configurazione trunk SIP definiscono le relazioni e le possibilità tra un Mediation Server e il gateway per la rete telefonica pubblica commutata (PSTN), IP-PBX, o Session Border Controller (SBC) al provider di servizi. Queste impostazioni specificano:

  - Se è necessario abilitare bypass multimediale sui trunk.

  - Le condizioni secondo le quali sono inviati i pacchetti RTCP (Real-Time Transport Control).

  - Se la crittografia SRTP è necessaria o meno su ciascun trunk.

Quando si installa Microsoft Lync Server 2013, viene creata automaticamente una raccolta globale di impostazioni di configurazione per il trunk SIP. Inoltre, gli amministratori possono creare raccolte di impostazioni personalizzate nell'ambito del sito o nell'ambito del servizio (solo per il gateway di servizi PSTN). Queste raccolte possono essere successivamente modificate attraverso Pannello di controllo di Lync Server o Windows PowerShell.

Quando si modificano le impostazioni di configurazione del trunk SIP attraverso Pannello di controllo di Lync Server, sono disponibili le seguenti opzioni:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione UI</th>
<th>Parametro PowerShell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome</p></td>
<td><p>Identità</p></td>
<td><p>Identificatore univoco della raccolta. È una proprietà di sola lettura; non è possibile modificare l'identitià di una raccolta di impostazioni di configurazione per il trunk.</p></td>
</tr>
<tr class="even">
<td><p>Descrizione</p></td>
<td><p>Descrizione</p></td>
<td><p>Consente agli amministratori di archiviare informazioni aggiuntive sulle impostazioni (ad esempio, le finalità della configurazione del trunk).</p></td>
</tr>
<tr class="odd">
<td><p>Dialoghi anticipati massimi supportati</p></td>
<td><p>MaxEarlyDialogs</p></td>
<td><p>Il numero massimo di risposte instradate che un gateway PSTN, IP-PBX o SBC nel provider di servizi può ricevere per un invito inviato a Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p>Livello di supporto della crittografia</p></td>
<td><p>SRTPMode</p></td>
<td><p>Indica il livello di supporto per la protezione del traffico multimediale tra Mediation Server e il gateway PSTN, il sistema IP-PBX o il servizio SBC nel provider dei servizi. Nel caso del bypass multimediale, questo valore deve essere compatibile con l'impostazione di EncryptionLevel nella configurazione degli elementi multimediali. La configurazione degli elementi multimediali viene definita utilizzando i cmdlet <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMediaConfiguration">New-CsMediaConfiguration</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMediaConfiguration">Set-CsMediaConfiguration</a>.</p>
<p>I valori consentiti sono:</p><ul><li><p>Obbligatorio: è necessario utilizzare la crittografia SRTP.</p></li><li><p>Facoltativo: SRTP verrà utilizzato se supportato dal gateway.</p></li><li><p>Non supportato: la crittografia SRTP non è supportata, pertanto non verrà utilizzata.</p></li></ul>
<p>SRTPMode viene utilizzato solo se il gateway è configurato per l'uso di TLS (Transport Layer Security). Se il gateway è configurato con il protocollo TCP (Transmission Control Protocol) per il trasporto, SRTPMode viene impostato internamente su NotSupported.</p></td>
</tr>
<tr class="odd">
<td><p>Supporto riferimento</p></td>
<td><p>Enable3pccRefer</p>
<p>EnableReferSupport</p></td>
<td><p>Se impostato su <strong>Abilita l'invio del riferimento al gateway</strong>, indica che il trunk supporta ricezione di richieste Refer da Mediation Server.</p>
<p>Se impostato su <strong>Abilita il riferimento usando il controllo delle chiamate di terze parti</strong>, indica che il protocollo 3pcc può essere utilizzato per consentire alle chiamate trasferite di eseguire il bypass del sito ospitato. Il protocollo 3pcc è noto anche come &quot;controllo delle terze parti,&quot; e si verifica quando si utilizza una terza parte per la connessione a una coppia di chiamanti (ad esempio, un operatore che connette una chiamata dall'utente A all'utente B).</p></td>
</tr>
<tr class="even">
<td><p>Abilita bypass multimediale</p></td>
<td><p>EnableBypass</p></td>
<td><p>Indica se il bypass multimediale è abilitato per questo trunk. È possibile abilitare il bypass multimediale solo se è abilitato anche <strong>Elaborazione multimediale centralizzata</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Elaborazione multimediale centralizzata</p></td>
<td><p>ConcentratedTopology</p></td>
<td><p>Indica se esiste un punto di terminazione multimediale noto. Un esempio di punto di terminazione multimediale noto può essere costituito da un gateway PSTN in cui la terminazione dei supporti ha lo stesso IP della terminazione dei segnali.</p></td>
</tr>
<tr class="even">
<td><p>Abilita scatto RTP</p></td>
<td><p>EnableRTPLatching</p></td>
<td><p>Indica se i trunk SIP supportano lo scatto RTP, una tecnologia che abilita la connettività RTP/RTCP attraverso un dispositivo NAT o firewall.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita inoltro cronologia chiamate</p></td>
<td><p>ForwardCallHistory</p></td>
<td><p>Indica se le informazioni relative alla cronologia delle chiamate saranno inoltrate attraverso il trunk.</p></td>
</tr>
<tr class="even">
<td><p>Abilita inoltro dati PAI</p></td>
<td><p>ForwardPAI</p></td>
<td><p>Indica se l'intestazione PAI sarà inoltrata con la chiamata. L'intestazione PAI consente di identificare l'identità del chiamante.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita timer di failover del routing in uscita</p></td>
<td><p>EnableFastFailoverTimer</p></td>
<td><p>Indica se le chiamate non risposte dal entro 10 secondi saranno instradate al primo trunk disponibile; se non esistono altri trunk, la chiamata sarà ignorata. In un'organizzazione con reti e risposte del gateway lente, ciò potrebbe portare a ignorare chiamate non volutamente.</p></td>
</tr>
<tr class="even">
<td><p>Utilizzo PSTN associato</p></td>
<td><p>PSTNUsages</p></td>
<td><p>Raccolta di utilizzi PSTN assegnati al trunk.</p></td>
</tr>
<tr class="odd">
<td><p>Numero convertito da testare</p></td>
<td><p>N/D</p></td>
<td><p>Numero di telefono che può essere utilizzato per un test ad hoc delle impostazioni di configurazione del trunk.</p></td>
</tr>
<tr class="even">
<td><p>Regole di conversione associate</p></td>
<td><p>OutboundTranslationRulesList</p></td>
<td><p>Raccolta di regole di conversione dei numeri di telefono che si applicano alle chiamate gestite mediante il routing in uscita (chiamate instradate a destinazioni PBX o PSTN).</p></td>
</tr>
<tr class="odd">
<td><p>Regole di conversione del numero chiamato</p></td>
<td><p>OutboundCallingNumberTranslationRulesList</p></td>
<td><p>Raccolta di regole di conversione del numero chiamato in uscita, assegnate al trunk.</p></td>
</tr>
<tr class="even">
<td><p>Numero di telefono da testare.</p></td>
<td><p>N/D</p></td>
<td><p>Numero di telefono che può essere utilizzato per un test ad hoc delle regole di conversione.</p></td>
</tr>
<tr class="odd">
<td><p>Numero di chiamata</p></td>
<td><p>N/D</p></td>
<td><p>Indica che il numero di telefono da testare è il numero di telefono del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>Numero chiamato</p></td>
<td><p>N/D</p></td>
<td><p>Indica che il numero di telefono da testare è il numero di telefono della persona che riceve la chiamata.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> I cmdlet di Lync Server CsTrunkConfiguration supportano proprietà aggiuntive non visualizzate in Pannello di controllo di Lync Server. Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsTrunkConfiguration">Set-CsTrunkConfiguration</A>.



## Modifica delle impostazioni di configurazione del trunk SIP attraverso Pannello di controllo di Lync Server

1.  In Pannello di controllo di Lync Server, fare clic su **Routing vocale** e quindi su **Configurazione trunk**.

2.  Nella scheda **Configurazione trunk** fare doppio clic sulle impostazioni di configurazione del trunk che si desidera modificare. È possibile modificare una sola raccolta di impostazioni per volta. Per apportare le stesse modifiche a più raccolte, utilizzare Windows PowerShell.

3.  Nella finestra di dialogo **Modifica configurazione trunk**, apportare le modifiche desiderate, quindi scegliere **OK**.

4.  La proprietà **Stato** della raccolta sarà aggiornata a **Commit non eseguito**. Per applicare le modifiche e eliminare la raccolta, fare clic su **Salva** e quindi su **Salva tutto**.

5.  Nella finestra di dialogo **Impostazioni di configurazione vocale di cui non è stato eseguito il commit**, fare clic su **OK**.

6.  Nella finestra di dialogo **Pannello di controllo di Microsoft Lync Server 2013** scegliere **OK**.

