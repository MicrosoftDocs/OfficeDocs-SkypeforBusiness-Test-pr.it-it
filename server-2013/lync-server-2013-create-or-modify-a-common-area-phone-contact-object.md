---
title: Creare o modificare un oggetto contatto di un telefono di area comune
TOCTitle: Creare o modificare un oggetto contatto di un telefono di area comune
ms:assetid: eec33ad1-e4f2-49b2-91d6-d5a9d2e1714b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994083(v=OCS.15)
ms:contentKeyID: 52062469
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un oggetto contatto di un telefono di area comune

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Per creare oggetti contatto di Servizi di dominio Active Directory per tutti i telefoni di area comune, usare il cmdlet **New-CsCommonAreaPhone**. Questo cmdlet può creare nuovi oggetti contatto da usare con i telefoni di area comune oppure può associare oggetti contatto esistenti con un nuovo telefono di area comune. Per modificare le proprietà degli oggetti contatto associati ai telefoni di area comune, usare il cmdlet **Set-CsCommonAreaPhone**. I parametri facoltativi per **Set-CsCommonAreaPhone** consentono di modificare gli elementi, ad esempio il nome visualizzato del contatto di Active Directory o l'URI (Uniform Resource Identifier) associato al telefono, e abilitare e disabilitare l'account per l'utilizzo con Lync Server. Per informazioni dettagliate su tutte le modifiche disponibili, vedere la sezione Parametri all'indirizzo [Set-CsCommonAreaPhone](set-cscommonareaphone.md). Per informazioni dettagliate sui parametri **New-CsCommonAreaPhone**, vedere [New-CsCommonAreaPhone](new-cscommonareaphone.md).

È possibile eseguire questi due cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).


## Creazione di un oggetto contatto di un telefono di area comune

  - Per creare un nuovo oggetto contatto di un telefono di area comune, utilizzare il cmdlet **New-CsCommonAreaPhone**. Quando si crea un oggetto contatto, è necessario specificare almeno le informazioni seguenti:
    
      - **LineUri**: numero di telefono assegnato al telefono di area comune. Si noti che è necessario utilizzare il formato E.164 quando si specifica il numero di telefono.
    
      - **RegistrarPool**: nome di dominio completo (FQDN) del pool di registrazione che ospiterà l'oggetto contatto.
    
      - **OU**: nome distinto del contenitore di Active Directory in cui verrà creato l'oggetto contatto.
    
    È inoltre consigliabile specificare un nome visualizzato di Servizi di dominio Active Directory. In caso contrario, sarà necessario utilizzare un GUID per specificare l'identità telefono. Ad esempio:
    
        New-CsCommonAreaPhone -LineUri "tel:+12065551219" -RegistrarPool "atl-cs-001.litwareinc.com" -OU "OU=Phones,dc=litwareinc,dc=com" -DisplayName "Lobby"

## Modifica di un oggetto contatto di un telefono di area comune

  - Per modificare le proprietà di un oggetto contatto di un telefono di area comune, utilizzare il cmdlet **Set-CsCommonAreaPhone**. Ad esempio, questo comando configura l'indirizzo SIP per il telefono di area comune con DisplayName "Lobby":
    
        Set-CsCommonAreaPhone -Identity "Lobby" -SipAddress "sip:lobby@litwareinc.com"

Per informazioni dettagliate, vedere gli argomenti della Guida per i cmdlet [New-CsCommonAreaPhone](new-cscommonareaphone.md) e [Set-CsCommonAreaPhone](set-cscommonareaphone.md).

