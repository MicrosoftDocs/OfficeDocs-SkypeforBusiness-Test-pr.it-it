---
title: Configurare le aree di rete per il servizio Controllo di ammissione di chiamata
TOCTitle: Configurare le aree di rete per il servizio Controllo di ammissione di chiamata
ms:assetid: ea3ff988-dd5a-4bc4-bec5-39a0fb09793a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399051(v=OCS.15)
ms:contentKeyID: 49302366
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le aree di rete per il servizio Controllo di ammissione di chiamata

 

_**Ultima modifica dell'argomento:** 2012-09-21_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se sono state già create aree di rete per il servizio di emergenza (E9-1-1) o per il bypass multimediale, è possibile modificare le aree di rete esistenti aggiungendo impostazioni specifiche del servizio Controllo di ammissione di chiamata utilizzando il cmdlet <strong>Set-CsNetworkRegion</strong>. Per un esempio della modifica di un'area di rete, vedere <a href="lync-server-2013-create-or-modify-a-network-region.md">Creare o modificare un'area di rete in Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


Le *aree di rete* sono hub o backbone di rete che si utilizzano nella configurazione del servizio Controllo di ammissione di chiamata, nel servizio di emergenza (E9-1-1) e nel bypass multimediale. Eseguire la procedura seguente per creare aree di rete allineate a quelle dell'esempio di topologia di rete per il servizio Controllo di ammissione di chiamata. Per visualizzare l'esempio di topologia di rete, vedere [Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md) nella documentazione relativa alla pianificazione.

L'esempio di topologia di rete per il servizio Controllo di ammissione di chiamata include tre aree: Nord America, EMEA e APAC. Per ogni area è specificato un sito centrale. Per il Nord America, il sito centrale designato è denominato CHICAGO. Nella procedura seguente è illustrato un esempio di come utilizzare il cmdlet **New-CsNetworkRegion** per creare l'area del Nord America.


> [!NOTE]
> Nella procedura seguente si utilizza Lync Server Management Shell per creare un'area di rete. Per informazioni dettagliate sul'utilizzo di Pannello di controllo di Lync Server per la creazione di un'area di rete, vedere <A href="lync-server-2013-create-or-modify-a-network-region.md">Creare o modificare un'area di rete in Lync Server 2013</A>.



## Per creare un'area di reste per il servizio Controllo di ammissione di chiamata

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet **New-CsNetworkRegion** per ogni area che è necessario creare. Ad esempio, per creare l'area del Nord America, eseguire:
    
        New-CsNetworkRegion -Identity NorthAmerica -CentralSite CHICAGO -Description "All North America Locations"

3.  Ripetere il passaggio 2 per creare le aree di rete di EMEA e APAC.

