# Cielo-API-3.0

Projeto em .NET para integração com a API de pagamento Cielo API 3.0.

### Métodos

- CreateTransaction
- GetTransaction
- CancellationTransaction
- CaptureTransaction

### Exemplo de uso em ambiente sandbox
- Transação com captura
```
/* api instance */
var api = new CieloApi(CieloEnvironment.Sandbox, Merchant.Sandbox);

/* customer */
var customer = new Customer(name: "Fulano da Silva");

/* customer credit card */
var creditCard = new CreditCard(
    cardNumber: SandboxCreditCard.Authorized1, 
    holder: "Teste Holder", 
    expirationDate: new DateTime(DateTime.Now.Year + 1, 12, 1), 
    securityCode: "123", 
    brand: Enums.CardBrand.Visa,
    saveCard: false);

/* create payment with credit card */
var payment = new Payment(
    amount: 119.19M, 
    currency: Enums.Currency.BRL, 
    installments: 1, 
    capture: true, 
    softDescriptor: ".Net Test Project", 
    creditCard: creditCard);

/* store order number */
var merchantOrderId = new Random().Next();

/* transaction data */
var transaction = new Transaction(
    merchantOrderId: merchantOrderId.ToString(), 
    customer: customer, 
    payment: payment);

/* call Cielo Api */
var returnTransaction = api.CreateTransaction(Guid.NewGuid(), transaction);
```

### Links
* [Cielo API 3.0] (http://developercielo.github.io/Webservice-3.0)
* [Webservice 1.5] (http://bit.ly/2bO2Cw2)
* [Merchant Key e Merchant Id em Sandbox] (https://cadastrosandbox.cieloecommerce.cielo.com.br)
* [Github da Cielo] (https://github.com/DeveloperCielo)
* [Cielo Developers] (https://www.cielo.com.br/desenvolvedores)

### Geração de pacote - Nuget pack
``` 
> nuget pack -Prop Configuration=Release -Prop AssemblyName=CieloSharpAPI -Build
```
* [Package published] (https://www.nuget.org/packages/CieloSharpAPI)
