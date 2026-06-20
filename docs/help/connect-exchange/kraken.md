# How do I connect Kraken to Anny?

In order to use Anny it's necessary to have an exchange account.

So let's prepare Kraken API keys and connect them to Anny.

**Preparing Kraken API keys**

In order to create an API it's necessary to have a Kraken account.

A very important point in this step is to **create an exclusive API for Anny**.

To do this, login to Kraken and access your settings: click on your profile (upper right corner)> Settings > API > create API key.

Select the necessary key permissions. The ones required to use Anny are the ones under the "Order & Trades" section and Query funds. 

**IMPORTANT: NEVER** check the "Withdraw Funds" field - this is the withdrawal permission and it's not required to operate with Anny. This will protect both, you and Anny. The withdrawal permission is not checked, just keep it as it is.

By clicking on "Generate key", API and Private key will be generated, save them somewhere as you will need to copy and paste them into Anny.

**Connect the API keys to Anny**

To connect the API and secret keys to Anny click on your Profile (upper right corner), then "Settings", select "Exchanges", "Add exchange" and paste the API and Secret keys.
