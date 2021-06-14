# Luminate Online Donation Tracking GTM code

This is the sample code to help your organization integrate the GTM analytics code into Luminate Online donation forms. 

This code is configured in accordance with best practices that DNL Omnimedia developed. Namely, the code structure puts wrapper head & body contents into PageBuilder reusable pages. The analytics code is also placed into PageBuilder reusable pages for ease of management and reuse in multiple wrappers.

Feel free to adapt this code to your needs. DNL Omnimedia, Inc. does not provide any guarantees with this code. 

## How to Configure Your Site

1. Clone this repository
2. Update `reus_analytics_head` & `reus_analytics_body` files to include the id of your GTM container
3. Create the PageBuilder pages `reus_analytics_head` & `reus_analytics_body`  in Luminate online
4. Place the updated content into PageBuilder pages created in the previous step
5. Update your wrapper code (here it lives in files that start with `reus_wrpr_`) to include the reusable PageBuilder pages `reus_analytics_head` & `reus_analytics_body` in appropriate sections
6. Configure your GTM container to forward errors into Google Analytics on `error` event
7. Configure your GTM to forward transactions to Google Analytics on `transactionComplete` event; [ensure that transaction is recorded only once](https://www.simoahava.com/gtm-tips/prevent-repeat-transactions/)
8. Configure GTM to forward `userId` data to Google Analytics, if desired
9. [Configure Google Analytics to use new `userId`](https://www.optimizesmart.com/google-analytics-user-id-explained/), if desired
10. Configure `userId` as a custom dimension in Google Analytics and configure GTM to send data to that custom dimension for more detailed reporting and data reconciliation with Luminate Online

## How to Configure Error Tracking in GTM

* Enable built-in `Error Message` variable
* Create a new data layer variable `numberOfErrors` that will pull in data layer value `numberOfErrors`
* Create a new GTM trigger to fire when a _Custom Event_ `error` is detected
* Create a new GTM tag to track _Event_ in Google Analytics
* Configure event _Label_ to pull in `{{Error Message}}`
* Configure event _Value_ to pull in `{{numberOfErrors}}`

## How to Configure Transaction Tracking in GTM

[Follow this guide to configure the unique transaction tracking](https://www.simoahava.com/gtm-tips/prevent-repeat-transactions/). Note that the article was written with assumption that the data layer uses the deprecated e-commerce object. To properly work with this code the data layer variables will have to be configured to get data from the [enhanced e-commerce data layer structure](https://developers.google.com/tag-manager/enhanced-ecommerce).

## How to Get Help

If you run into issues with this code or need assistance implementing analytics in other Blackbaud Luminate Online module. [Contact DNL Omnimedia](https://www.dnlomnimedia.com/contact/?utm_source=github&utm_medium=web&utm_campaign=bbdevconference).
