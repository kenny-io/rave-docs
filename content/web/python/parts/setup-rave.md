## Setup Rave

Assuming you’ve signed up using a sandbox account, login to your **Ravepay** Dashboard and at the sidebar, click on **Setup Rave**.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_8CA58C87BD82C742CD0884051C7ADAB3BACA5DC2CB44CB404AA1A0C3C4832142_1522280153710_Screenshot+from+2018-03-29+00-28-11.png)

When you click on **Setup Rave**,  you will be shown a handful of options via which you can start collecting payments:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_8CA58C87BD82C742CD0884051C7ADAB3BACA5DC2CB44CB404AA1A0C3C4832142_1522281473908_Screenshot+from+2018-03-29+00-57-40.png)

Since we are integrating Rave with Flask, how to accept payments with Rave in our custom applications should be our concern here. To be able to generate the payment modal on your application, you first need to include the test script URL in your application. The importance of the test script is to load the modal. It works in a fashion similar to how images load over content delivery networks.

    <html>
      <script type="text/javascript" src="https://ravesandbox.flutterwave.com/flwv3-pug/getpaidx/api/flwpbf-inline.js"></script>
    </html>

When you are done including the test script, you need to embed Rave’s inbuilt  `getPaidSetup` function in your code. The  `getPaidSetup`  function is one of Rave’s core functions and is an integral part of Rave’s engine, it is responsible for handling the payments your customers make on your page. Below is a basic example of how the `getpaidSetup` function will appear in your application’s code:

      <script>  
          getpaidSetup({
          PBFPubKey: "YOUR PUBLIC KEY",
          customer_email: "user@example.com",
          custom_title: "OGTECH",
          amount: 500,
          customer_phone: "233546744623",
          payment_method: "both",
          txref: "rave-123456",
          onclose: function() {},
          callback: function(response) {
            var flw_ref = response.tx.flwRef;
            console.log("This is the response returned after a charge", response);
            if (
              response.tx.chargeResponseCode == "00" ||
              response.tx.chargeResponseCode == "0"
            ) {
              // redirect to a success page
              console.log('Payment Successful')
            } else {
              // redirect to a failure page
              console.log('Error! Issue with Payment')
            }
          }
        });
      </script>  

The `getPaidSetup` function needs a public key, this key serves as the link between your Rave account and the Payment Button you want to create. To view your public as well as secret key, on your Rave dashboard navigate to **Settings** >> **API** 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_8CA58C87BD82C742CD0884051C7ADAB3BACA5DC2CB44CB404AA1A0C3C4832142_1524003443152_Screenshot+from+2018-04-17+23-16-54.png)

>  **CAUTION**: The **public key** is used when embedding the pay button, it can be used on the **client page**. The **secret key** is very sensitive to your Rave account and should not be exposed to your **client page**. Do not commit your **secret key** to GitHub or any other versioning system and ensure you only use your **secret key** on the **server side**. Kindly re-read this paragraph. 

After you have implemented the `getpaidSetup`  function in your code and your customers want to make payments to your account, they should see a modal similar to this:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_8CA58C87BD82C742CD0884051C7ADAB3BACA5DC2CB44CB404AA1A0C3C4832142_1522336147851_Screenshot+from+2018-03-29+15-24-07.png)

Should your payment go through, this is what your sample callback response will look like:

    {
      "status": "success",
      "message": "Charge Complete",
      "data": {
        "data": {
          "responsecode": "00",
          "responsemessage": "successful"
        },
        "tx": {
          "id": 10604,
          "txRef": "12373",
          "orderRef": "URF_1501152088995_7069035",
          "flwRef": "FLW-MOCK-f0ef7b5fc0e9a2e00e02169aff4572de",
          "redirectUrl": "http://127.0.0",
          "device_fingerprint": "69e6b7f0b72037aa8428b70fbe03986c",
          "settlement_token": null,
          "cycle": "recurring-daily",
          "amount": 290,
          "charged_amount": 290,
          "appfee": 0,
          "merchantfee": 0,
          "merchantbearsfee": 0,
          "chargeResponseCode": "00",
          "chargeResponseMessage": "Success-Pending-otp-validation",
          "authModelUsed": "PIN",
          "currency": "NGN",
          "IP": "197.242.109.215",
          "narration": "FLW-PBF CARD Transaction ",
          "status": "successful",
          "vbvrespmessage": "successful",
          "authurl": "http://flw-pms-dev.eu-west-1.elasticbeanstalk.com/mockvbvpage?ref=FLW-MOCK-f0ef7b5fc0e9a2e00e02169aff4572de&code=00&message=Approved. Successful",
          "vbvrespcode": "00",
          "acctvalrespmsg": null,
          "acctvalrespcode": null,
          "paymentType": "card",
          "paymentId": "2",
          "fraud_status": "ok",
          "charge_type": "normal",
          "is_live": 0,
          "createdAt": "2017-07-27T10:41:28.000Z",
          "updatedAt": "2017-07-27T10:41:42.000Z",
          "deletedAt": null,
          "customerId": 517,
          "AccountId": 134,
          "customer": {
            "id": 517,
            "phone": null,
            "fullName": "teni adebola",
            "customertoken": null,
            "email": "temi@gmail.com",
            "createdAt": "2017-06-02T10:33:13.000Z",
            "updatedAt": "2017-06-02T10:33:13.000Z",
            "deletedAt": null,
            "AccountId": 134
          },
          "chargeToken": {
            "user_token": "82bfc",
            "embed_token": "flw-t0-2a2646448375873c9060eeffe48bdedb-m03k"
          }
        }
      }
    }

To view sample callback responses for other situations such as a failed response, a declined transaction, insufficient funds etc,  do check out this [gist](https://gist.github.com/fullstackmafia/117b6046f968e14dcf3f6693816b815f) on Github.