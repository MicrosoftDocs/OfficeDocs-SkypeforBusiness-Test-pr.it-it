---
title: Eliminare un oggetto contatto di un telefono di area comune
TOCTitle: Eliminare un oggetto contatto di un telefono di area comune
ms:assetid: f4c139dc-f07c-4c75-9345-e291aea41173
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994087(v=OCS.15)
ms:contentKeyID: 52062478
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un oggetto contatto di un telefono di area comune

 

_**Ultima modifica dell'argomento:** 2013-02-20_

È possibile che si desideri eliminare l'oggetto contatto associato a un telefono di area comune. Ad esempio, se si rimuove il telefono dalla sala ritrovo del personale, non sarà necessario un oggetto contatto associato al telefono. Il cmdlet **Remove-CsCommonAreaPhone** consente di eliminare gli account relativi ai telefoni di area comune. Quando si esegue questo cmdlet, il telefono viene eliminato dall'elenco dei telefoni delle aree comuni restituito da **Get-CsCommonAreaPhone**. L'oggetto contatto associato al telefono verrà inoltre eliminato da Servizi di dominio Active Directory.

Utilizzare **Remove-CsCommonAreaPhone** per rimuovere un telefono di area comune o tutti i telefoni di area comune che hanno un elemento in comune, ad esempio un nome visualizzato o un indicativo di località. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).


## Rimozione di un telefono di area comune specifico

  - Il comando seguente consente di rimuovere il telefono di area comune con indirizzo SIP sip:mainlobby@litwareinc.com:
    
        Remove-CsCommonAreaPhone -Identity "sip:mainlobby@litwareinc.com"

## Rimozione di telefoni di area comune in base al nome visualizzato

  - Questo comando consente di rimuovere tutti i telefoni di area comune il cui nome visualizzato include il valore di stringa "Building 14":
    
        Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -match "Building 14"} | Remove-CsCommonAreaPhone

## Rimozione di telefoni di area comune in base al codice paese e all'indicativo di località

  - Questo comando consente di rimuovere tutti i telefoni di area comune per gli Stati Uniti (codice paese 1) e con indicativo di località 425:
    
        Get-CsCommonAreaPhone | Where-Object {$_.LineUri  -match "^tel:\+1425"} | Remove-CsCommonAreaPhone

Per informazioni dettagliate, vedere l'argomento della guida relativo al cmdlet [Remove-CsCommonAreaPhone](remove-cscommonareaphone.md).

## Vedere anche

#### Ulteriori risorse

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)

