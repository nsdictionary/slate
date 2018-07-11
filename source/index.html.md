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
  - api/user/create_user
  - api/user/user_info
  - api/user/register_user
  - api/user/get_list_data
  - api/verifications/create_bank_verification
  - api/verifications/create_document_verification
  - api/verifications/create_mobile_verification
  - api/verifications/verify_mobile
  - api/verifications/verify_bank
  - api/recipient/remittance_codes
  - api/recipient/recipient_params
  - api/recipient/create_recipient
  - api/recipient/recipient_info
  - api/transfer/check_commission
  - api/transfer/create_transfer
  - api/transfer/check_transfer_status
  - api/transfer/cancel_transfer
#   - callback
  - errors
  - update_log

search: true
---

# Introduction
currently in beta

# Getting Started
아래 이미지와 같은 절차를 통해 송금이 진행됩니다.

3가지 단계를 통해 센트비 API를 사용하실 수 있습니다:

1. Contact email(<a href="mailto:contact@sentbe.com">outbound@sentbe.com</a>) 을 통해 센트비의 파트너사로 등록합니다.
2. 등록후 접속 정보를 받아서 API호출에 필요한 개발을 진행할 수 있습니다.
3. API를 통해 거래를 생성하고 Traking 합니다.
