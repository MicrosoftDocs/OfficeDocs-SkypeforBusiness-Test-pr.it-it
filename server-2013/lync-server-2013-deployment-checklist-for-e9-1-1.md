---
title: "Lync Server 2013: Elenco controllo di distribuz. per i servizi di emergenza"
TOCTitle: Elenco di controllo di distribuzione per i servizi di emergenza
ms:assetid: cc6a656a-6043-4b9b-85c2-5708b9bb1c06
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398864(v=OCS.15)
ms:contentKeyID: 49301991
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per i servizi di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per una pianificazione efficiente del servizio chiamate di emergenza Enhanced 9-1-1 (E9-1-1), includere i requisiti di distribuzione seguenti:

  - Prerequisiti per la distribuzione di E9-1-1.

  - Passaggi necessari per distribuire E9-1-1.

## Prerequisiti per la distribuzione di E9-1-1

Prima di distribuire il servizio E9-1-1, è necessario aver già distribuito i server interni di Lync Server, incluso un archivio di gestione centrale, un pool Front End o un server Standard Edition, uno o più Mediation Server o pool di Mediation Server e i client Lync Server. Inoltre, una distribuzione del servizio E9-1-1 richiede un trunk SIP per un provider di servizi E9-1-1 qualificato o un gateway ELIN (Emergency Location Identification Number) per la rete PSTN (Public Switched Telephone Network). Lync Server supporta l'utilizzo dei provider di servizi E9-1-1 solo negli Stati Uniti.

## Processo di distribuzione

Nella tabella che segue è illustrata una panoramica del processo di distribuzione di E9-1-1. Per informazioni dettagliate sui passaggi di distribuzione, vedere [Configurare i servizi di emergenza avanzati in Lync Server 2013](lync-server-2013-configure-enhanced-9-1-1.md) nella documentazione relativa alla distribuzione.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Ruoli</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configurazione degli utilizzi e delle route vocali e specifica dei trunk</p></td>
<td><ol>
<li><p>Creare un nuovo record di utilizzo PSTN, con lo stesso nome utilizzato per l'impostazione <strong>Utilizzo PSTN</strong> nei criteri percorso.</p></li>
<li><p>Creare o assegnare una route vocale al record di utilizzo PSTN creato nel passaggio precedente e quindi fare in modo che l'attributo del gateway punti al trunk SIP o al gateway ELIN di E9-1-1.</p></li>
<li><p>Per il provider di servizi E9-1-1 di un trunk SIP, impostare il trunk che gestirà le chiamate E9-1-1 tramite SIP in modo che passi i dati PIDF-LO mediante il cmdlet <strong>Set-CsTrunkConfiguration –EnablePIDFLOSupport</strong>.</p></li>
<li><p>Facoltativamente, per il provider di servizi E9-1-1 di un trunk SIP, creare o assegnare una route PSTN locale per le chiamate che non vengono gestite mediante il trunk SIP del provider di servizi E9-1-1. Questa route verrà utilizzata se la connessione al provider di servizi E9-1-1 non è disponibile. Se consentito dal provider di servizi E9-1-1 in uso, assegnare una regola di configurazione del trunk al gateway che converte la stringa da comporre 911 nel numero DID (Direct Inward Dialing) del centro nazionale/regionale ECRC (Emergency Call Response Center).</p></li>
</ol></td>
<td><p>CSVoiceAdmin</p></td>
<td><p><a href="lync-server-2013-configure-an-e9-1-1-voice-route.md">Configurare una route vocale E9-1-1 in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Creazione di criteri di percorso e relativa assegnazione a utenti e subnet</p></td>
<td><ol>
<li><p>Esaminare i criteri di percorso globali.</p></li>
<li><p>Creare criteri percorso con un ambito a livello di utente oppure, se l'organizzazione presenta più siti con utilizzi dei servizi di emergenza diversi, creare criteri percorso a livello di rete.</p></li>
<li><p>Assegnare i criteri di percorso ai siti di rete.</p></li>
<li><p>Aggiungere le subnet appropriate al sito di rete.</p></li>
<li><p>(Facoltativo) Assegnare i criteri percorso a criteri utente.</p></li>
</ol>
<p></p></td>
<td><p>CSVoiceAdmin</p>
<p>CSLocationAdmin (tranne per la creazione dei criteri di percorso)</p></td>
<td><p><a href="lync-server-2013-create-location-policies.md">Creare criteri percorso in Lync Server 2013</a></p>
<p><a href="lync-server-2013-add-a-location-policy-to-a-network-site.md">Aggiungere criteri percorso a un sito di rete</a></p>
<p><a href="lync-server-2013-associate-subnets-with-network-sites-for-e9-1-1.md">Associare subnet a siti di rete per il servizio E9-1-1</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione del database delle posizioni</p></td>
<td><ol>
<li><p>Popolare il database con il mapping degli elementi di rete ai percorsi.</p></li>
<li><p>Per i gateway ELIN, aggiungere i numeri ELIN alla colonna &lt;NomeSocietà&gt;.</p></li>
<li><p>Configurare la connessione al provider di servizi E9-1-1 per la convalida degli indirizzi.</p></li>
<li><p>Convalidare gli indirizzi nel provider di servizi E9-1-1.</p></li>
<li><p>Pubblicare il database aggiornato.</p></li>
<li><p>Per i gateway ELIN, caricare i numeri ELIN nel database ALI (Automatic Location Identification) del gestore telefonico PSTN.</p></li>
</ol></td>
<td><p>CSVoiceAdmin</p>
<p>CSLocationAdmin</p></td>
<td><p><a href="lync-server-2013-configure-the-location-database.md">Configurare il database delle posizioni in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurazione delle funzionalità avanzate (facoltativo)</p></td>
<td><ol>
<li><p>Configurare l'URL dell'applicazione SNMP.</p></li>
<li><p>Configurare l'URL del percorso del servizio Informazioni percorso secondario.</p></li>
</ol></td>
<td><p>CSVoiceAdmin</p></td>
<td><p><a href="lync-server-2013-configure-an-snmp-application.md">Configurare un'applicazione SNMP</a></p>
<p><a href="lync-server-2013-configure-a-secondary-location-information-service.md">Configurare un servizio Informazioni percorso secondario</a></p></td>
</tr>
</tbody>
</table>

