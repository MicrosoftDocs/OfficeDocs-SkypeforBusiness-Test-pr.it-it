---
title: Riepilogo dei certificati - federazione di XMPP (Extensible Messaging and Presence Protocol)
TOCTitle: Riepilogo dei certificati - federazione di XMPP (Extensible Messaging and Presence Protocol)
ms:assetid: b059a34e-99df-40af-91fe-fe2aa52841f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618374(v=OCS.15)
ms:contentKeyID: 49301681
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - federazione di XMPP (Extensible Messaging and Presence Protocol)

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Tra i requisiti dei certificati per consentire e stabilire le comunicazioni con partner XMPP (Extensible Messaging and Presence Protocol) è previsto il record aggiuntivo dei domini XMPP. Il record incluso nel certificato come nome alternativo del soggetto (SAN) corrisponderà al dominio che può partecipare alle comunicazioni XMPP. Il dominio può essere a livello della radice (ad esempio, contoso.com) se si desidera abilitare XMPP per l'intero dominio oppure può corrispondere a domini figlio selezionati (ad esempio, corp.contoso.com, finance.contoso.com) se si desidera abilitare XMPP per un sottoinsieme di utenti.

## Riepilogo certificati per XMPP (Extensible Messaging and Presence Protocol)


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Nome soggetto</th>
<th>Nomi alternativi soggetto (SAN)/Ordine</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Assegnazione al servizio Access Edge del server perimetrale o del pool di server perimetrali</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p>
<p>contoso.com</p></td>
<td><p>Le prime tre voci SAN sono le voci SAN normali per un server perimetrale completo. La voce contoso.com è necessaria per la federazione con il partner XMPP a livello del dominio radice. Questa voce consentirà l'utilizzo di XMPP per tutti i domini con il suffisso contoso.com.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Esempio di configurazione XMPP in Lync Server 2013 - federazione di XMPP con Google Talk](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### Concetti

[Pianificare i certificati dei server perimetrali in Lync Server 2013](lync-server-2013-plan-for-edge-server-certificates.md)  

#### Ulteriori risorse

[Configurare i certificati perimetrali per Lync Server 2013](lync-server-2013-set-up-edge-certificates.md)  
[Request-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Request-CsCertificate)  
[Set-CsCertificate](set-cscertificate.md)

