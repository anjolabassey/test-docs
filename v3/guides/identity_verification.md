## Identity verification

You can verify the identity of a customer through BVN Validation. It allows you verify a BVN supplied by a customer. It can also be used for KYC methods such as validating certain data given by the customer such as date of birth, mobile number and full name. Each API call to validate a BVN costs 50 NGN. This would require you to fund your Rave account adequately. To fund your account, navigate to Transfers on your dashboard and use the  Topup Balance option. 

&nbsp;

<img src="https://res.cloudinary.com/fullstackmafia/image/upload/v1576476481/image_preview_20_piesds.png"/>

&nbsp;

To top up your test account, follow the steps below:


- Select the currency you would like to top up and input the amount you would like to top your account up with.

&nbsp;

<img src="https://res.cloudinary.com/fullstackmafia/image/upload/v1576476554/image_preview_21_kverle.png"/>

&nbsp;


- When the Rave payment modal comes up, select  `Access Bank`.
-  Use this test account number -   `0690000031`.
- When prompted to input an OTP, use  `12345`.


**Pre-requisites for using the BVN validation service.**


1. Sign-up for a test account [here](https://ravesandbox.flutterwave.com/), and for a live account [here](https://rave.flutterwave.com/) .
2. Retrieve your secret key to make authenticated calls to the BVN API.

**Storing BVN Information** <br>
**You are strongly advised to not store or encrypt BVN information in your database or any other storage format.**

To verify a customer's identity make an API call similar to the one below:

**Sandbox Endpoint**: `https://ravesandboxapi.flutterwave.com/v2/kyc/bvn` <br>
**Live Endpoint**: `https://api.ravepay.co/v2/kyc/bvn`

```python

    url = "https://ravesandboxapi.flutterwave.com/v2/kyc/bvn/1234567890?"
    querystring = {
      "seckey": "FLWSECK_TEST-09891ac8c459eafdb10e3afccc0df58d-X" #test secret key
    }
    headers = {
      'content-type': 'application/json'
    }
    response = requests.request("GET", url, headers = headers, params = querystring)
    print(response.text)

```

In the above request, we passed the BVN of the customer as a path to the endpoint and added our test secret key as a query parameter 

 `https://ravesandboxapi.flutterwave.com/v2/kyc/bvn/:bvnnumber?seckey=FLWSECK-e6db11d1f8a6208de8cb2f94e293450e-X`

**Sample Response:**

```python

    {
        "status": "success",
        "message": "BVN-DETAILS",
        "data": {
            "bvn": "12345678901",
            "first_name": "Wendy",
            "middle_name": "Chucky",
            "last_name": "Rhoades",
            "date_of_birth": "01-01-1905",
            "phone_number": "08012345678",
            "registration_date": "01-01-1921",
            "enrollment_bank": "044",
            "enrollment_branch": "Idejo"
        }
    }

```

