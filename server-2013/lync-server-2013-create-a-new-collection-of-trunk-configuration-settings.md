---
title: Creare una nuova raccolta di impostazioni di configurazione trunk
TOCTitle: Creare una nuova raccolta di impostazioni di configurazione trunk
ms:assetid: 4ebd710c-38cd-4cff-9a45-df029d424580
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688054(v=OCS.15)
ms:contentKeyID: 49887558
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare una nuova raccolta di impostazioni di configurazione trunk

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Le impostazioni di configurazione dei trunk SIP definiscono la relazione e le funzionalità tra un Mediation Server e il gateway PSTN (Public Switched Telephone Network), un PBX IP o un SBC (Session Border Controller) presso il provider di servizi. Queste impostazioni hanno la funzione di specificare, tra l'altro:

  - L'abilitazione o meno del bypass multimediale per i trunk.

  - Le condizioni in base alle quali vengono inviati pacchetti RTCP (Real-time Transport Control Protocol).

  - La necessità o meno della crittografia SRTP (Secure Real-Time Protocol) in ogni trunk.

Quando si installa Microsoft Lync Server 2013, viene creata automaticamente una raccolta globale di impostazioni di configurazione dei trunk SIP. Inoltre, gli amministratori possono creare raccolte di impostazioni personalizzate nell'ambito del sito o nell'ambito del servizio (solo per il servizio gateway PSTN).

Per la creazione di impostazioni di configurazione di trunk SIP mediante Pannello di controllo di Lync Server sono disponibili le opzioni seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione interfaccia utente</th>
<th>Parametro PowerShell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome</p></td>
<td><p>Identity</p></td>
<td><p>Identificatore univoco della raccolta. Questa proprietà è di sola lettura. Non è possibile modificare il parametro Identity di una raccolta di impostazioni di configurazione di trunk.</p></td>
</tr>
<tr class="even">
<td><p>Descrizione</p></td>
<td><p>Description</p></td>
<td><p>Consente agli amministratori di memorizzare informazioni aggiuntive sulle impostazioni, ad esempio lo scopo della configurazione di trunk.</p></td>
</tr>
<tr class="odd">
<td><p>Numero massimo di dialoghi anticipati supportati</p></td>
<td><p>MaxEarlyDialogs</p></td>
<td><p>Il numero massimo di risposte instradate che un gateway PSTN, IP-PBX o SBC presso il provider di servizi può ricevere per un invito inviato al Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p>Livello di supporto crittografia</p></td>
<td><p>SRTPMode</p></td>
<td><p>Indica il livello di supporto per la protezione del traffico multimediale tra il Mediation Server e il gateway PSTN, il sistema IP-PBX o il servizio SBC presso il provider dei servizi. Nel caso del bypass multimediale, questo valore deve essere compatibile con l'impostazione di EncryptionLevel nella configurazione degli elementi multimediali. La configurazione degli elementi multimediali viene definita tramite i cmdlet <a href="new-csmediaconfiguration.md">New-CsMediaConfiguration</a> e <a href="set-csmediaconfiguration.md">Set-CsMediaConfiguration</a>.</p>
<p>I valori consentiti sono:</p>
<ul>
<li><p>Obbligatorio: è necessario usare la crittografia SRTP.</p></li>
<li><p>Facoltativo: SRTP verrà usato se supportato dal gateway.</p></li>
<li><p>Non supportato: la crittografia SRTP non è supportata, pertanto non verrà usata.</p></li>
</ul>
<p>Il parametro SRTPMode viene usato solo se il gateway è configurato per l'uso di TLS (Transport Layer Security). Se il gateway è configurato con il protocollo TCP (Transmission Control Protocol) per il trasporto, il parametro SRTPMode viene impostato internamente come non supportato.</p></td>
</tr>
<tr class="odd">
<td><p>Supporto riferimento</p></td>
<td><p>Enable3pccRefer</p>
<p>EnableReferSupport</p></td>
<td><p>Se impostato su <strong>Abilita l'invio del riferimento al gateway</strong>, indica che il trunk supporta la ricezione di richieste Refer dal Mediation Server.</p>
<p>Se impostato su <strong>Abilita il riferimento usando il controllo delle chiamate di terze parti</strong>, indica che è possibile usare il protocollo 3pcc per consentire il trasferimento delle chiamate e ignorare il sito ospitato. Il protocollo 3pcc, detto anche &quot;controllo di terze parti&quot;, interviene quando si usano terze parti per connettere una coppia di chiamanti (ad esempio un operatore per stabilire una chiamata tra l'utente A e l'utente B).</p></td>
</tr>
<tr class="even">
<td><p>Abilita bypass multimediale</p></td>
<td><p>EnableBypass</p></td>
<td><p>Indica se per il trunk è abilitato il bypass multimediale. Il bypass multimediale può essere abilitato solo se è abilitata anche l'<strong>Elaborazione multimediale centralizzata</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Elaborazione multimediale centralizzata</p></td>
<td><p>ConcentratedTopology</p></td>
<td><p>Indica se esiste un punto di terminazione multimediale noto. Un esempio di punto di terminazione multimediale noto può essere costituito da un gateway PSTN in cui la terminazione degli elementi multimediali ha lo stesso IP della terminazione dei segnali.</p></td>
</tr>
<tr class="even">
<td><p>Abilita latch RTP</p></td>
<td><p>EnableRTPLatching</p></td>
<td><p>Indica se i trunk SIP supportano o meno il latch RTP. Questa è una tecnologia che consente la connettività RTP/RTCP attraverso un dispositivo NAT (Network Address Translator) o un firewall.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita cronologia inoltro di chiamata</p></td>
<td><p>ForwardCallHistory</p></td>
<td><p>Indica se le informazioni relative alla cronologia delle chiamate verranno inoltrate attraverso il trunk.</p></td>
</tr>
<tr class="even">
<td><p>Abilita inoltro dati P-Asserted-Identity</p></td>
<td><p>ForwardPAI</p></td>
<td><p>Indica se l'intestazione P-Asserted-Identity (PAI) verrà inoltrata insieme alla chiamata. L'intestazione PAI è uno dei modi per verificare l'identità del chiamante.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita timer di failover del routing in uscita</p></td>
<td><p>EnableFastFailoverTimer</p></td>
<td><p>Indica se le chiamate in uscita a cui il gateway non risponde entro 10 secondi devono essere instradate al trunk disponibile successivo. Se non ci sono altri trunk, le chiamate vengono automaticamente terminate. In un'organizzazione caratterizzata da una certa lentezza delle reti e delle risposte del gateway, questa impostazione potrebbe comportare la conclusione di più chiamate del necessario.</p></td>
</tr>
<tr class="even">
<td><p>Usi PSTN associati</p></td>
<td><p>PSTNUsages</p></td>
<td><p>Raccolta di usi PSTN assegnati al trunk.</p></td>
</tr>
<tr class="odd">
<td><p>Numero convertito da testare</p></td>
<td><p>N/D</p></td>
<td><p>Numero di telefono utilizzabile per test ad hoc delle impostazioni di configurazione del trunk.</p></td>
</tr>
<tr class="even">
<td><p>Regole di conversione associate</p></td>
<td><p>OutboundTranslationRulesList</p></td>
<td><p>Raccolta di regole di conversione dei numeri di telefono che si applicano alle chiamate gestite mediante il routing in uscita (chiamate instradate a destinazioni PBX o PSTN).</p></td>
</tr>
<tr class="odd">
<td><p>Regole di conversione per il numero chiamato</p></td>
<td><p>OutboundCallingNumberTranslationRulesList</p></td>
<td><p>Raccolta di regole di conversione dei numeri delle chiamate in uscita assegnate al trunk.</p></td>
</tr>
<tr class="even">
<td><p>Numero di telefono da testare</p></td>
<td><p>N/D</p></td>
<td><p>Numero di telefono utilizzabile per test ad hoc delle regole di conversione.</p></td>
</tr>
<tr class="odd">
<td><p>Numero del chiamante</p></td>
<td><p>N/D</p></td>
<td><p>Indica che il numero di telefono da testare è il numero di telefono del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>Numero chiamato</p></td>
<td><p>N/D</p></td>
<td><p>Indica che il numero di telefono da testare è il numero di telefono della persona chiamata.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> I cmdlet CsTrunkConfiguration di Lync Server supportano ulteriori proprietà non visualizzate nel Pannello di controllo di Lync Server. Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet <A href="new-cstrunkconfiguration.md">New-CsTrunkConfiguration</A>.



## Creazione di nuove impostazioni di configurazione mediante il Pannello di controllo di Lync Server

1.  Nel Pannello di controllo di Lync Server fare clic su **Routing vocale** e quindi fare clic su **Configurazione trunk**.

2.  Nella scheda **Configurazione trunk** fare clic su **Nuovo** e quindi su **Trunk sito** per creare la nuova impostazione nell'ambito del sito, oppure fare clic su **Trunk pool** per creare le nuove impostazioni dell'ambito del servizio.

3.  Nella finestra di dialogo **Selezionare un sito** o **Selezionare un servizio** (la finestra di dialogo visualizzata dipende dal tipo di impostazioni create: nell'ambito del sito o nell'ambito del servizio) selezionare la posizione delle nuove impostazioni di configurazione e quindi fare clic su **OK**. Se la finestra di dialogo è vuota, non ci sono posizioni in cui creare le nuove impostazioni. Ad esempio, se la finestra di dialogo **Selezionare un sito** è vuota, significa che a tutti i siti è già stata assegnata una raccolta di siti di configurazione di trunk, dato che a ogni sito (e a ogni servizio) può essere assegnata una sola raccolta di questo tipo. In questo caso, è possibile eliminare la raccolta esistente e crearne una nuova o semplicemente modificare la raccolta esistente.

4.  Nella finestra di dialogo **Nuova Configurazione trunk** eseguire le selezioni appropriate e quindi fare clic su **OK**.

5.  La proprietà **Stato** della raccolta verrà aggiornata con **Commit non eseguito**. Per eseguire il commit delle modifiche ed eliminare la raccolta, fare clic su **Commit** e quindi su **Salva tutto**.

6.  Nella finestra di dialogo **Impostazioni di configurazione vocale di cui non è stato eseguito il commit**fare clic su **OK**.

7.  Nella finestra di dialogo **Pannello di controllo di Microsoft Lync Server 2013** fare clic su **OK**.

