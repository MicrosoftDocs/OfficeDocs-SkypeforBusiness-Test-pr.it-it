---
title: Pianificazione dell'autenticazione a due fattori
TOCTitle: Pianificazione dell'autenticazione a due fattori
ms:assetid: 16f08710-8961-4659-acbf-ebb95a198fb4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308562(v=OCS.15)
ms:contentKeyID: 56269891
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione dell'autenticazione a due fattori

 

_**Ultima modifica dell'argomento:** 2015-04-06_

Di seguito è riportato un elenco di considerazioni sulla distribuzione per la configurazione di un ambiente Microsoft Lync Server 2013per il supporto dell'autenticazione a due fattori.

## Supporto per client

Il client desktop disponibile con gli aggiornamenti cumulativi per Lync Server 2013 di giugno 2013 per Lync 2013 è l'unico client Lync che attualmente supporta l'autenticazione a due fattori.

## Requisiti della topologia

I clienti sono invitati a distribuire l'autenticazione a due fattori usando i ruoli del server Edge, Director e User Pool di Lync Server 2013 con gli aggiornamenti cumulativi per Lync Server 2013: luglio 2013. Per abilitare l'autenticazione passiva per gli utenti di Lync, è necessario disabilitare altri metodi di autenticazione per altri ruoli e servizi, inclusi quelli riportati di seguito:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di configurazione</th>
<th>Tipo di servizio</th>
<th>Ruolo server</th>
<th>Tipo di autenticazione da disabilitare</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servizio Web</p></td>
<td><p>WebServer</p></td>
<td><p>Director</p></td>
<td><p>Kerberos, NTLM e autenticazione del certificato</p></td>
</tr>
<tr class="even">
<td><p>Servizio Web</p></td>
<td><p>WebServer</p></td>
<td><p>Front End</p></td>
<td><p>Kerberos, NTLM e autenticazione del certificato</p></td>
</tr>
<tr class="odd">
<td><p>Proxy</p></td>
<td><p>EdgeServer</p></td>
<td><p>Edge</p></td>
<td><p>Kerberos e NTLM</p></td>
</tr>
<tr class="even">
<td><p>Proxy</p></td>
<td><p>Registrar</p></td>
<td><p>Front End</p></td>
<td><p>Kerberos e NTLM</p></td>
</tr>
</tbody>
</table>


Se questi tipi di autenticazione non sono disabilitati al livello del servizio, tutte le altre versioni del client Lync non saranno in grado di eseguire l'accesso dopo avere abilitato l'autenticazione a due fattori nella distribuzione in uso.

## Individuazione servizio Lync

I record DNS usati dai client interni e/o esterni per l'individuazione dei servizi Lync devono essere configurati in modo da puntare a un server Lync non abilitato per l'autenticazione a due fattori. Con questa configurazione, agli utenti dei pool di Lync non abilitati per l'autenticazione a due fattori non verrà richiesto di immettere un PIN per l'autenticazione, mentre agli utenti dei pool di Lync abilitati per l'autenticazione a due fattori verrà richiesto di immettere il PIN.

## Autenticazione di Exchange

Per i clienti che hanno distribuito l'autenticazione a due fattori per Microsoft Exchange, alcune funzionalità del client Lync non sono disponibili. Si tratta di un comportamento legato alla progettazione del prodotto, in quanto il client Lync non supporta l'autenticazione a due fattori per funzionalità che dipendono dall'integrazione di Exchange.

## Contatti di Lync

Per gli utenti di Lync configurati per l'uso della funzionalità Archivio contatti unificato, i contatti non saranno più disponibili dopo avere eseguito l'accesso con l'autenticazione a due fattori.

Usare il cmdlet **Invoke-CsUcsRollback** per rimuovere i contatti esistenti dell'utente dall'archivio contatti unificato e archiviarli in Lync Server 2013 prima di abilitare l'autenticazione a due fattori.

## Ricerca per competenza

Per i clienti che hanno configurato la funzionalità di ricerca per competenza nell'ambiente Lync, la funzionalità non funziona quando Lync è abilitato per l'autenticazione a due fattori. Si tratta di un comportamento legato alla progettazione del prodotto, in quanto Microsoft SharePoint attualmente non supporta l'autenticazione a due fattori.

## Credenziali di Lync

Numerose considerazioni sulla distribuzione riguardano le credenziali di Lync salvate che possono influire sugli utenti configurati per l'uso dell'autenticazione a due fattori.

## Eliminazione di credenziali salvate

Gli utenti devono usare l'opzione **Elimina le informazioni di accesso** nel client Lync ed eliminare la cartella del proprio profilo SIP da %localappdata%\\Microsoft\\Office\\15.0\\Lync prima di tentare di accedere per la prima volta con l'autenticazione a due fattori.

## DisableNTCredentials

Con il metodo di autenticazione Kerberos o NTLM, per l'autenticazione vengono usate automaticamente le credenziali di Windows dell'utente. In una distribuzione di Lync Server 2013 tipica in cui Kerberos o NTLM è abilitato per l'autenticazione, gli utenti non devono immettere le proprie credenziali ogni volta che eseguono l'accesso.

Se agli utenti viene inavvertitamente richiesto di immettere le credenziali prima che venga richiesto di immettere il PIN, è possibile che la chiave del Registro di sistema **DisableNTCredentials** sia stata inavvertitamente configurata nei computer client, possibilmente tramite i Criteri di gruppo.

Per evitare questa ulteriore richiesta di credenziali, creare la voce del Registro di sistema seguente nella workstation locale o usare il modello amministrativo di Lync per applicarla a tutti gli utenti di un determinato pool tramite Criteri di gruppo:

HKEY\_LOCAL\_MACHINE\\Software\\Policies\\Microsoft\\Office\\15.0\\Lync

REG\_DWORD: DisableNTCredentials

Valore: 0x0

## SavePassword

Quando un utente accede a Lync per la prima volta, gli viene richiesto di salvare la password. Se questa opzione è selezionata, il certificato client dell'utente verrà archiviato nell'archivio dei certificati personali e le credenziali Windows dell'utente verranno archiviate in Gestione credenziali nel computer locale.

L'impostazione del Registro di sistema **SavePassword** deve essere disabilitata quando Lync è configurato per supportare l'autenticazione a due fattori. Per evitare che gli utenti salvino le proprie password, modificare la voce del Registro di sistema seguente nella workstation locale o usare il modello amministrativo di Lync per applicarla a tutti gli utenti di un determinato pool tramite Criteri di gruppo:

HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\15.0\\Lync

REG\_DWORD: SavePassword

Valore: 0x0

## Riproduzione token di ADFS 2.0

ADFS 2.0 offre una caratteristica denominata rilevamento riproduzione token, in base alla quale è possibile individuare ed eliminare più richieste token che usano lo stesso token. Quando questa caratteristica è abilitata, il rilevamento della riproduzione token protegge l'integrità delle richieste di autenticazione sia nel profilo passivo WS-Federation sia nel profilo WebSSO SAML garantendo che lo stesso token non venga mai usato più di una volta.

Questa caratteristica deve essere abilitata nelle situazioni in cui la sicurezza presenta rischi elevati, ad esempio nell'uso dei chioschi. Per ulteriori informazioni sul rilevamento della riproduzione dei token, vedere le procedure consigliate relative alla pianificazione e alla distribuzione sicure di ADFS 2.0 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=309215](http://go.microsoft.com/fwlink/p/?linkid=309215).

## Accesso utenti esterni

La configurazione di un proxy ADFS o di un proxy inverso per il supporto dell'autenticazione a due fattori di Lync da reti esterne non è trattata in questi argomenti.

