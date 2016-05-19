---
Description: The Payout summary shows you details about the money you’ve earned with your apps and in-app products. It also lets you know when you’ll receive payments and how much you'll be paid.
title: Payout summary
ms.assetid: F0D070BE-8267-4CC9-B0D2-085EBA74AC98
---

# Payout summary


The **Payout summary** shows you details about the money you’ve earned with your apps and in-app products. It also lets you know when you’ll receive payments and how much you'll be paid.

If you use Microsoft Advertising to earn money, and your [pubCenter and Dev Center accounts are linked](pubcenter-dev-center-integration.md), you'll also see payment info for advertising proceeds in the **Payout summary**. For more details regarding Advertising Payment policies, see the [pubCenter Payment policies](http://go.microsoft.com/fwlink/p/?LinkID=624469).

If you sell products in the Azure Marketplace, you’ll also see info on successful payouts from November 1, 2015 and forward in the **Payout summary**. For more details regarding Azure Marketplace payment, see the [Microsoft Azure Marketplace Participation Policies](http://go.microsoft.com/fwlink/p/?LinkId=722436) and the [Microsoft Azure Marketplace Publisher Agreement](http://go.microsoft.com/fwlink/p/?LinkID=699560 ). More info about viewing earlier Azure Marketplace payout info can be found [here](http://go.microsoft.com/fwlink/p/?LinkID=722439).

**Note**  
To be eligible for payout, your app proceeds must reach the applicable payment threshold. If the proceeds are less than the payment threshold, they will remain in the Reserved category until the threshold has been met. For more details, see the [App Developer Agreement](https://msdn.microsoft.com/library/windows/apps/hh694058).

 

## Current proceeds and payments


Near the top of the page, you’ll find your **Current proceeds and payments**, which contains three sections: **Reserved**, **Upcoming payment**, and **Most recent payment**.

-   **Reserved** shows the amount of money your account has accumulated but which has not yet been scheduled for payment, including advertising proceeds. (Azure Marketplace proceeds do not appear in the Reserved section; if you only participate in the Azure Marketplace, you will see $0.00 here.) Proceeds from your most recent advertising and app sales remain on hold for about 30 days before they become eligible for payout. After that, the proceeds will be scheduled for payment the following month (assuming the payment threshold has been met). When a payment is attempted, your reserved balance will decrease by the payment amount and you will see the amount reflected in **Upcoming payment**. Note that the amount shown in **Reserved** is an estimate, because exchange rates for sales in other currencies may fluctuate prior to payment creation. You may notice your reserved balance change slightly at the beginning of every month. Your reserved balance is updated monthly to reflect monthly exchange rates, so that it represents a more accurate estimate. You can click **View details** to see additional information, or click the link to **Download your reserved transactions** to view a .csv file of all your **Reserved** transactions.
-   **Upcoming payment** shows the number of upcoming payments, the amount of your next payment(s), and the payment creation date(s). If your eligible proceeds haven’t met the payment threshold yet, no upcoming payment will be shown here. You can click **View details** to see additional information, including the payment amount(s) and their respective revenue source.
-   **Most recent payment** shows the amount of the last payment attempted. If the payment was successful, the **View details** link will be blue, and you can click it to see the details for each payment. Note that if we attempted to make multiple payments and only one of them was successful, only the amount of the successful payment will be shown here. If one or more payments failed, the **View details** link will be red and the number of failed payments will be displayed. You can click **View details** to see more details about the problem so that you can remedy the situation.

## Proceeds by app and adjustments


This section breaks down the summary info to let you see specifics by app. If you earned money through Microsoft Advertising, the total amount of your advertising proceeds is shown here as a single line item.

By reviewing this section, you can determine which apps have earned money that’s currently in the **Reserved** or **Most recent payment** category. You can also see the total amount you’ve received for each app. If it was necessary to make any [adjustments](#adjust) to your account balance, you can view them here too. (Note that adjustments for Microsoft Advertising proceeds are not currently shown here.)

## Payment statements


In this section you can view statements for all successful monthly payments and see the total amount of money you've been paid.

The **Total paid to date** section shows the total amount you've been paid for all your sales. Click **View details** to see the amounts that came from each revenue source.

Below the **Total paid to date** section, you will see your last three statements by default. To see the full statement (for successful payments), click **View**. You can access your historical payment statements through the drop-down box.

At the top of each statement, you’ll see the total amount of your monthly payment. Immediately below, in **Payments issued**, you’ll see a summary of how your payment amount was calculated.

Underneath, in the **Proceeds breakdown** section, you can view details on how much money was made per market and per revenue source (such as Windows Phone Store, Windows Store 8, Windows Store, etc.) by app. You’ll also see details on any [adjustments](#adjust) that were made, including the date, amount, and reason for the adjustment.

Note that the sections mentioned above only show info on your proceeds (and adjustments) from app sales; if you earned money through advertising, you’ll see a separate Microsoft Advertising section with details about the payouts and currency conversions.

## Adjustments


| Adjustment category     | Description                                                                                                |
|-------------------------|------------------------------------------------------------------------------------------------------------|
| Compensatory adjustment | Any adjustment made to your payout balance that does not pertain to the other adjustment categories listed |
| Historic balance        | Payout balances from a historic payment system                                                             |
| Passin tax              | Tax adjustment related to sales in Korea                                                                   |

 

## Downloading payment transactions


At the top of each statement, you’ll see a link to **Download transactions**. Click this link to get a .csv file with detailed info about each of the transactions included in your payment.

The following table describes the fields that appear in the .csv file. Note that the exact fields you see may vary as we continue to update our reporting.

| Field name              | Description                                                                                                                              |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Revenue Source          | The source of your revenue, based on where the transaction occurred (such as Windows Phone Store, Windows Store 8, Windows Store, etc.)  |
| Transaction ID          | Unique transaction identifier                                                                                                            |
| Transaction Date Time   | The date and time the transaction occurred (UTC)                                                                                         |
| Parent Product ID       | Unique parent product identifier. Please note: if there isn’t a parent product for the transaction, then Parent Product ID = Product ID. |
| Product ID              | Unique product identifier                                                                                                                |
| Parent Product Name     | Name of the parent product. Please note: if there isn’t a parent product for the transaction, then Parent Product Name = Product Name.   |
| Product Name            | Name of the product                                                                                                                      |
| Product Type            | Type of product (such as App, In-App, Game, etc.)                                                                                        |
| Transaction Type        | Type of transaction (such as purchase, refund, reversal, chargeback, etc.)                                                               |
| Payment Method          | Customer payment instrument used for the transaction (such as credit card, mobile operator, etc,)                                        |
| Country / Region        | Country/region where the transaction occurred                                                                                            |
| Local Provider / Seller | Local provider/seller of record                                                                                                          |
| Transaction Currency    | Currency of the transaction                                                                                                              |
| Transaction Amount      | Amount of the transaction                                                                                                                |
| Tax Remitted            | Amount of tax remitted (sales, use, or VAT/GST taxes)                                                                                    |
| Net Receipts            | Transaction amount less tax remitted                                                                                                     |
| Store Fee               | The percentage of Net Receipts retained by Microsoft as a fee for making the app or in-app product available in the Store                |
| App Proceeds            | Net receipts minus the Store Fee                                                                                                         |
| Taxes Withheld          | Amount of income tax withheld                                                                                                            |
| Payment                 | App Proceeds less any applicable income tax withholding (amount shown in Transaction Currency)                                           |
| FX Rate                 | Foreign exchange rate used to convert Transaction Currency to Payment Currency                                                           |
| Payment Currency        | Currency your payment is made in                                                                                                         |
| Converted Payment       | Payment amount converted to Payment Currency using the FX Rate                                                                           |
| Tax Remit Model         | Party responsible for remitting taxes (sales, use, or VAT/GST taxes)                                                                     |
| Charges                 | Shows a breakdown of all the charge details aggregated in the Transaction Amount column. (Only included for Azure Marketplace.)          |

 

 

 






<!--HONumber=Mar16_HO2-->

