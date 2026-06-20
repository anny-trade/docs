---
faq:
  - q: "Does Anny need the Withdraw permission on my OKX API key?"
    a: "No. Never check the 'Withdraw' field. Anny only needs the 'trade' permission — leaving withdrawals off protects both you and Anny."
  - q: "What IPs should I restrict my OKX API key to for Anny?"
    a: "18.197.221.166, 3.120.52.14, 3.124.90.105, 3.124.91.26, 3.124.99.155."
  - q: "Do I need a passphrase to connect OKX to Anny?"
    a: "Yes. OKX V5 API keys require a passphrase. Set one when creating the key and enter it in Anny alongside the API and secret keys."
---
# How do I connect OKX to Anny?

In order to use Anny it's necessary to have an exchange account.

So let's prepare OKX API keys and connect them to Anny.

In case you don't have one yet, create an account using [this link.](https://www.okx.com/join/29916875)

## **Preparing OKX API keys**

A very important point in this step is to **create an exclusive API for Anny**.

To do this, login to OKX and access your settings: click on your profile (in the right corner) > API > Create V5 API key

Give your API a name and create a Passphrase.

Select the "trade" field and copy-paste Anny's restricted IPs.

**IMPORTANT: NEVER** check the "Withdraw" field - this is the withdrawal permission and it's not required to operate with Anny. This will protect both, you and Anny. The withdrawal permission is not checked, just keep it as it is.

**Coy-paste the restricted IPs:** 

18.197.221.166,3.120.52.14,3.124.90.105,3.124.91.26,3.124.99.155

By confirming the API and Private keys will be generated, save them somewhere as you will need to copy and paste them into Anny.

If you are going to operate the futures account, make sure that the account mode is not set to Simple.

##

## **Connect the API keys to Anny**

To connect the API and secret keys to Anny access your Profile (upper right corner), click on "Settings" then select "Exchanges".

Click on "Add exchange", select the correct exchange and paste the API and Secret keys along with the passphrase.
## See Also

- [How do I connect Binance to Anny?](binance.md)
- [How do I connect Bybit to Anny?](bybit.md)
- [How do I create an Anny Trade account?](../getting-started/register.md)

> **Anny Trade** — AI crypto portfolio intelligence, 29,000+ traders across 7 exchanges, since 2019. [anny.trade](https://anny.trade)
