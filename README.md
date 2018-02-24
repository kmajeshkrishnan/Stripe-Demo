## Stripe-Backend

- Backend support for charge card using stripe API
  - python3 flask setup with a `requirements.txt` file
  - Gunicorn integration
  - Auto-reloading for local development
  - Ready to go Dockerfile that will automatically install deps from `requirements.txt`

### Deployment instructions

### Basic deployment:

* Clone the repository
``` shell
git clone https://github.com/kmajeshkrishnan/Stripe-Demo.git
```
* Replace the 'secret_key' with your secret key in server.js file

### Request Format
Get a token by requesting at stripe api endpoiint
``` shell
 'https://api.stripe.com/v1/tokens', {
    method: 'POST',Req
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded',
      'Authorization': 'Bearer <public-key>'
    },
    body: formBody
  }
```
where formBody will be
``` shell
 formBody = {
    'card[name]':<name>,
    'card[number]':<card-no>,
    'card[exp_month]':<exp-month>,
    'card[exp_year]':<exp-year>,
    'card[cvc]':<cvc>
  };
```
A successful request will return an access token. Make a request to the <b>backend</b> using th token just received
``` shell
 'https://app.backpedal70.hasura-app.io/charge',{
    method: 'POST',
    body: formData
    }
```
where formData will be
``` shell
 formData = {
    'stripeToken':<token>,
    'stripeEmail':<email>,
    'stripeAmount':<amount>,
  };
```
That's it. Transaction status can be obtained from the response. All transactions can be viewed on Transactions tab at stripe dashboard.

