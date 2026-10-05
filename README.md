# omnibus/jdl-express

JD Logistics (京东物流) for [glitchr/omnibus](https://github.com/glitchr-studio/omnibus):
orders with their waybills and labels, tracking and cancellation - the open platform's signed
ECAP APIs. Prices come from configuration (`rates`): JD quotes by contract.

```php
$gateway = (new JdlExpressGatewayFactory($http))->create($options);   // $http: the application's HTTP client - none given, the factory makes its own; the options below
```

No framework needed: the package requires `glitchr/omnibus` and `symfony/http-client`. In a
Symfony application, the same through the bundle's configuration:

```yaml
omnibus:
    gateways:
        jdl_express:
            factory: jdl_express
            options:
                app_key: '%env(JDL_APP_KEY)%'
                app_secret: '%env(JDL_APP_SECRET)%'
                access_token: '%env(JDL_ACCESS_TOKEN)%'
                customer_code: '%env(JDL_CUSTOMER)%'     # 商家编码
                sandbox: true
                rates: [...]
```

The service is the product code (ed-m-0001 特惠送 by default, ed-m-0002 特快送...). Addresses: the
third street line carries the province. Shipment options: `description`, `instructions`,
`template`. No pickup points.

Credentials: an app on [JD Logistics' open platform](https://open.jdl.com) gives the app key and
secret; the merchant's authorisation gives the access token and the 商家编码 (UAT first).

Built from JD Logistics' published open platform documentation and tested on recorded answers;
**unverified** against UAT until an account's keys are at hand.

License: LGPL-3.0-or-later.
