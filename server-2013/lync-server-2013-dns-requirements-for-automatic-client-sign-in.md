---
title: Requisiti DNS per l'accesso automatico dei client in Lync Server 2013
TOCTitle: Requisiti DNS per l'accesso automatico dei client in Lync Server 2013
ms:assetid: 3bcd4bb3-a022-4ffa-b005-1a95ad2b1796
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425884(v=OCS.15)
ms:contentKeyID: 49300258
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti DNS per l'accesso automatico dei client in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti i record DNS (Domain Name System) necessari per l'accesso client automatico. Quando si distribuiscono i Server Standard o i pool Front End, è possibile configurare i client per l'utilizzo dell'individuazione automatica in modo da accedere al Server Standard o al pool Front End appropriato. Se si intende richiedere che i client si connettano manualmente a Lync Server 2013, è possibile ignorare questo argomento.

Per supportare l'accesso automatico dei client, è necessario:

  - Designare un solo server o un pool per la distribuzione e l'autenticazione delle richieste di accesso dei client. A tale scopo, è possibile designare un server o un pool disponibile nell'organizzazione che ospita gli utenti oppure un server o un pool dedicato che non ospita alcun utente. Per garantire la disponibilità elevata, è consigliabile designare un pool Front End per questa funzione.

  - Creare un record SRV DNS interno per supportare l'accesso automatico dei client per questo server o pool.
    

    > [!NOTE]
    > Nei requisiti dei record riportati di seguito il dominio SIP fa riferimento alla parte host degli URI SIP assegnati agli utenti. Se ad esempio gli URI SIP sono nel formato *@contoso.com, contoso.com è il dominio SIP. Il dominio SIP è spesso diverso dal dominio Active Directory interno. Un'organizzazione può supportare anche più domini SIP.



Per abilitare la configurazione automatica per i client, è necessario creare un record SRV DNS interno per il mapping tra uno dei record seguenti e il nome di dominio completo (FQDN) del pool Front End o del server Standard Edition che distribuisce le richieste di accesso dei client Lync:

  - \_sipinternaltls.\_tcp.*\<dominio\>* - per connessioni TLS interne

È sufficiente creare un unico record SRV per il pool Front End o il server Standard Edition che distribuirà le richieste di accesso.

Nella tabella riportata di seguito vengono illustrati alcuni record di esempio necessari per la società fittizia Contoso, che supporta i domini SIP contoso.com e retail.contoso.com.

### Esempio di record DNS obbligatori per l'accesso automatico dei client con più domini SIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN del pool Front End utilizzato per distribuire le richieste di accesso</th>
<th>Dominio SIP</th>
<th>Record SRV DNS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>pool01.contoso.com</p></td>
<td><p>contoso.com</p></td>
<td><p>Record SRV per il dominio _sipinternaltls._tcp.contoso.com tramite la porta 5061 associata a pool01.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>pool01.contoso.com</p></td>
<td><p>retail.contoso.com</p></td>
<td><p>Record SRV per il dominio _sipinternaltls._tcp.retail.contoso.com tramite la porta 5061 associata a pool01.contoso.com</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Per impostazione predefinita, le query per i record DNS seguono la rigida corrispondenza dei nomi di dominio tra il dominio del nome utente e il record SRV. Se si desidera che le query DNS del client utilizzino invece la corrispondenza dei suffissi, è possibile configurare il criterio di gruppo DisableStrictDNSNaming. Per informazioni dettagliate, vedere <A href="lync-server-2013-planning-for-clients-and-devices.md">Pianificazione dei client e dei dispositivi in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Esempio dei certificati e dei record DNS obbligatori per l'accesso automatico dei client

In questo esempio vengono utilizzati gli stessi nomi di esempio della tabella precedente. L'organizzazione Contoso supporta i domini SIP contoso.com e retail.contoso.com e tutti i relativi utenti dispongono di un URI SIP in uno dei formati seguenti:

  - *\<utente\>*@retail.contoso.com

  - *\<utente\>*@contoso.com

