# Kucoin — Connect Exchange

In order to use Anny it's necessary to have an exchange account.

Let's create the Kucoin API keys and connect them to Anny.

## **Preparing Kucoin API keys**

In order to create the API it's necessary to have an account and have it verified.

A very important point in this step is to **create an exclusive API for Anny**.

To do this, login to Kucoin and access your settings. Click on your profile (in the upper right corner) and then on API management.

Click on Create API, select the API-based trading tab, choose a name and create a Passphrase.

In the API restriction fields select the necessary key permissions to operate on Anny.

-   Spot trading
-   Futures trading

**IMPORTANT: NEVER** check the "Transfer" field - this is the withdrawal permission and it's not required to operate with Anny. This will protect both, you and Anny. The withdrawal permission is not checked, just keep it as it is.

**Coy-paste the restricted IPs:** 

18.197.221.166,3.120.52.14,3.124.90.105,3.124.91.26,3.124.99.155,52.57.104.76

 

By confirming, the API and Secret keys will be generated, save them somewhere as you will need to copy and paste them into Anny.

## **Connect the API keys to Anny**

To connect the API and secret keys to Anny access your Profile (upper right corner), click on "Settings" then select "Exchanges".

Click on "Add exchange", select the correct exchange and paste the API and Secret keys along with the passphrase.
