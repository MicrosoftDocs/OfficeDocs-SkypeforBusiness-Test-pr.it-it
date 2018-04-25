---
title: Rimuovere una voce host autorizzata
TOCTitle: Rimuovere una voce host autorizzata
ms:assetid: 56a04140-347e-4eef-bede-0e858534f71e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204902(v=OCS.15)
ms:contentKeyID: 49300583
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere una voce host autorizzata

 

_**Ultima modifica dell'argomento:** 2012-09-26_

In questo argomento viene descritto come rimuovere una voce host autorizzato legacy, nota come *voce applicazione attendibile* in Lync Server 2013. È necessario rimuovere le voci host autorizzato esistenti per tutti i gateway SIP/CSTA nella distribuzione di Office Communications Server 2007 R2 quando si esegue la migrazione del controllo delle chiamate remote in una distribuzione di Lync Server 2013. Per rimuovere le voci host autorizzato esistenti, è necessario usare gli strumenti di amministrazione inclusi in Office Communications Server 2007 R2.

## Per rimuovere una voce host autorizzato in una distribuzione di Office Communications Server 2007 R2

1.  Aprire la console di amministrazione di Office Communications Server 2007 R2.

2.  Espandere l'albero e fare clic con il pulsante destro del mouse sul pool in cui è stato creato l'host autorizzato.

3.  Scegliere **Proprietà** e quindi fare clic su **Proprietà Front End** .

4.  Fare clic sulla scheda **Autorizzazione host** .

5.  Selezionare un server e quindi fare clic su **Rimuovi** .

6.  In **Proprietà** fare clic su **OK** .

