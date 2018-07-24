---
title: 'Lync Server 2013: Modificare o configurare URL semplici'
TOCTitle: Modificare o configurare URL semplici
ms:assetid: 0008aeea-4ae9-4e36-83cd-ef7ff7b6e128
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398063(v=OCS.15)
ms:contentKeyID: 49299474
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare o configurare URL semplici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-04_

Per eseguire questa procedura non è richiesta l'appartenenza a un gruppo di amministratori locale o a un gruppo di dominio con privilegi. È consigliabile eseguire l'accesso a un computer come utenti standard.

Lync Server 2013 usa URL semplici per indirizzare le chiamate interne ed esterne ai servizi nel Front End Server o nel server Server Director, se ne è stato distribuito uno. Per ulteriori informazioni sugli URL semplici, vedere [Pianificazione degli URL semplici in Lync Server 2013](lync-server-2013-planning-for-simple-urls.md) nella documentazione relativa alla pianificazione. È possibile selezionare il formato degli URL semplici scegliendo tra le diverse opzioni disponibili. Per informazioni dettagliate su queste opzioni, vedere [Requisiti DNS per gli URL semplici in Lync Server 2013](lync-server-2013-dns-requirements-for-simple-urls.md) nella documentazione relativa alla pianificazione.

Per impostazione predefinita, gli URL semplici saranno configurati (ad esempio, per l'accesso esterno) nel formato seguente: https://dialin.\<SIP Domain\>

## Per configurare gli URL semplici

1.  In Generatore di topologie fare clic con il pulsante destro del mouse sul nodo **Lync Server** e quindi scegliere **Modifica proprietà**.

2.  Nel riquadro **URL semplici** selezionare gli **URL di accesso a telefono** (accesso esterno, dialin) o gli **URL riunione** (meet) da modificare e quindi fare clic su **Modifica URL**.

3.  Aggiornare l'URL in base al valore desiderato e quindi fare clic su **OK** per salvare l'URL modificato. Nell'esempio l'URL di accesso a telefono è stato modificato in https://pool01.contoso.net/dialin.

4.  Se necessario, modificare l'URL riunione eseguendo la stessa procedura.

## Per definire l'URL semplice facoltativo per l'accesso amministrativo

1.  In Generatore di topologie fare clic con il pulsante destro del mouse sul nodo **Lync Server** e quindi scegliere **Modifica proprietà**.

2.  Nella casella **URL di accesso amministrativo** immettere l'URL semplice che si desidera utilizzare per l'accesso amministrativo al Pannello di controllo di Lync Server 2013 e quindi fare clic su **OK** .
    
    > [!tip]  
    > È consigliabile utilizzare l'URL più semplice possibile per l'accesso amministrativo. L'opzione più semplice è <strong>https://admin.</strong> <em>&lt;domain&gt;</em> .    
    > [!important]  
    > Se si modifica un URL semplice dopo la distribuzione iniziale, è necessario considerare quali modifiche influiscono sui record DNS (Domain Name System) e sui certificati per gli URL semplici. Se la modifica influisce sulla base di un URL semplice, sarà necessario modificare anche i record DNS e i certificati. Ad esempio, la modifica da https://lync.contoso.com/Meet a https://meet.contoso.com comporta la modifica dell'URL di base da lync.contoso.com a meet.contoso.com, pertanto sarà necessario modificare i record DNS e i certificati in modo che facciano riferimento a meet.contoso.com. Se l'URL semplice è stato modificato da https://lync.contoso.com/Meet a https://lync.contoso.com/Meetings, l'URL di base lync.contoso.com resterà invariato, pertanto non sarà necessario apportare modifiche ai record DNS o ai certificati. Ogni volta che si modifica il nome di un URL semplice, sarà tuttavia necessario eseguire il cmdlet <strong>Enable-CsComputer</strong> su ogni server Server Director e Front End Server per registrare la modifica.

## Vedere anche

#### Concetti

[Pianificazione degli URL semplici in Lync Server 2013](lync-server-2013-planning-for-simple-urls.md)

