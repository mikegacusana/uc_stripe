
This is a payment gateway module for Stripe. 

!! IMPORTANT !!
This module is a work in progress and as such has not been extensively tested in a production environment. DO NOT INSTALL THIS IN A PRODUCTION ENVIRONMENT. If you want to help test, please do, but do not use it for anything mission critical until it has been tested further.

It has experimental support for the development
uc_recurring-6.x-2.x API for recurring payments, using the ability to 
store credit card details at Stripe and then make charges with
the returned transaction ID and no credit card #.

It is recommended to use the latest version of Ubercart 6.x with this
module. 

Installation and Setup
======================

a) Install and enable the module in the normal way for Drupal.

b) Visit your Ubercart Store Administration page, Configuration
section, and enable the gateway under the Payment Gateways.
(admin/store/settings/payment/edit/gateways)

c) On this page, provide the following settings: 
   - Your Stripe API key, private

d) Download and install the latest version of the PHP Stripe library. (https://github.com/stripe/stripe-php) Put it in sites/all/libraries/stripe such that the path to Stripe.php is sites/all/libraries/stripe/lib/Stripe.php

e) If you are using recurring payments, install the uc_recurring module. (http://drupal.org/project/uc_recurring) and set up as described below

Supports recurring payments with uc_recurring 2.x series.


Recurring Payments Setup
========================

First, you'll need the uc_recurring module (http://drupal.org/project/uc_recurring) installed. It is not listed as a dependency for this Stripe payment module because this module could be used without recurring payments. But it is a dependency to use the recurring payments piece of this module.

Create a product in your Drupal site. After creating that product, edit it and click on the "Features" tab. Under "Add a new feature," select "Recurring fee" and click add. In order for this to work with Stripe, you must select the "Applicable SKU." This will create the subscription plan in Stripe (provided of course that you have your API keys set up). Then, later, when a user purchases this product, they will get added as "Customers" to this "Plan."

Notes:
 - Stripe doesn't have a way to set the number of billing periods. So basically people are subscribed or unsubscribed, not subscribed for 12 months then done. We hope to add the ability to change this later, but we would have to do it on our end. So for example, we would have to keep track of the time since the subscription started in Drupal and send Stripe a request when that time is up.


Todo
====
 - Enable set number of billing periods. So the system will keep track of the time and then shoot of a request to Stripe via cron to cancel the subscription once the billing period is up.
