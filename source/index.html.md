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
  - api/user_info
  - api/recipient_params
  - api/create_recipient
  - api/recipient_info
  #  - api/update_user_info
  #  - api/update_recipient_info
  - api/bank_info
  - api/balance_info
  - api/check_commission
  - api/create_transfer
  - api/check_transfer_status
  - api/get_list_data
  - callback
  - errors
  - update_log

search: true
---

# Introduction
Sentbe provides a simple yet powerful API that allows partners to send cross-border payments for end-to-end delivery within just minutes of time.
The API enables our partners to send transfers to anyone in Korea securely and conveniently. Experience Sentbe's instant bank-to-bank transfer with best FX conversion and payout fees in the market.


# Getting Started
아래 이미지와 같은 절차를 통해 송금이 진행됩니다.
![Image](./images/api_graph.svg)

3가지 단계를 통해 센트비 API를 사용하실 수 있습니다:

1. Contact email(<a href="mailto:contact@sentbe.com">outbound@sentbe.com</a>) 을 통해 센트비의 파트너사로 등록합니다.
2. 등록후 접속 정보를 받아서 API호출에 필요한 개발을 진행할 수 있습니다.
3. API를 통해 거래를 생성하고 Traking 합니다.
