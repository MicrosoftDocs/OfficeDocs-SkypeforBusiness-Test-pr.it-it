---
title: 'Lync Server 2013: Delegare le autorizzazioni di installazione'
TOCTitle: Delegare le autorizzazioni di installazione
ms:assetid: 9dca1683-4c69-4534-8ebe-6bd635cbae49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412735(v=OCS.15)
ms:contentKeyID: 49301495
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Delegare le autorizzazioni di installazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Se non si desidera concedere l'appartenenza al gruppo Domain Admins agli utenti o ai gruppi che distribuiscono Lync Server 2013, è possibile consentire ai membri del gruppo RTCUniversalServerAdmins di eseguire il cmdlet **Enable-CsTopology** di Windows PowerShell nei server che eseguono Lync Server 2013. Per impostazione predefinita, i membri del gruppo RTCUniversalServerAdmins non sono abilitati per l'esecuzione di questo cmdlet. Per concedere i diritti di amministratore e le autorizzazioni per l'esecuzione di **Enable-CsTopology** nei server che eseguono Lync Server, utilizzare il cmdlet **Grant-CsSetupPermission** e specificare un'unità organizzativa in cui si trovano gli oggetti computer del server in cui è in esecuzione Lync Server 2013.

Con la preparazione del dominio che avviene quando si installa Lync Server, non vengono aggiunte automaticamente le autorizzazioni che consentono ai membri del gruppo RTCUniversalServerAdmins di eseguire il cmdlet Enable-CsTopology. Per questo motivo, per impostazione predefinita è necessario essere amministratori del dominio per abilitare una topologia. Per concedere ai membri del gruppo RTCUniversalServerAdmins il diritto di abilitare una topologia, è necessario eseguire il cmdlet Grant-CsSetupPermissions. Sarà inoltre necessario eseguire questo cmdlet per ogni contenitore di Active Directory che include computer in cui è in esecuzione Lync Server.

Questo cmdlet concede esclusivamente le autorizzazioni al gruppo RTCUniversalServerAdmins; non può essere utilizzato per concedere le autorizzazioni ad altri gruppi di sicurezza o a singoli utenti.


> [!NOTE]
> <STRONG>Enable-CsTopology</STRONG> è il cmdlet principale per consentire ai membri del gruppo RTCUniversalServerAdmins di impostare e distribuire Lync Server 2013.



## Per aggiungere la possibilità di eseguire Enable-CsTopology al gruppo RTCUniversalServerAdmins

1.  Accedere a un server come membro del gruppo Domain Admins per il dominio in cui l'utente delegato eseguirà **Enable-CsTopology**.

2.  Aprire Lync Server 2013 Management Shell. Lync Server 2013 Management Shell viene installato automaticamente in ogni Front End Server o in ogni computer in cui sono stati installati gli strumenti di amministrazione di Lync Server 2013. Per informazioni dettagliate su Lync Server 2013 Management Shell, vedere [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md) nella documentazione relativa alle operazioni.

3.  Eseguire il cmdlet seguente da Lync Server 2013 Management Shell:
    
        Grant-CsSetupPermission -ComputerOU <DN of the OU> -Domain <Domain FQDN>
    

    > [!NOTE]
    > Se l'unità organizzativa non è di primo livello, è necessario specificare il nome di dominio completo.

    
    Nell'esempio seguente l'unità organizzativa (OU) è Lync Servers, che si trova nel dominio contoso.com.
    
        Grant-CsSetupPermission -ComputerOU "OU=Lync Servers" -Domain contoso.com

