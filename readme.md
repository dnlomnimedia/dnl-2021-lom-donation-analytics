# Luminate Online Donation Tracking GTM code

This is the sample code to help your organization integrate the GTM analytics code into Luminate Online donation forms. 

This code is configured in accordance with best practices that DNL Omnimedia developed. Namely, the code structure puts wrapper head & body contents into PageBuilder reusable pages. The analytics code is also placed into PageBuilder reusable pages for ease of management and reuse in multiple wrappers.

Feel free to adapt this code to your needs. DNL Omnimedia, Inc. does not provide any guarantees with this code. 

## How to Configure Your Site
1. Clone this repository
2. Update `reus_analytics_head` & `reus_analytics_body` files to include the id of your GTM container
3. Create the PageBuilder pages `reus_analytics_head` & `reus_analytics_body`  in Luminate online.
4. Place the updated content into PageBuilder pages
5. Update your wrapper code (here it lives in files that start with `reus_wrpr_`) to include the reusable PageBuilder pages `reus_analytics_head` & `reus_analytics_body`
6. Configure your GTM container to forward errors into Google Analytics on `error` event
7. Configure your GTM to forward transactions to Google Analytics on `transactionComplete` event; [ensure that transaction is recorded only once](https://www.simoahava.com/gtm-tips/prevent-repeat-transactions/)
8. Configure GTM to forward `userId` data, if desired
9. [Configure Google Analytics to use new `userId`](https://www.optimizesmart.com/google-analytics-user-id-explained/), if desired
10. Configure `userId` as a custom dimension in Google Analytics and configure GTM to send data to that custom dimension for more detailed reporting and data reconciliation with Luminate Online

## How to Get Help
If you run into issues with this code or need assistance implementing analytics in other Blackbaud Luminate Online module. [Contact DNL Omnimedia](https://www.dnlomnimedia.com/contact/?utm_source=github&utm_medium=web&utm_campaign=bbdevconference)