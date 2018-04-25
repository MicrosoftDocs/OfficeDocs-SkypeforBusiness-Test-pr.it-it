---
title: Aggiornamento dell'elenco dei componenti aggiuntivi di Outlook abilitati
TOCTitle: Aggiornamento dell'elenco dei componenti aggiuntivi di Outlook abilitati
ms:assetid: 5db120dc-52f9-4dde-acb9-3824ae245086
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215438(v=OCS.15)
ms:contentKeyID: 49300706
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiornamento dell'elenco dei componenti aggiuntivi di Outlook abilitati

 

_**Ultima modifica dell'argomento:** 2013-01-07_

È possibile assicurarsi che componente aggiuntivo per riunioni online per Microsoft Lync 2013 rimanga sempre abilitato per gli utenti tramite la creazione di criteri per includerlo nell'elenco di gestione dei componenti aggiuntivi per Outlook. I criteri per l'elenco di gestione dei componenti aggiuntivi sono inclusi nei file dei modelli amministrativi di Office per la console di gestione di Criteri di gruppo. Viene creata una chiave del Registro di sistema in HKCU\\Software\\Policies\\Microsoft\\Office\\15.0\\Outlook15\\Resiliency\\AddinList. È possibile aggiungere un valore per ucaddin.dll a questa chiave e configurare il valore di ucaddin.dll in modo che sia sempre abilitato e non possa essere disabilitato manualmente dagli utenti.

## Per aggiungere ucaddin.dll all'elenco dei componenti aggiuntivi di Outlook

  - Per aggiungere la chiave del Registro di sistema AddinList, disponibile in HKCU\\Software\\Policies\\Microsoft\\Office\\15.0\\Outlook15\\Resiliency\\AddinList, aggiungere il valore seguente:
    
      - Tipo di valore del Registro di sistema = REG\_SZ
    
      - Nome = ucaddin.dll
    
      - Valore = 1 (specifica che il componente aggiuntivo è sempre abilitato e non può essere gestito dall'utente finale)

