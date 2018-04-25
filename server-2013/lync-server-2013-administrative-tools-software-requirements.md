---
title: 'Lync Server 2013: Requisiti software degli strumenti di amministrazione'
TOCTitle: Requisiti software degli strumenti di amministrazione
ms:assetid: 2fb172c3-7b84-4e49-981c-2a17e7a00a29
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg195653(v=OCS.15)
ms:contentKeyID: 49300068
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti software degli strumenti di amministrazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

In questo argomento viene descritto il software necessario per installare e usare gli strumenti di amministrazione di Lync Server 2013 oltre ai requisiti del sistema operativo.

## Microsoft .NET Framework 4.5

È richiesta l'edizione a 64 bit di Microsoft .NET Framework 4.5 per Lync Server 2013.

## Windows PowerShell 3.0

È richiesto Windows PowerShell 3.0 per l'esecuzione dei componenti di Microsoft Lync Server 2013. Per ulteriori informazioni, vedere [Installazione di Windows PowerShell 3.0 per Lync Server 2013](lync-server-2013-installing-windows-powershell-3-0.md).

## Windows Installer versione 4.5

In Lync Server 2013 viene utilizzata la tecnologia Windows Installer per installare, disinstallare e gestire diversi ruoli server. Windows Installer versione 4.5 è disponibile come componente ridistribuibile per il sistema operativo Windows Server. Windows Installer 4.5 viene fornito con Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, ciò significa che non è necessario scaricare l'utilità per qualsiasi computer che esegue Lync Server 2013 ( Lync Server 2013 può essere installato solo nei computer che eseguono Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2).

Tuttavia, se si desidera installare il Generatore di topologie di Lync Server Management Shell o Lync Server in una workstation di amministrazione, potrebbe essere necessario scaricare Windows Installer 4.5. Questa utilità viene fornita con Windows 7 e Windows 2008 R2, ma non con altre versioni precedenti del sistema operativo Windows. È possibile scaricare Windows Installer 4.5 dall'Area download Microsoft all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=197395>.

## Plug-in del browser Microsoft Silverlight 5

Pannello di controllo di Lync Server 2013 è uno strumento basato sul Web che richiede l'installazione dell'ultima versione del plug-in del browser Microsoft Silverlight 5. Se all'avvio del Pannello di controllo di Lync Server 2013 questo software non è installato o è installata una versione precedente, Pannello di controllo di Lync Server 2013 richiede di installare la versione necessaria.

## Vedere anche

#### Concetti

[Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md)  

#### Ulteriori risorse

[Requisiti dell'infrastruttura degli Strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-infrastructure-requirements.md)  
[Autorizzazioni e diritti di amministratore necessari per l'installazione e l'amministrazione di Lync Server 2013](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)

