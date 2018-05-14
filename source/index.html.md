---
title: Sentbe API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - ruby
  - php
  - javascript

toc_footers:
  - <a href='mailto:dev@sentbe.com'>Contact for registration</a>

includes:
  - authentication
  - api/intro
  - api/create_user
  - api/create_recipient
  - api/user_info
  - api/recipient_info
  #  - api/update_user_info
  #  - api/update_recipient_info
  - api/bank_info
  - api/balance_info
  - api/check_commission
  - api/create_transfer
  - api/check_transfer_status
  - callback
  - errors
  - update_log

search: true
---

# Introduction
Sentbe provides a simple yet powerful API that allows partners to send cross-border payments for end-to-end delivery within just minutes of time.
The API enables our partners to send transfers to anyone in Korea securely and conveniently. Experience Sentbe's instant bank-to-bank transfer with best FX conversion and payout fees in the market.


# Getting Started
Here's how it works
![Image](./images/api_graph.svg)

Follow the given steps to start distribution with Sentbe:

1. Contact us at <a href="mailto:contact@sentbe.com">inbound@sentbe.com</a> and register as a partner of Sentbe
2. Deposit funds to your account to initiate FX conversion and payouts
3. Send us systematically generated requests via API on who to send the funds.
4. Track your requests via API.

## 1. Sender prefunds in USD
Sentbe can only accept USD prefunds due to series of compliance issues. That's why we are trying to give best exchange rate for KRW/USD in this market. 

As soon as prefunds arrived at settlement bank account shall be credited to USD wallet. 
Per each payout made, we shall convert credit from partner's USD wallet to KRW (Local Currency) using Sentbe exchange rate given at real-time.

Please feel free to contact us at <a href="mailto:contact@sentbe.com">inbound@sentbe.com</a> for further inquiries on prefunding.

## 2. Sender generates distribution requests
Sender generates a create_transfer API call to initiate a transfer to the recipient. As of now, local bank account is the only option available for fund transfer in Korea.
Once you've made the create_transfer API call, Sentbe will instantly send verification request to recipient.
(In case the recipient has already completed verfication, verification process will be skipped.)

As soon as recipient completes verification, Sentbe processes payout to recipient taking less than a minute to arrive.

## 3. Real-time update on payout progress
Partners may track payout progress real-time via API updates. We have 7-stage status updates for partners.

