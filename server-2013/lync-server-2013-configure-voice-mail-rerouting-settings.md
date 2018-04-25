---
title: 'Lync Server 2013: Configurare le impostazioni di rerouting della segreteria telefonica'
TOCTitle: Configurare le impostazioni di rerouting della segreteria telefonica
ms:assetid: 7ab6be28-eabb-4a79-a796-648887d71b83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398606(v=OCS.15)
ms:contentKeyID: 49301077
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le impostazioni di rerouting della segreteria telefonica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

I sistemi Survivable Branch Appliance e Survivable Branch Server sono in grado di garantire il funzionamento della segreteria telefonica per gli utenti di siti derivati durante un problema della rete WAN, se la Messaggistica unificata di Exchange è installata nel sito centrale ed è distribuito un Operatore automatico per i messaggi della Messaggistica unificata di Exchange. È opportuno che l'amministratore di Exchange configuri l'Operatore automatico in modo che accetti solo i messaggi, disabilitando altre funzionalità generiche come il trasferimento a un utente o a un operatore. In alternativa, è possibile utilizzare un Operatore automatico generico o personalizzato per il routing della chiamata.

Per informazioni dettagliate, vedere la sezione relativa alle attività preparatorie per garantire il funzionamento della segreteria telefonica in [Requisiti di resilienza dei siti di succursale per Lync Server 2013](lync-server-2013-branch-site-resiliency-requirements.md) nella documentazione relativa alla pianificazione.

## Per configurare il funzionamento ininterrotto della segreteria telefonica

1.  Chiedere all'amministratore di Exchange di configurare l'Operatore automatico in modo che accetti solo i messaggi. Nella shell di Exchange utilizzare il seguente cmdlet: **Set-UMAutoAttendant \<AA name\> -CallSomeoneEnabled $false**. Il parametro che specifica di lasciare i messaggi ( *SendVoiceMsgEnabled*) è true per impostazione predefinita.

2.  In Lync Server Management Shell utilizzare il cmdlet **New-CSVoiceMailReroutingConfiguration** per impostare il numero di telefono dell'Operatore automatico come numero di telefono dell'Operatore automatico della Messaggistica unificata di Exchange nella configurazione di rerouting della segreteria telefonica in Survivable Branch Appliance o Survivable Branch Server.
    

    > [!NOTE]
    > Se in seguito sarà necessario modificare l'impostazione di rerouting della segreteria telefonica, utilizzare il cmdlet <STRONG>Set-CsVoiceMailReRoutingConfiguration</STRONG> a tale scopo. Per informazioni dettagliate su <STRONG>New-</STRONG>, vedere <STRONG>Set-CSVoiceMailReroutingConfiguration</STRONG> negli argomenti della Guida della shell.



3.  Impostare il numero di accesso del sottoscrittore della Messaggistica unificata di Exchange che corrisponde al dial plan della Messaggistica unificata di Exchange degli utenti di siti derivati come numero di accesso del sottoscrittore della Messaggistica unificata di Exchange nella configurazione di rerouting della segreteria telefonica in Survivable Branch Appliance o Survivable Branch Server.
    

    > [!NOTE]
    > Configurare il dial plan degli utenti della Messaggistica unificata di Exchange in modo che vi sia un solo dial plan associato a tutti gli utenti di siti derivati che devono accedere alla funzionalità di posta vocale durante un problema della rete WAN.



**Passaggio successivo** per Survivable Branch Appliance o Survivable Branch Server: [Ospitare utenti in Survivable Branch Appliance o Survivable Branch Server in Lync Server 2013](lync-server-2013-home-users-on-a-survivable-branch-appliance-or-server.md).

