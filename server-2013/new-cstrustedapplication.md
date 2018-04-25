---
title: New-CsTrustedApplication
TOCTitle: New-CsTrustedApplication
ms:assetid: 1c804a97-f9b5-4c3e-adc6-a120b26c1f51
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398259(v=OCS.15)
ms:contentKeyID: 49299857
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge un'applicazione attendibile a un pool. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsTrustedApplication -ApplicationId <String> -TrustedApplicationPoolFqdn <String> <COMMON PARAMETERS>

    New-CsTrustedApplication [-Identity <ExternalApplicationIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Port <Int32> [-Confirm [<SwitchParameter>]] [-EnableTcp <SwitchParameter>] [-Force <SwitchParameter>] [-LegacyApplicationName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio consente di creare un'applicazione attendibile con Application ID tapp1. Viene utilizzato il parametro TrustedApplicationPoolFqdn per specificare il pool di appartenenza dell'applicazione; in questo caso si tratta del pool con FQDN TrustPool.litwareinc.com. Inoltre, occorre specificare una porta per l'applicazione; in questo esempio viene usata la porta 6000. Si noti che l'esecuzione di questo cmdlet con i valori specificati per i parametri ApplicationId e TrustedApplicationPoolFqdn comporta la creazione automatica di un'identità che potrà essere utilizzata successivamente per recuperare, modificare o rimuovere questa applicazione.

    New-CsTrustedApplication -ApplicationId tapp1 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com -Port 6000

## ESEMPIO 2

In questo esempio viene creata un'applicazione attendibile con Identity TrustPool.litwareinc.com/tapp2 sulla porta (Port) 6100. Si noti il formato del valore di Identity. Questo valore deve essere nel formato \<FQDN pool attendibile\>/\<ID applicazione\>.

    New-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2 -Port 6100

## Descrizione dettagliata

Un'applicazione attendibile è un'applicazione sviluppata da terze parti alla quale è stato assegnato lo stato di attendibile per essere eseguita come parte di Lync Server, ma che non è parte integrante del prodotto. Questo cmdlet aggiunge un'applicazione attendibile a un pool di applicazioni attendibili e assegna una porta al servizio esterno che esegue l'applicazione.

Le applicazioni attendibili devono essere associate ai GRUU (Globally Routable User Agent URI) sia del servizio sia del computer. Questo cmdlet crea automaticamente questi valori in base ai computer e servizi associati al pool che ospita l'applicazione.

Quando viene utilizzato questo cmdlet per creare un'applicazione affidabile, è necessario fornire il valori del parametro Identity o dei parametri ApplicationID e TrustedApplicationPoolFqdn. L'identità è data dal valore del parametro TrustedApplicationPoolFqdn seguito da una barra (/) e quindi dal valore del parametro ApplicationID. Ad esempio, TrustPool.litwareinc.com/tapp2, dove TrustPool.litwareinc.com è TrustedApplicationPoolFqdn e tapp2 è ApplicationID.

Si noti che quando viene immesso un ID applicazione, come parte del parametro Identity o ApplicationID, occorre immettere solo il nome dell'applicazione. Tuttavia, all'ID applicazione completo verrà automaticamente aggiunto il prefisso urn:application:. Ad esempio, se viene immesso il valore tapp2 per ApplicationID, quell'ID verrà memorizzato nel formato urn:application:tapp2. Allo stesso modo, se viene immessa l'identità TrustPool.litwareinc.com/tapp2, essa verrà memorizzata nel sistema nel formato TrustPool.litwareinc.com/urn:application:tapp2.

Se viene specificato il valore del parametro Port tramite questo cmdlet, il cmdlet non apre la porta. È necessario aprire la porta in Windows Firewall e in eventuali firewall aziendali affinché l'applicazione attendibile possa entrare in contatto con le reti esterne al firewall.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsTrustedApplication** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplication\\b"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ApplicationId</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'applicazione. Questo nome deve essere una stinga univoca nell'ambito del pool specificato nel parametro TrustedApplicationPoolFqdn. La stringa non può contenere spazi. Se viene fornito un valore per il parametro ApplicationId, è necessario specificare un valore anche per il parametro TrustedApplicationPoolFqdn. Non è possibile specificare un valore per ApplicationId e un valore per Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Port</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero della porta sulla quale verrà eseguita l'applicazione. La porta deve essere univoca in un determinato pool. In altre parole, nel pool specificato non possono essere definite altre applicazioni che utilizzano questa stessa porta.</p></td>
</tr>
<tr class="odd">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome FQDN del pool di applicazioni attendibili nel quale risiederà l'applicazione. Se viene fornito un valore per il parametro TrustedApplicationPoolFqdn, occorre fornire un valore anche per il parametro ApplicationId, ma non per il parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTcp</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare che l'applicazione attendibile utilizza il protocollo TCP (Transmission Control Protocol). Utilizzare questo parametro solo l'applicazione attendibile non è un'applicazione Microsoft Unified Communications Managed API (UCMA). Questo perché le applicazioni UCMA supportano solo il protocollo MTLS (Mutual Transport Layer Security). Se non viene specificato il parametro Force con il parametro EnableTcp, viene visualizzato un messaggio di richiesta di conferma prima che l'applicazione attendibile venga creata.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>Identificatore univoco dell'applicazione attendibile nel pool. I valori di Identity devono essere immessi nel formato &lt;FQDN pool&gt;/&lt;ID applicazione&gt;, dove FQDN pool è il nome di dominio completo (FQDN) del pool nel quale risiede l'applicazione e ID applicazione è il nome dell'applicazione. L'ID applicazione deve essere univoco per un determinato pool.</p>
<p>Se si specifica un valore per Identity, non è possibile specificare valori anche per i parametri ApplicationId o TrustedApplicationPoolFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>LegacyApplicationName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Utilizzare questo parametro solamente se si sta eseguendo la migrazione dell'applicazione da una distribuzione Microsoft Office Communications Server 2007 R2. Affinché queste due distribuzioni possano coesistere, questo valore deve essere uguale a quello del tipo GRUU della versione Office Communications Server 2007 R2 dell'applicazione.</p>
<p>Si noti che nella maggior parte dei casi, è sufficiente impostare il parametro ApplicationID su un valore uguale a quello del tipo GRUU perché le applicazioni possano coesistere. Tuttavia, se il tipo GRUU dell'applicazione Office Communications Server 2007 R2 contiene dei caratteri che non sono validi in ApplicationID, è necessario specificare quel valore nel parametro LegacyApplicationName.</p>
<p>Se non si specifica un valore per questo parametro, verrà automaticamente inserito il valore di ApplicationID senza il prefisso urn:application:.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayTrustedApplication.

## Vedere anche

#### Ulteriori risorse

[Remove-CsTrustedApplication](remove-cstrustedapplication.md)  
[Set-CsTrustedApplication](set-cstrustedapplication.md)  
[Get-CsTrustedApplication](get-cstrustedapplication.md)

