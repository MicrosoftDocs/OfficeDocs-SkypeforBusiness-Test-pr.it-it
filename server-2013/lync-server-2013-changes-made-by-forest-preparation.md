---
title: Modifiche apportate durante la preparazione della foresta in Lync Server 2013
TOCTitle: Modifiche apportate durante la preparazione della foresta in Lync Server 2013
ms:assetid: 2e12613e-59f2-4810-a32d-24a9789a4a6e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425791(v=OCS.15)
ms:contentKeyID: 49300046
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche apportate durante la preparazione della foresta in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti gli oggetti e le impostazioni globali e i gruppi amministrativi e di servizio universali creati durante il passaggio di preparazione della foresta.

## Oggetti e impostazioni globali di Active Directory

Se si archiviano impostazioni globali nel contenitore Configuration (come per tutte le nuove distribuzioni di Lync Server 2013), per la preparazione della foresta verrà usato il contenitore Services esistente e verrà aggiunto un oggetto **RTC Service** nell'oggetto Configuration\\Services. Nell'oggetto RTC Service viene aggiunto per la preparazione della foresta un oggetto **Global Settings** di tipo msRTCSIP-GlobalContainer. Nell'oggetto Global Settings sono contenute tutte le impostazioni che si applicano alla distribuzione di Lync Server. Se si archiviano le impostazioni globali nel contenitore System, per la preparazione della foresta verrà usato un contenitore Microsoft nel contenitore System del dominio radice e un oggetto RTC Service nell'oggetto System\\Microsoft.

Durante la preparazione della foresta viene aggiunto inoltre un nuovo oggetto **msRTCSIP-Domain** per il dominio radice in cui viene eseguita la procedura.

## Gruppi amministrativi e di servizio universali di Active Directory

Durante la preparazione della foresta vengono creati gruppi universali basati sul dominio specificato e vengono aggiunte voci di controllo di accesso (ACE) per tali gruppi. Durante questo passaggio vengono creati i gruppi universali nei contenitori User del dominio specificato.

I gruppi universali consentono agli amministratori di accedere ai servizi e alle impostazioni globali e di gestirli. Per la preparazione della foresta vengono aggiunti i tipi di gruppi universali seguenti:

  - **Gruppi amministrativi**   Questi gruppi definiscono i ruoli di amministratore per una rete Lync Server.

  - **Gruppi di infrastruttura**   Questi gruppi forniscono l'autorizzazione per accedere ad aree specifiche dell'infrastruttura di Lync Server. Funzionano come componenti di gruppi amministrativi. Non modificare questi gruppi né aggiungervi direttamente gli utenti.

  - **Gruppi di servizio**   Questi gruppi sono account di servizio necessari per accedere ai diversi servizi di Lync Server.

Nella tabella riportata di seguito vengono descritti i gruppi amministrativi.

### Gruppi amministrativi creati durante la preparazione della foresta

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo amministrativo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCUniversalServerAdmins</p></td>
<td><p>Consente ai membri di gestire le impostazioni di server e pool, inclusi tutti gli utenti, le impostazioni globali e i ruoli del server.</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Consente ai membri di gestire le impostazioni utente e di spostare gli utenti da un server o da un pool a un altro.</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalReadOnlyAdmins</p></td>
<td><p>Consente ai membri di leggere le impostazioni di server, pool e utenti.</p></td>
</tr>
</tbody>
</table>


Nella tabella riportata di seguito vengono descritti i gruppi di infrastruttura.

### Gruppi di infrastruttura creati durante la preparazione della foresta

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo di infrastruttura</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCUniversalGlobalWriteGroup</p></td>
<td><p>Concede l'accesso in scrittura agli oggetti impostazioni globali per Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalGlobalReadOnlyGroup</p></td>
<td><p>Concede l'accesso in sola lettura agli oggetti impostazioni globali per Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Concede l'accesso in sola lettura alle impostazioni utente di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>Concede l'accesso in sola lettura alle impostazioni di Lync Server. Questo gruppo non dispone dell'accesso alle impostazioni a livello di pool, ma solo a quelle specifiche di un singolo server.</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalSBATechnicians</p></td>
<td><p>Concede l'accesso in sola lettura alla configurazione di Lync Server ed è incluso nel gruppo Local Administrators dei Survivable Branch Appliance durante l'installazione.</p></td>
</tr>
</tbody>
</table>


Nella tabella riportata di seguito vengono descritti i gruppi di servizio.

### Gruppi di servizio creati durante la preparazione della foresta

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo di servizio</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>Include gli account di servizio usati per eseguire il Front End Server e i server Standard Edition. Questo gruppo concede ai server l'accesso in lettura/scrittura alle impostazioni globali di Lync Server e agli oggetti utente Active Directory.</p></td>
</tr>
<tr class="even">
<td><p>RTCComponentUniversalServices</p></td>
<td><p>Include gli account di servizio utilizzati per eseguire A/V Conferencing Server, servizi Web, Mediation Server, server di archiviazione e Monitoring Server.</p></td>
</tr>
<tr class="odd">
<td><p>RTCProxyUniversalServices</p></td>
<td><p>Include gli account di servizio usati per eseguire i server perimetrali Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalConfigReplicator</p></td>
<td><p>Include i server che possono partecipare alla replica dell'archivio di gestione centrale di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p>RTCSBAUniversalServices</p></td>
<td><p>Concede l'accesso in sola lettura alle impostazioni di Lync Server, ma consente la configurazione dell'installazione di una distribuzione di Survivable Branch Server e Survivable Branch Appliance.</p></td>
</tr>
</tbody>
</table>


Durante la preparazione della foresta vengono quindi aggiunti i gruppi amministrativi e di servizio ai gruppi di infrastruttura appropriati, come indicato di seguito:

  - RTCUniversalServerAdmins viene aggiunto a RTCUniversalGlobalReadOnlyGroup, RTCUniversalGlobalWriteGroup, RTCUniversalServerReadOnlyGroup e RTCUniversalUserReadOnlyGroup.

  - RTCUniversalUserAdmins viene aggiunto come membro di RTCUniversalGlobalReadOnlyGroup, RTCUniversalServerReadOnlyGroup e RTCUniversalUserReadOnlyGroup.

  - RTCHSUniversalServices, RTCComponentUniversalServices e RTCUniversalReadOnlyAdmins vengono aggiunti come membri di RTCUniversalGlobalReadOnlyGroup, RTCUniversalServerReadOnlyGroup e RTCUniversalUserReadOnlyGroup.

Durante la preparazione della foresta vengono creati inoltre i gruppi di controllo dell'accesso basato sui ruoli seguenti:

  - CSAdministrator

  - CSArchivingAdministrator

  - CSHelpDesk

  - CSLocationAdministrator

  - CSResponseGroupAdministrator

  - CSServerAdministrator

  - CSUserAdministrator

  - CSViewOnlyAdministrator

  - CSVoiceAdministrator

  - CsPersistentChatAdministator

  - CsResponseGroupManager

Per informazioni dettagliate sui gruppi di controllo dell'accesso basato sui ruoli e sulle attività consentite per ognuno, vedere [Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013](lync-server-2013-planning-for-role-based-access-control.md) nella documentazione relativa alla pianificazione.

Durante la preparazione della foresta vengono create voci di controllo di accesso private e pubbliche. Le voci di controllo di accesso private vengono create nel contenitore di impostazioni globali usato da Lync Server. Questo contenitore viene usato solo da Lync Server ed è posizionato nel contenitore Configuration o nel contenitore System del dominio radice, a seconda della posizione di archiviazione delle impostazioni globali. Le voci di controllo di accesso pubbliche create durante la preparazione della foresta sono elencate nella tabella seguente.

### Voci di controllo di accesso pubbliche create durante la preparazione della foresta

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Voce di controllo di accesso</th>
<th>RTCUniversalGlobalReadOnlyGroup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lettura del contenitore System del dominio radice (non ereditata)<strong>*</strong></p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Lettura del contenitore DisplaySpecifiers della configurazione (non ereditata)</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <STRONG>*</STRONG>Alle voci di controllo di accesso non ereditate non viene concesso l'accesso agli oggetti figlio presenti in tali contenitori. Alle voci di controllo di accesso ereditate viene concesso l'accesso agli oggetti figlio presenti in tali contenitori.



Nel contesto dei nomi di configurazione all'interno del contenitore Configuration durante la preparazione della foresta vengono eseguite le attività seguenti:

  - Aggiunta di una voce **{AB255F23-2DBD-4bb6-891D-38754AC280EF}** per la pagina della proprietà **RTC** negli attributi adminContextMenu e adminPropertyPages dell'identificatore di visualizzazione lingua per gli oggetti User, Contact e InetOrgPerson, ad esempio, CN=user-Display,CN=409,CN=DisplaySpecifiers.

  - Aggiunta di un oggetto **RTCPropertySet** di tipo **controlAccessRight** in **Extended-Rights** che da applicare alle classi User e Contact.

  - Aggiunta di un oggetto **RTCUserSearchPropertySet** di tipo **controlAccessRight** in **Extended-Rights** da applicare alle classi User, Contact, OU e DomainDNS.

  - Aggiunta di un oggetto **msRTCSIP-PrimaryUserAddress** nell'attributo **extraColumns** di ogni identificatore di visualizzazione unità organizzativa lingua (ad esempio CN=organizationalUnit-Display,CN=409,CN=DisplaySpecifiers) e copia dei valori dell'attributo **extraColumns** della visualizzazione predefinita (ad esempio CN=default-Display, CN=409,CN=DisplaySpecifiers).

  - Aggiunta degli attributi di filtro **msRTCSIP-PrimaryUserAddress**, **msRTCSIP-PrimaryHomeServer** e **msRTCSIP-UserEnabled** nell'attributo **attributeDisplayNames** di ogni identificatore di visualizzazione lingua per gli oggetti User, Contact e InetOrgPerson (ad esempio per la lingua inglese: CN=user-Display,CN=409,CN=DisplaySpecifiers).

