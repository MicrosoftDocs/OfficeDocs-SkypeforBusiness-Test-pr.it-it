---
title: Modifiche dello schema in Lync Server 2013
TOCTitle: Modifiche dello schema in Lync Server 2013
ms:assetid: d760cb93-77d4-4d64-adb7-416b808f36f8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398944(v=OCS.15)
ms:contentKeyID: 49302137
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche dello schema in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Prima di distribuire e utilizzare Lync Server 2013, è necessario preparare Servizi di dominio Active Directory estendendo lo schema. Le estensioni dello schema aggiungono le classi e gli attributi richiesti da Lync Server 2013.

Lync Server 2013 richiede diversi nuovi attributi e nuove classi e modifica alcuni attributi e classi esistenti. Inoltre, la maggior parte delle informazioni di configurazione di Lync Server 2013 è archiviata nell'archivio di gestione centrale anziché in Servizi di dominio Active Directory come nelle versioni precedenti. Le informazioni seguenti vengono ancora archiviate in Servizi di dominio Active Directory in Lync Server 2013:

  - **Estensioni dello schema**:
    
      - Estensioni degli oggetti utente
    
      - Estensioni per le classi di Office Communications Server 2007 e Office Communications Server 2007 R2 per mantenere la compatibilità con le versioni precedenti supportate

<!-- end list -->

  - **Dati** (memorizzati nello schema esteso di Lync Server e nelle classi di schema esistenti):
    
      - URI (Uniform Resource Identifier) SIP dell'utente e altre impostazioni utente
    
      - Oggetti contatto per applicazioni quali Response Group e Operatore Conferenza
    
      - Puntatore all'archivio di gestione centrale
    
      - Account di autenticazione Kerberos (un oggetto computer facoltativo)

In questo argomento vengono descritte le modifiche dello schema di Active Directory richieste da Lync Server 2013. Non sono incluse le modifiche dello schema introdotte dalle precedenti versioni di Office Communications Server. Per un elenco delle classi e delle relative descrizioni, vedere [Classi e descrizioni di schemi in Lync Server 2013](lync-server-2013-schema-classes-and-descriptions.md). Per un elenco degli attributi e delle relative descrizioni, vedere [Attributi e descrizioni di schema in Lync Server 2013](lync-server-2013-schema-attributes-and-descriptions.md). Per un elenco delle classi con gli attributi che possono contenere, vedere [Attributi dello schema in base alla classe in Lync Server 2013](lync-server-2013-schema-attributes-by-class.md).

Il prefisso msRTCSIP identifica le classi e gli attributi specifici di Lync Server.

## Nuovi attributi di Active Directory

Nella tabella seguente sono descritti gli attributi di Active Directory aggiunti da Lync Server 2013.

### Attributi aggiunti da Lync Server 2013

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>msExchUserHoldPolicies</p></td>
<td><p>Questo attributo multivalore include identificatori per i criteri di esenzione che si applicano all'utente. I criteri di esenzione mantengono gli elementi della casetta postale dell'utente per la durata dell'esenzione. Questo attributo è condiviso con Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserRoutingGroupId</p></td>
<td><p>Questo è l'ID del gruppo di routing SIP. Gli utenti dello stesso gruppo si registrano nello stesso Front End Server.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MirrorBackEndServer</p></td>
<td><p>Questo attributo viene utilizzato per archiviare il back-end SQL Server con mirroring utilizzato dal pool Front End.</p></td>
</tr>
</tbody>
</table>


## Classi di Active Directory modificate

Nella tabella seguente vengono descritte le classi di Active Directory modificate da Lync Server 2013.

### Classi modificate da Lync Server 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Modifica</th>
<th>Classe o attributo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>User</p></td>
<td><p>add: mayContain</p>
<p>add: mayContain</p></td>
<td><p>ProxyAddresses</p>
<p>msRTCSIP-UserRoutingGroupId</p></td>
</tr>
<tr class="even">
<td><p>Contact</p></td>
<td><p>add: mayContain</p>
<p>add: mayContain</p></td>
<td><p>ProxyAddresses</p>
<p>msRTCSIP-UserRoutingGroupId</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchUserHoldPolicies</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-GlobalTopologySetting</p></td>
<td><p>add: mayContain</p></td>
<td><p>msRTCSIP-MirrorBackEndServer</p></td>
</tr>
</tbody>
</table>

