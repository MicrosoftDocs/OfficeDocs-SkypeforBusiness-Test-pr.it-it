---
title: 'Lync Server 2013: Panoramica della preparazione di Servizi di dominio Active Directory'
TOCTitle: Panoramica della preparazione di Servizi di dominio Active Directory
ms:assetid: cdd2a652-6a0d-4728-9950-3fcaa7a80066
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398869(v=OCS.15)
ms:contentKeyID: 49302014
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica della preparazione di Servizi di dominio Active Directory in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per preparare Servizi di dominio Active Directory per la distribuzione di Lync Server 2013, è necessario eseguire tre passaggi in una sequenza specifica.

Nella tabella che segue vengono descritti i passaggi necessari per preparare Servizi di dominio Active Directory per Lync Server.

### Passaggi di preparazione di Active Directory

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Passaggio</th>
<th>Descrizione</th>
<th>Esecuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1.</p></td>
<td><p><a href="lync-server-2013-preparing-the-active-directory-schema.md">Preparazione dello schema di Active Directory in Lync Server 2013</a></p></td>
<td><p>Estende lo schema di Active Directory tramite l'aggiunta di nuove classi e nuovi attributi utilizzati da Lync Server.</p>
<p>Eseguire il passaggio una volta per ogni foresta nella distribuzione in cui verrà implementato Lync Server.</p></td>
<td><p>Sul master schema nel dominio radice di ogni foresta in cui verrà distribuito Lync Server.</p>


> [!NOTE]
> Non è necessario eseguire questo passaggio nel dominio radice se si dispone delle autorizzazioni sul master di schemi, ma è necessario essere un membro del gruppo Schema Admins nel dominio radice e un membro del gruppo Enterprise Admins nel master di schemi. In una topologia di foresta di risorse eseguire questo passaggio solo nella foresta di risorse e non nelle foreste di utenti. In una topologia di foresta centrale eseguire questo passaggio solo nella foresta centrale e non nelle foreste di utenti.


</td>
</tr>
<tr class="even">
<td><p>2.</p></td>
<td><p><a href="lync-server-2013-preparing-the-forest.md">Preparazione della foresta per Lync Server 2013</a></p></td>
<td><p>Crea impostazioni globali e gruppi universali utilizzati da Lync Server.</p>
<p>Eseguire il passaggio una volta per ogni foresta nella distribuzione in cui verrà implementato Lync Server.</p></td>
<td><p>Nel dominio radice di ogni foresta in cui verrà distribuito Lync Server. Per eseguire questo passaggio, è necessario essere un membro del gruppo Enterprise Admins.</p>


> [!NOTE]
> In una topologia di foresta di risorse eseguire questo passaggio solo nella foresta di risorse e non nelle foreste di utenti. In una topologia di foresta centrale eseguire questo passaggio solo nella foresta centrale e non nelle foreste di utenti.


</td>
</tr>
<tr class="odd">
<td><p>3.</p></td>
<td><p><a href="lync-server-2013-preparing-domains.md">Preparazione dei domini per Lync Server 2013</a></p></td>
<td><p>Aggiunge autorizzazioni per gli oggetti che verranno utilizzati dai membri dei gruppi universali.</p>
<p>Eseguire il passaggio una volta per ogni dominio utente o server.</p>


> [!NOTE]
> Se si esegue la migrazione da Lync Server 2010 a Lync Server 2013, la Distribuzione guidata potrebbe indicare che la preparazione del dominio è stata già completata e pertanto non è necessario eseguire di nuovo questo passaggio. Le autorizzazioni non sono state modificate nel passaggio da Lync Server 2010 a Lync Server 2013.


</td>
<td><p>Su un server membro in ogni domino in cui verrà distribuito Lync Server. Per eseguire questo passaggio, è necessario essere un membro del gruppo Domain Admins.</p></td>
</tr>
</tbody>
</table>


Analogamente a Lync Server 2010, in Lync Server 2013 la maggior parte delle informazioni sulla configurazione viene memorizzata nell' archivio di gestione centrale anziché in Servizi di dominio Active Directory, come avviene invece in Office Communications Server 2007 R2. Le informazioni seguenti tuttavia vengono ancora memorizzate in Servizi di dominio Active Directory:

  - **Estensioni dello schema**:
    
      - Estensioni degli oggetti utente
    
      - Estensioni delle classi Office Communications Server 2007 R2 per garantire la compatibilità con le versioni precedenti

<!-- end list -->

  - **Dati** (memorizzati nello schema esteso di Lync Server e nelle classi di schema esistenti):
    
      - URI (Uniform Resource Identifier) SIP dell'utente e altre impostazioni utente
    
      - Oggetti contatto per applicazioni quali Response Group e Operatore Conferenza
    
      - Puntatore all' archivio di gestione centrale
    
      - Account di autenticazione Kerberos (un oggetto computer facoltativo)

In Lync Server 2013 le operazioni di installazione e di amministrazione vengono delegate concedendo autorizzazioni di installazione al gruppo universale RTCUniversalServerAdmins in modo che i membri di tale gruppo possano installare e attivare Lync Server 2013 in un server locale (dopo che il server è stato aggiunto alla topologia, pubblicato e abilitato). Gli utenti delegati devono essere amministratori locali per il computer in cui installano e attivano Lync Server 2013, ma non è necessario che siano membri del gruppo Domain Admins. È anche possibile concedere autorizzazioni per gli oggetti di unità organizzative specificate, in modo che i membri dei gruppi universali creati durante la preparazione della foresta possano accedere a tali oggetti senza essere membri del gruppo Domain Admins.

Per nuove distribuzioni di Lync Server 2013, è necessario archiviare le impostazioni globali nel contenitore Configuration. Se nell'organizzazione viene eseguito l'aggiornamento da una versione precedente e sono ancora presenti impostazioni globali nel contenitore System, tale contenitore continuerà a essere supportato.

## Vedere anche

#### Concetti

[Preparazione dello schema di Active Directory in Lync Server 2013](lync-server-2013-preparing-the-active-directory-schema.md)  
[Estensioni dello schema, classi e attributi di Active Directory utilizzati da Lync Server 2013](lync-server-2013-active-directory-schema-extensions-classes-and-attributes-used-by-lync-server.md)  

#### Ulteriori risorse

[Preparazione della foresta per Lync Server 2013](lync-server-2013-preparing-the-forest.md)  
[Preparazione dei domini per Lync Server 2013](lync-server-2013-preparing-domains.md)

