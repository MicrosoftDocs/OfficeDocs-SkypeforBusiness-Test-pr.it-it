---
title: Pianificazione per la federazione di XMPP (Extensible Messaging and Presence Protocol) in Lync Server 2013
TOCTitle: Pianificazione per la federazione di XMPP (Extensible Messaging and Presence Protocol) in Lync Server 2013
ms:assetid: 952b33e2-1f58-4831-9a39-1dfec2a316ad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205107(v=OCS.15)
ms:contentKeyID: 49301362
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione per la federazione di XMPP (Extensible Messaging and Presence Protocol) in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Le versioni precedenti di Lync Server e Office Communications Server includono un gateway XMPP (Extensible Messaging and Presence Protocol) che può essere distribuito come ruolo server separato per consentire la federazione con distribuzioni XMPP. In Microsoft Lync Server 2013, la funzionalità XMPP può essere distribuita come funzionalità. La funzionalità XMPP viene installata in due parti: un proxy XMPP che viene eseguito nel server perimetrale e il gateway XMPP che viene eseguito nei Front End Server.

La distribuzione e la configurazione di XMPP sono illustrate in [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md). Per pianificare il supporto di XMPP in un'organizzazione, occorre definire le regole delle porte e del protocollo nel firewall, la configurazione dei certificati e l'aggiunta dei record DNS. Negli argomenti seguenti di questa sezione vengono riepilogate le informazioni necessarie per pianificare correttamente la federazione XMPP per la distribuzione.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La funzionalità XMPP di Lync Server 2013 è testata e supportata da Microsoft per la federazione di messaggistica istantanea con Google Talk. Per altri sistemi XMPP, contattare il fornitore di terze parti per verificare l'eventuale supporto della federazione con Lync Server 2013 e per indicazioni per la distribuzione o la risoluzione dei problemi.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Riepilogo dei certificati - federazione di XMPP (Extensible Messaging and Presence Protocol)](lync-server-2013-certificate-summary-extensible-messaging-and-presence-protocol-xmpp-federation.md)

  - [Riepilogo delle porte - federazione di XMPP (Extensible Messaging and Presence Protocol)](lync-server-2013-port-summary-extensible-messaging-and-presence-protocol-xmpp-federation.md)

  - [Riepilogo di DNS - federazione di XMPP (Extensible Messaging and Presence Protocol)](lync-server-2013-dns-summary-extensible-messaging-and-presence-protocol-xmpp-federation.md)

## Vedere anche

#### Attività

[Configurazione della federazione di XMPP in Lync Server 2013](lync-server-2013-setting-up-xmpp-federation.md)  
[Configurare criteri per controllare l'accesso utente federato XMPP in Lync Server 2013](lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md)  

#### Ulteriori risorse

[Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)  
[Get-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExternalAccessPolicy)  
[Get-CsXmppAllowedPartner](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsXmppAllowedPartner)  
[Get-CsXmppGatewayConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsXmppGatewayConfiguration)

