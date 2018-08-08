---
title: "Lync Server 2013: Guida alle impostazioni dei criteri di conferenza"
TOCTitle: "Lync Server 2013: Guida alle impostazioni dei criteri di conferenza"
ms:assetid: ec8125f7-ef78-4a2b-8db0-4dd3cf5a4065
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429724(v=OCS.15)
ms:contentKeyID: 49302362
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-04-22_

Nelle tabelle di questo argomento sono elencate tutte le impostazioni dei criteri di conferenza che è possibile specificare utilizzando il Pannello di controllo di Lync Server 2013.

## Impostazione dei criteri per organizzatori

Nella tabella seguente sono elencate tutte le impostazioni dei criteri di conferenza applicabili agli organizzatori di conferenze. Per l'elenco aggiornato delle impostazioni dei criteri di conferenza, vedere l'argomento della Guida per il cmdlet [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy).

### Impostazione dei criteri per organizzatori

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensione massima riunione</p></td>
<td><p>Imposta il numero massimo di partecipanti consentiti a una riunione.</p></td>
</tr>
<tr class="even">
<td><p>Consenti ai partecipanti di invitare utenti anonimi</p></td>
<td><p>Consente agli organizzatori di riunioni di invitare a partecipare utenti non autenticati.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita registrazione</p></td>
<td><p>Consente a relatori o partecipanti di registrare la riunione.</p></td>
</tr>
<tr class="even">
<td><p>Consenti ai partecipanti anonimi e federati di registrare</p></td>
<td><p>Consente a partecipanti esterni e non autenticati di registrare la riunione.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita audio IP</p></td>
<td><p>Consente l'utilizzo di audio in una riunione.</p></td>
</tr>
<tr class="even">
<td><p>Abilita audio/video IP</p></td>
<td><p>Consente l'utilizzo di audio e video in una riunione.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti conferenza telefonica con accesso esterno PSTN</p></td>
<td><p>Consente all'utente di partecipare a una riunione tramite accesso esterno dalla rete PSTN (Public Switched Telephone Network).</p></td>
</tr>
<tr class="even">
<td><p>Consenti chiamate in uscita ai partecipanti anonimi</p></td>
<td><p>Consente a utenti non autenticati di partecipare a una riunione mediante chiamate in uscita. . Con le chiamate in uscita il server per conferenze telefona all'utente, il quale accederà alla riunione rispondendo al telefono.</p></td>
</tr>
<tr class="odd">
<td><p>Risoluzione video massima consentita per le conferenze</p></td>
<td><p>Imposta la risoluzione massima per le videoconferenze. I valori validi sono <strong>640*480(VGA)</strong> e <strong>352*288(CIF)</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Abilita collaborazione dati</p></td>
<td><p>Abilita le conferenze con collaborazione dati o le conferenze Web.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti ai partecipanti anonimi e federati di scaricare contenuto</p></td>
<td><p>Consente a partecipanti esterni e non autenticati di scaricare contenuto dalla riunione.</p></td>
</tr>
<tr class="even">
<td><p>Consenti ai partecipanti di trasferire file</p></td>
<td><p>Consente ai partecipanti di trasferire file durante una riunione.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti annotazioni</p></td>
<td><p>Consente ai partecipanti di creare annotazioni nel contenuto della riunione.</p></td>
</tr>
<tr class="even">
<td><p>Consenti sondaggi</p></td>
<td><p>Consente ai partecipanti di condurre un sondaggio durante una riunione.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti condivisione applicazioni</p></td>
<td><p>Consente agli utenti di pianificare riunioni che supportano la condivisione di applicazioni.</p></td>
</tr>
<tr class="even">
<td><p>Consenti ai partecipanti di assumere il controllo</p></td>
<td><p>Consente ai partecipanti di assumere il controllo dell'applicazione condivisa di un altro utente.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti ai partecipanti anonimi e federati di assumere il controllo</p></td>
<td><p>Consente a partecipanti esterni e anonimi di assumere il controllo dell'applicazione condivisa di un altro utente.</p>

> [!NOTE]
> Se questa opzione è impostata su True e l'opzione <STRONG>Consenti ai partecipanti di assumere il controllo</STRONG> è impostata su False, questa opzione viene ignorata.


</td>
</tr>
</tbody>
</table>


## Impostazioni dei criteri per partecipanti

Nella tabella seguente sono elencate tutte le impostazioni dei criteri di conferenza applicabili ai partecipanti a conferenze.

### Impostazioni dei criteri per partecipanti

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Consenti condivisione applicazioni</p></td>
<td><p>Consente agli utenti di pianificare riunioni che supportano la condivisione di applicazioni.</p></td>
</tr>
<tr class="even">
<td><p>Abilita condivisione applicazioni e desktop</p></td>
<td><p>Consente agli utenti di partecipare a riunioni che supportano la condivisione di applicazioni e del desktop. In una conferenza il valore di questa impostazione che si applica all'organizzatore della conferenza verrà applicato a tutti gli endpoint anonimi che vi partecipano.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti trasferimento di file tramite peer-to-peer</p></td>
<td><p>Consente ai partecipanti di eseguire trasferimenti di file peer-to-peer durante una riunione. Un trasferimento di questo tipo non coinvolge tutti i partecipanti alla riunione.</p></td>
</tr>
<tr class="even">
<td><p>Consenti registrazione peer-to-peer</p></td>
<td><p>Consente ai partecipanti di registrare le sessioni di conferenza peer-to-peer.</p></td>
</tr>
</tbody>
</table>

