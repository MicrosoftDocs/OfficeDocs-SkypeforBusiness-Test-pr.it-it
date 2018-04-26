---
title: Verificare che tutti gli oggetti contatto della messaggistica unificata di Exchange siano stati rimossi dal pool legacy
TOCTitle: Verificare che tutti gli oggetti contatto della messaggistica unificata di Exchange siano stati rimossi dal pool legacy
ms:assetid: 5a813169-0ed7-4f84-a242-ed2cd4ea5c43
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688068(v=OCS.15)
ms:contentKeyID: 49887576
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare che tutti gli oggetti contatto della messaggistica unificata di Exchange siano stati rimossi dal pool legacy

 

_**Ultima modifica dell'argomento:** 2012-09-26_

Utilizzare lo strumento **OCSUmUtil** o il cmdlet **Get-CsExumContact** per verificare che gli oggetti contatto di messaggistica unificata di Exchange siano stati rimossi dal pool Office Communications Server 2007 R2 legacy. **OCSUmUtil** è contenuto nella cartella seguente:

%Program Files%\\Common Files\\ Lync Server 2013\\Support\\OcsUMUtil.exe

Lo strumento **OCSUmUtil** deve essere eseguito da un account utente:

  - Membro del gruppo RTCUniversalServerAdmins e del gruppo RTCUniversalUserAdmins (include i diritti di lettura delle impostazioni di messaggistica unificata di Exchange Server)

  - Con diritti a livello di dominio per creare oggetti contatto nel contenitore di unità organizzative specificato

Per informazioni dettagliate sull'utilizzo del cmdlet **Get-CsExumContact**, vedere [Get-CsExUmContact](get-csexumcontact.md) nella documentazione relativa a Lync Server Management Shell.

