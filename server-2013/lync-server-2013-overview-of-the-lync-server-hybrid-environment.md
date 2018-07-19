---
title: "Lync Server 2013: Panoramica dell'ambiente ibrido di Lync Server"
TOCTitle: Panoramica dell'ambiente ibrido di Lync Server 2013
ms:assetid: 0d16ec3a-28f0-4483-96e7-8e68f30398fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204669(v=OCS.15)
ms:contentKeyID: 49299669
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dell'ambiente ibrido di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-28_

Per ambiente ibrido di Lync Server 2013 si intende una distribuzione in cui sono presenti utenti ospitati in Lync Server 2013 locale e altri in Lync Online, ma tali utenti condividono lo stesso dominio, ad esempio user@contoso.com.

## Informazioni sulla Guida

In questa Guida vengono descritte le attività necessarie per configurare l'ambiente di Lync Server 2013 per l'interoperabilità con Lync Online e quindi spostare gli utenti dalla distribuzione locale per utilizzare Lync Online.

## Prerequisiti

Per completare le attività per la configurazione di una distribuzione ibrida, è necessario installare le seguenti applicazioni e utilità. I programmi di installazione di questi file sono inclusi nei supporti di installazione forniti per la distribuzione e nei collegamenti inclusi nell'elenco seguente.

  - [Active Directory Federation Services (ADFS) 2.0](http://go.microsoft.com/fwlink/p/?linkid=257305)

  - [Strumento di sincronizzazione della directory Microsoft 9.1](http://go.microsoft.com/fwlink/p/?linkid=257307)

  - [Installazione di Windows PowerShell per l'acceso Single Sign-On con ADFS](http://go.microsoft.com/fwlink/p/?linkid=398710)

  - L'Assistente per l'accesso ai Microsoft Online Services (msoidcli-7.0.msi) è incluso con il programma di installazione del desktop per Office 365, che può essere scaricato dalla pagina Download a cui si accede tramite un collegamento nel portale di amministrazione di Office 365.

## Credenziali di amministratore

Quando viene richiesto di immettere le credenziali di amministratore, utilizzare il nome utente e la password forniti dell'account amministratore del tenant di Office 365. Le credenziali verranno inoltre utilizzate per configurare Active Directory Federation Services (AD FS) 2.0, la sincronizzazione della directory, l'accesso Single Sign-On, la federazione e lo spostamento utenti in Lync Online.

## Connessione a Lync Online PowerShell

Gli amministratori ora hanno la possibilità di usare Windows PowerShell per gestire Lync Online e gli account utente di Lync Online. A questo scopo è necessario scaricare e installare per prima cosa il modulo del connettore di Lync Online dall'Area download Microsoft (http://go.microsoft.com/fwlink/?LinkId=294688). Per altre informazioni su download, installazione e uso del modulo del connettore di Lync Online e per informazioni dettagliate sull'uso di Windows PowerShell per gestire Lync Online, vedere [Uso di Windows PowerShell per gestire Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell).

