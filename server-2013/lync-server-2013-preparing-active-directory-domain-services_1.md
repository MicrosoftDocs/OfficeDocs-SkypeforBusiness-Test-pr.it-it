---
title: 'Lync Server 2013: Preparazione di Servizi di dominio Active Directory'
TOCTitle: Preparazione di Servizi di dominio Active Directory
ms:assetid: 7b0d9aa4-f1ab-4578-b22f-b802b6ed1530
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398607(v=OCS.15)
ms:contentKeyID: 49301069
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione di Servizi di dominio Active Directory in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel Lync Server 2013 è possibile utilizzare la Distribuzione guidata di Lync Server per preparare Servizi di dominio Active Directory oppure è possibile utilizzare direttamente i cmdlet di Lync Server Management Shell. È inoltre possibile utilizzare lo strumento da riga di comando ldifde.exe nei controller di dominio, come descritto più avanti in questo argomento.

La Distribuzione guidata di Lync Server guida l'utente nelle attività di preparazione di Active Directory. La Distribuzione guidata esegue cmdlet di Lync Server Management Shell. Questo strumento è utile per gli ambienti con una topologia a singolo dominio e a singola foresta o con un'altra topologia simile.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È possibile distribuire Lync Server in una foresta o in un dominio in cui i controller di dominio eseguono versioni a 32 bit di alcuni sistemi operativi (per informazioni dettagliate, vedere <a href="lync-server-2013-active-directory-infrastructure-requirements.md">Requisiti dell'infrastruttura di Active Directory per Lync Server 2013</a>). In questi ambienti non è tuttavia possibile utilizzare la Distribuzione guidata di Lync Server per eseguire la preparazione dello schema, della foresta e del dominio, in quanto la procedura guidata e i file di supporto sono solo a 64 bit. È tuttavia possibile utilizzare ldifde.exe e i file con estensione ldf associati in un controller di dominio a 32 bit per preparare lo schema, la foresta e il dominio. Vedere la sezione &quot;Utilizzo dei cmdlet e di Ldifde.exe&quot; più avanti in questo argomento.</td>
</tr>
</tbody>
</table>


È possibile utilizzare i cmdlet di Lync Server Management Shell per eseguire attività in remoto o per ambienti più complessi.

## Prerequisiti di preparazione di Active Directory

È necessario eseguire la procedura di preparazione di Active Directory in un computer in cui è in esecuzione Windows Server 2012, Windows Server 2012 R2 o Windows Server 2008 R2 con SP1 a 64 bit. Per la preparazione di Active Directory sono necessari Lync Server Management Shell e OCSCore.

Per eseguire le attività di preparazione di Active Directory sono necessari i componenti seguenti:

  - Componenti di base di Lync Server (OCScore.msi)
    

    > [!NOTE]
    > Se si prevede di utilizzare Lync Server Management Shell per la preparazione di Active Directory, prima di installare OCScore.msi è necessario eseguire la Distribuzione guidata di Lync Server.



  - Microsoft .NET Framework 4.5
    

    > [!NOTE]
    > Per Windows Server 2012 e Windows Server 2012 R2, è necessario installare e attivare .NET Framework 4.5 attraverso Server Manager. Per informazioni dettagliate, vedere "Microsoft .NET Framework 4.5" in <A href="lync-server-2013-additional-software-requirements.md">Requisiti software aggiuntivi per Lync Server 2013</A>. Per Windows Server&nbsp;2008&nbsp;R2, scaricare e installare <A href="http://www.microsoft.com/it-it/download/details.aspx?id=30653">.Net Framework 4.5</A> dal sito Web Microsoft.



  - Strumenti di amministrazione remota del server
    

    > [!NOTE]
    > Se si eseguono le attività di preparazione di Active Directory in un server membro anziché in un controller di dominio, sono necessari alcuni strumenti inclusi in Strumenti di amministrazione remota del server. Installare gli snap-in e gli strumenti da riga di comando di Servizi di dominio Active Directory e il modulo Active Directory per Windows PowerShell dal nodo degli strumenti di Servizi di dominio Active Directory e Active Directory Lightweight Directory Services.



  - Microsoft Visual C++ 11 Redistributable
    

    > [!NOTE]
    > Se il componente non è già presente nel computer, nel corso dell'installazione viene richiesto di installare questo prerequisito. Il pacchetto è fornito in dotazione e non è necessario acquistarlo separatamente.



  - Windows PowerShell 3.0 (64 bit)
    
    Per Windows Server 2012 e Windows Server 2012 R2, Windows PowerShell 3.0 dovrebbe essere incluso nell'installazione di Lync Server 2013. Per Windows Server 2008 R2, è necessario installare o aggiornare a Windows PowerShell 3.0. Per ulteriori informazioni, vedere [Installazione di Windows PowerShell 3.0 per Lync Server 2013](lync-server-2013-installing-windows-powershell-3-0.md).

## Diritti e ruoli amministrativi

Nella tabella seguente vengono indicati i diritti e i ruoli amministrativi necessari per ogni attività di preparazione di Active Directory.

### Diritti utente necessari per la preparazione di Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Procedura</th>
<th>Diritti o ruoli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Preparazione dello schema</p></td>
<td><p>Membro del gruppo Schema Admins per il dominio radice della foresta e diritti di amministratore per il master schema</p></td>
</tr>
<tr class="even">
<td><p>Preparazione della foresta</p></td>
<td><p>Membro del gruppo Enterprise Admins della foresta</p></td>
</tr>
<tr class="odd">
<td><p>Preparazione del dominio</p></td>
<td><p>Membro del gruppo Enterprise Admins o Domain Admins per il dominio specificato</p></td>
</tr>
</tbody>
</table>


## Cmdlet per la preparazione di Active Directory

Nella tabella seguente i cmdlet di Lync Server Management Shell utilizzati per preparare Servizi di dominio Active Directory vengono confrontati ai comandi LcsCmd utilizzati allo stesso scopo in Microsoft Office Communications Server 2007 R2.

### Confronto tra cmdlet e LcsCmd

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>LcsCmd</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Install-CsAdServerSchema</p></td>
<td><p>Lcscmd /forest /action:SchemaPrep /SchemaType:Server</p></td>
</tr>
<tr class="even">
<td><p>Get-CsAdServerSchema</p></td>
<td><p>Lcscmd /forest /action:CheckSchemaPrepState</p></td>
</tr>
<tr class="odd">
<td><p>Enable-CsAdForest</p></td>
<td><p>Lcscmd /forest /action:ForestPrep</p></td>
</tr>
<tr class="even">
<td><p>Disable-CsAdForest</p></td>
<td><p>Lcscmd /forest /action:ForestUnprep</p></td>
</tr>
<tr class="odd">
<td><p>Get-CsAdForest</p></td>
<td><p>Lcscmd /forest /action:CheckForestPrepState</p></td>
</tr>
<tr class="even">
<td><p>Enable-CsAdDomain</p></td>
<td><p>Lcscmd /domain /action:DomainPrep</p></td>
</tr>
<tr class="odd">
<td><p>Disable-CsAdDomain</p></td>
<td><p>Lcscmd /domain /action: DomainUnprep</p></td>
</tr>
<tr class="even">
<td><p>Get-CsAdDomain</p></td>
<td><p>Lcscmd /domain /action:CheckDomainPrepState</p></td>
</tr>
</tbody>
</table>


## Requisiti per un ambiente Active Directory bloccato

Se l'ereditarietà delle autorizzazioni è disabilitata o è necessario disabilitare le autorizzazioni degli utenti autenticati nell'organizzazione, durante la preparazione del dominio sono necessari alcuni passaggi aggiuntivi. Per informazioni dettagliate, vedere [Preparazione di un ambiente Servizi di dominio Active Directory bloccato in Lync Server 2013](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md).

## Autorizzazioni per contenitori personalizzati

Se nell'organizzazione vengono utilizzati contenitori personalizzati anziché i tre contenitori predefiniti, ovvero Utenti, Computer e Controller di dominio, è necessario concedere al gruppo Authenticated Users l'accesso in lettura ai contenitori personalizzati, necessario per la preparazione del dominio. Per informazioni dettagliate, vedere [Preparazione dei domini per Lync Server 2013](lync-server-2013-preparing-domains.md).

## Utilizzo dei cmdlet e di Ldifde.exe

Il passaggio **Prepara schema** della Distribuzione guidata di Lync Server e il cmdlet **Install-CsAdServerSchema** estendono lo schema di Active Directory nei controller di dominio che eseguono un sistema operativo a 64 bit. Se è necessario estendere lo schema di Active Directory in un controller di dominio che esegue un sistema operativo a 32 bit, è possibile utilizzare il cmdlet **Install-CsAdServerSchema** in remoto da un server membro (procedura consigliata). Se è necessario eseguire la preparazione dello schema direttamente nel controller di dominio, è tuttavia possibile utilizzare lo strumento Ldifde.exe per importare i file di schema. Lo strumento Ldifde.exe è incluso nella maggior parte delle versioni del sistema operativo Windows.

Se si utilizza o strumento Ldifde.exe per importare i file di schema è necessario importare tutti e quattro i file, indipendentemente dal fatto che si stia eseguendo la migrazione da una versione precedente oppure un'installazione pulita. I file vanno importati nell'ordine seguente:

1.  ExternalSchema.ldf

2.  ServerSchema.ldf

3.  BackCompatSchema.ldf

4.  VersionSchema.ldf


> [!NOTE]
> I quattro file con estensione ldf si trovano nella directory \Support\Schema del supporto di installazione o del download.



Per utilizzare Ldifde.exe per importare i quattro file di schema in un controller di dominio che funge da master schema, utilizzare il formato seguente:

    ldifde -i -v -k -s <DCName> -f <Schema filename> -c DC=X <defaultNamingContext> -j logFilePath -b <administrator account> <logon domain> <password>

Ad esempio:

    ldifde -i -v -k -s DC1 -f ServerSchema.ldf -c DC=X "DC=contoso,DC=com" -j C:\BatchImportLogFile -b Administrator contoso password


> [!NOTE]
> Utilizzare il parametro b solo se si è effettuato l'accesso come un altro utente. Per informazioni dettagliate sui diritti utente necessari, vedere la sezione "Diritti e ruoli amministrativi" in precedenza in questo argomento.



Per utilizzare Ldifde.exe per importare i quattro file di schema in un controller di dominio che non funge da master schema, utilizzare il formato seguente:

    ldifde -i -v -k -s <SchemaMasterFQDN> -f <Schema filename> -c DC=X <rootDomainNamingContext> -j logFilePath -b <administrator account> <domain> <password>

Per ulteriori informazioni sull'utilizzo di Ldifde, vedere l'articolo 237677 della Microsoft Knowledge Base "Utilizzo di LDIFDE per importare/esportare oggetti directory in Active Directory" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=132204\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=132204%26clcid=0x410).

## Contenuto della sezione

  - [Preparazione dello schema di Active Directory in Lync Server 2013](lync-server-2013-preparing-the-active-directory-schema.md)

  - [Preparazione della foresta per Lync Server 2013](lync-server-2013-preparing-the-forest.md)

  - [Preparazione dei domini per Lync Server 2013](lync-server-2013-preparing-domains.md)

