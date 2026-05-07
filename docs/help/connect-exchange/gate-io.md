# Gate.io — Connect Exchange

In order to use Anny it's necessary to have an exchange account.

So let's prepare Gate.io API keys and connect them to Anny.

**Preparing Gate.io API keys**

In order to create an API it's necessary to have a Gate.io account. In case you don't have one, create an account using [this link](https://www.gate.io/signup/VLEVU1AOBQ?ref_type=103).

A very important point in this step is to **create an exclusive API for Anny**.

To do this, login to Gate.io and access your settings:

Security Settings > Sub-accounts & APIs > API Management > Create API Key

**Coy-paste the restricted IPs:** 

18.197.221.166,3.120.52.14,3.124.90.105,3.124.91.26,3.124.99.155,52.57.104.76

Select the necessary key permissions. The ones required to use Anny are just the ones selected below "Spot Trade", "Perpetual Futures" e "Delivery Futures" com "Read And Write". 

**IMPORTANT: NEVER** check the "Withdraw Funds" field - this is the withdrawal permission and it's not required to operate with Anny. This will protect both, you and Anny.

By clicking on "Generate key", API and Private key will be generated, save them somewhere as you will need to copy and paste them into Anny.

**Connect the API keys to Anny**

To connect the API and secret keys to Anny click on your Profile (upper right corner), then "Settings", select "Exchanges", "Add exchange" and paste the API and Secret keys.
