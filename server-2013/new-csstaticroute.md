---
title: New-CsStaticRoute
TOCTitle: New-CsStaticRoute
ms:assetid: 1df0c537-f24f-4a63-be6d-70d016f985a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398265(v=OCS.15)
ms:contentKeyID: 49299865
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsStaticRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova route telefonica statica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsStaticRoute -Destination <String> -MatchUri <String> -Port <UInt16> -TLSRoute <SwitchParameter> [-Enabled <$true | $false>] [-MatchOnlyPhoneUri <$true | $false>] [-ReplaceHostInRequestUri <$true | $false>] [-TLSCertIssuer <String>] [-TLSCertSerialNumber <Byte[]>] [-UseDefaultCertificate <$true | $false>] <COMMON PARAMETERS>

    New-CsStaticRoute -Destination <String> -MatchUri <String> -Port <UInt16> -TCPRoute <SwitchParameter> [-Enabled <$true | $false>] [-MatchOnlyPhoneUri <$true | $false>] [-ReplaceHostInRequestUri <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 creano una nuova route statica e quindi la aggiungono alla raccolta di configurazione del routing statico nell'ambito globale. A tale scopo, il primo comando utilizza il cmdlet **New-CsStaticRoute** per creare solo in memoria una route che utilizza TCP come protocollo di trasporto. La route punta all'indirizzo IP 192.168.0.100 dell'hop successivo, utilizza la porta 8025 e include tutti gli URI del dominio litwareinc.com. L'oggetto route risultante viene archiviato in una variabile denominata $x.

Il secondo comando dell'esempio quindi aggiunge la nuova route alla raccolta di configurazione del routing statico globale. A tale scopo, viene chiamato il cmdlet **Set-CsStaticRoutingConfiguration** con il parametro Route. Il valore @{Add=$x} del parametro aggiunge l'oggetto route archiviato in $x all'insieme di route già presenti nella raccolta globale.

    $x = New-CsStaticRoute -TCPRoute -Destination "192.168.0.100" -Port 8025 -MatchUri "litwareinc.com" 
    
    Set-CsStaticRoutingConfiguration -Identity global -Route @{Add=$x}

## ESEMPIO 2

Nell'esempio 2 viene mostrato come creare una nuova route statica che utilizza TLS come protocollo di trasporto e quindi aggiungerla alla raccolta di configurazione del routing statico globale. A tale scopo, il primo comando riportato nell'esempio utilizza il cmdlet **New-CsStaticRoute** per creare solo in memoria una route che utilizza TLS come protocollo di trasporto. La route punta all'indirizzo "atl-proxy-001.litwareinc.com" come destinazione, utilizza la porta 8025 e include tutti gli URI con il suffisso di dominio "litwareinc.com". Il nuovo oggetto route, archiviato in una variabile denominata $x, inoltre utilizza il certificato predefinito per le procedure di autenticazione (-UseDefaultCertificate $True).

Una volta creato l'oggetto route, il secondo comando nell'esempio consente di aggiungere la nuova route alla raccolta di configurazione del routing statico nell'ambito globale.

    $x = New-CsStaticRoute -TLSRoute -Destination "atl-proxy-001.litwareinc.com" -Port 8025 -MatchUri "*.litwareinc.com" -UseDefaultCertificate $True
    
    Set-CsStaticRoutingConfiguration -Identity global -Route @{Add=$x}

## ESEMPIO 3

Nell'esempio 3 viene creata una nuova route statica utilizzando TLS e un certificato specifico, come indicato dai parametri TLS obbligatori inclusi.

Una volta creato l'oggetto route, il secondo comando nell'esempio consente di aggiungere la nuova route alla raccolta di configurazioni del routing statico nell'ambito globale.

    $x = New-CsStaticRoute -TLSRoute -Destination "atl-proxy.litwareinc.com" -Port 5061 -MatchUri "litwareinc.com" -UseDefaultCertificate $False -TLSCertIssuer "CN=CertificateAuthority, DC=litwareinc, DC=com" -TLSCertSerialNumber 0x8f,0x33,0x70,0x93,0x70,0x05,0x33,0x00,0x02,0x33
    
    Set-CsStaticRoutingConfiguration -Identity global -Route @{Add=$x}

## Descrizione dettagliata

Quando si invia un messaggio SIP a qualcuno, quel messaggio potrebbe dover attraversare più subnet e reti prima di essere consegnato; il percorso effettuato dal messaggio viene spesso chiamato "route". Nelle reti, esistono due tipi di route: dinamiche e statiche. Con le route dinamiche, i server utilizzano degli algoritmi per stabilire la destinazione successiva (prossimo hop) dove inoltrare il messaggio. Con le route statiche, il percorso del messaggio viene stabilito a priori dagli amministratori di sistema. Quando un messaggio viene ricevuto da un server, questo controlla l'indirizzo del messaggio e lo inoltra al prossimo server che è stato preconfigurato da un amministratore. Se configurate correttamente le route statiche aiutano ad assicurare una tempestiva ed accurata consegna del messaggio senza sovraccarico sul server. Lo svantaggio delle route statiche è rappresentato dal fatto che i messaggi non vengono dinamicamente reinstradati nel caso di un errore di rete.

Le nuove route statiche vengono create utilizzando il cmdlet **New-CsStaticRoute**. Dopo che la route è stata creata tramite il cmdlet **New-CsStaticRoute**, è necessario aggiungerla a una raccolta di impostazioni di configurazione del routing utilizzando li cmdlet **Set-CsStaticRoutingConfiguration**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsStaticRoute** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsStaticRoute"}

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
<td><p><em>Destination</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Se la route utilizza il protocollo TLS (Transport Layer Security) come protocollo di trasporto, il valore del parametro Destination è il nome di dominio completo del server hop successivo. Ad esempio: -Destination &quot;atl-proxy-001.litwareinc.com&quot;.</p>
<p>Se la route utilizza il protocollo TCP (Transmission Control Protocol) come protocollo di trasporto, il valore del parametro Destination è l'indirizzo IP del router hop successivo. Ad esempio: -Destination &quot;192.168.0.240&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MatchUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo (FQDN) o il suffisso di dominio utilizzato per stabilire se il messaggio è diretto a un utente gestito da questa route. Ad esempio, è possibile utilizzare il nome FQDN &quot;litwareinc.com&quot;. Questo modello include tutti gli utenti con indirizzo SIP che termina con il nome di dominio &quot;litwareinc.com&quot;.</p>
<p>Per includere tutti i domini figli di un dominio, è possibile utilizzare un valore con carattere jolly come &quot;*.litwareinc.com&quot;. Questo valore include tutti i domini che terminano con il suffisso &quot;litwareinc.com&quot;. Ad esempio: northamerica.litwareinc.com; asia.litwareinc.com; europe.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta usato per il routing SIP. Ad esempio: -Port 7742.</p></td>
</tr>
<tr class="even">
<td><p><em>TCPRoute</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di configurare il protocollo TCP come protocollo di trasporto della nuova route.</p></td>
</tr>
<tr class="odd">
<td><p><em>TLSRoute</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di configurare il protocollo TLS come protocollo di trasporto della nuova route.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, la route è abilitata e per tutti i messaggi conformi al modello MatchURI verrà effettuato il routing al server hop successivo. Se impostato su False, la route è disabilitata e non verrà utilizzata per il routing dei messaggi. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>MatchOnlyPhoneUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, solo i messaggi indirizzati agli URI telefonici (ad esempio, sip:kenmmyer@litwareinc.com;user=phone) verranno inclusi ed eventualmente inoltrati. Se impostato su False (il valore predefinito), vengono inclusi tutti i messaggi.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplaceHostInRequestUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True ($True), la porzione host di un URI richiesta verrà sostituita dall'indirizzo del server hop successivo. Se impostato su False, l'URI richiesta verrà utilizzato senza alterazioni. L'URI richiesta rappresenta l'URI dell'utente o servizio a cui è indirizzata la richiesta (messaggio). Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>TLSCertIssuer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'Autorità di certificazione che ha emesso il certificato da utilizzare nella route statica. Questo parametro non viene utilizzato, se non è stato configurato il protocollo TCP come protocollo di trasporto.</p>
<p>Se viene incluso il parametro TLSCertIssuer, occorre anche utilizzare il parametro TLSCertSerialNumber.</p></td>
</tr>
<tr class="even">
<td><p><em>TLSCertSerialNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Il numero di serie del certificato TLS da utilizzare nella route statica. I numeri di serie devono essere specificati sotto forma di matrice di byte; ciò significa che occorre specificare il numero di serie sotto forma di una matrice di valori di due caratteri. Ad esempio: -TLSCertSerialNumber 0x01, 0xA4, 0xD5, 0x67, 0x89.</p>
<p>Questo parametro non viene utilizzato, se non è stato configurato il protocollo TCP come protocollo di trasporto.</p>
<p>Se viene incluso il parametro TLSCertSerialNumber, occorre anche utilizzare il parametro TLSCertIssuer.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseDefaultCertificate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Configura la route in modo da utilizzare il certificato Lync Server predefinito come certificato di autenticazione. Se non si desidera utilizzare il certificato predefinito, è necessario specificarne un altro utilizzando i parametri TLSCertIssuer e TLSCertSerialNumber.</p>
<p>Per visualizzare i certificati predefiniti, utilizzare il seguente comando:</p>
<p>Get-CsCertificate | Where-Object {$_.Use –eq &quot;urn:certref:Default&quot;}</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsStaticRoute** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsStaticRoute** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Route.

## Vedere anche

#### Ulteriori risorse

[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

