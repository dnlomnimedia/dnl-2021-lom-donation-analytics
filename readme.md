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
1. Log into Google Tag Manager
2. Create an account for your site
3. Create a few User-Defined variables which will be reused for all future tags created as to eliminate retyping values:  
  1a. Go to the Variables menu tab and click on 'new' under User-Defined Variables and name it `gaSettings`  
  1b. Select the variable type _Google Analytics Settings_  
  1c. Then enter the Tracking ID for your site that was supplied to you by Google Analtyics when you created that site account in Google Analytics. This can be found in that site's account in the Admin gear icon tab under the Property column in the Property Settings tab.  
  1d. Leave _Cookie Domain_ as `auto` and click on _More Settings_ > _Ecommerce_ > _Enable Enhanced Ecommerce Features_ > _Use Data Layer_  
  1e. If your site uses a donation form supplied by a different domain or your site redirects to another page click on the _Cross Domain Tracking_ tab and enter in the domains seperated by a comma that are used in your sites process in the _Auto Link Domains_ text box  
  1f. Save this variable  
  1g. _Add Field_ in _Fields to Set_ section. For the Field Name enter `allowLinker` and set value to `true`; this will enable cross domain linking  
  2a. Create another variable and name it `gaProperty` and select the variable type as _Constant_ and for the value enter the Google Analytics Tracking ID for your site  
  3a. Create another variable and name it `gaCrossDomains` and select the variabel type as Constant and for the value enter in any domains you want to track same as we did when creating the first variable and separate the domains by a comma. 
4. Go to the Triggers tab and create two triggers, one for donation completion and another one for an error:
 1a. Create a new trigger and name it `Transaction complete`.
 1b. Select _Custom Event_ for the trigger type.
 1c. For the event name enter `transactionComplete`.
 1d. Select this trigger to fire on 'some custom events', and from the selects select the options to make this trigger fire when: `isTransactionInInTheCookie` does not equal `true`.
5. Go to the Tag menu tab and create three tags page view, donation complete, donation error:
 1a. The first tag is a standard pageview tracking tag and you can name it `Google Analytics Page View`
 1b. Click on New and in the Tag Configuration box choose the tag type _Universal Analytics_ with track type _page view_, and for the _Google Analytics Settings_ select your _Site-Name Google Analytics_ variable that you created previously to supply all site information.
 1c. Select _More Settings_ > Ecommerce  > select _True_ from the dropdown > check _Use Data Layer_ checkbox. Save this tag.
 2a. Create your second tag, this one is for tracking the completion of the donation as an event; name it accordingly. If you have set up a transaction tracking for Teamraiser you can just add an additional trigger to the same tag.
 Ex: _GA - Transaction Complete_
 2b. Select tag type _Universal Analytics_, for _Track Type_ select _Transaction_ and for _Google Analytics Settings_ select the  _Site-Name Universal Google Analytics_ variable that you created previously and used in the creation of the first tag.
 2c. The trigger for this event is the Custom Event trigger we created named _Donation Complete Event_ created in step 4 above.
 3a. Create your third tag, this one is for tracking donation errors; name it accordingly.  Ex: _GA - Transaction Error_.
 3b. Select tag type _Universal Analytics_, for _Track Type_ select _Event_. Enter `luminate donation` or something similar for the _Category_. Enter `error` for the _Action_. Enter `{{Error Mesage}}` for the _Label_ and `{{numberOfErrors}}` for _Value_. For the _Google Analytics Settings_ select your _Site-Name Google Analytics_ variable that you created previously to supply all site information.

6. Create new User-Defined variables for each of the data layer fields that you have in your GTM data layer array.
 Careful not to alter the left field values in the data layer as those must be camel case and must stay named as they are by Google default.
 The values assigned to each field on the right are the ones coming from server/site side and you can name those yourself accordingly.
 1a. When creating a new variable select 'Data Layer Variable' for the variable type, and for the data layer variable name field enter
 the left field values in the data layer array. Ex: 'transactionId'. If you have an array field within the data layer array you must annotate that in the data layer variable name field accordingly. Ex: 'sku' would be 'transactionProducts.0.sku'. The following variables will have to be defined for our code to work out of the box. Note that GTM will automatically know what to do with `transactionX` fields on a tag that is marked as _Transaction_.
    - `transactionId`
    - `transactionAffiliation`
    - `transactionTotal`
    - `transactionTax`
    - `transactionShipping`
    - `transactionProducts`
    - `numberOfErrors`
7. Once you've created variables for all of your data layer fields return to the transaction tag created earlier and add the data layer fields.
 1a. Go to More Settings > Fields to Set  and begin adding fields. The Field Name column are the fields that will show up in the Google Analytics breakdown, there is no documentation found on if/how specific the nameing needs to be but stick to simple naming like 'id', 'sku', 'shipping'.
 The Value column is the variable you created that links to the Data Layer array, enter those here.
8. If you are wanting to use debug mode click 'Preview' at the top right menu area in GTM and go to your site.
 A Google Tag Manager workspace area will pop up on the bottom of your screen and here you can view the data layer, your variables, and see which tags are being fired on each page.

## How to Get Help
If you run into issues with this code or need assistance implementing analytics in other Blackbaud Luminate Online module. [Contact DNL Omnimedia](https://www.dnlomnimedia.com/contact/?utm_source=github&utm_medium=web&utm_campaign=bbdevconference).
