### Using Muk APIs
- Required instatlled Odoo APP *MuK Webhooks for Odoo*
- Version 1.0.2
- Last modified at: 2022-11-21

### How to custom Endpoints
- Access Setting -> API -> Configuration -> Endpoint
- On listing endpoints click to button Create
#### 1. Custom API Create Invoices
- Name: Enter name of API (ex: _Sales Advance Payment Invoices_)
- Endpoint: `create-invoices`
- HTTP Method: `POST`
- Model: Select model `sale.advance.payment.inv` (_Sales Advance Payment Invoice_)
- Evaluation Type: `Execute Python Code`
- Protected: `Yes`
- Sudo Evaluation: `Yes`
- Logging: `Yes`
- *Python codes setting*:
    ```python
    ids = params['args'][0] if params['args'] else False
    payment = model.browse(ids)
    context = params['with_context']
    if not context.get('active_model'):
      context['active_model'] = 'sale.order'
    payment.with_context(context).create_invoices()
    content = True
    ```
#### 2. Custom API Immediate Transfer for confirm DO
- Name: Enter name of API  (ex: _Immediate Transfer_)
- Endpoint: `immediate-transfer`
- HTTP Method: `POST`
- Model: Select model `stock.immediate.transfer` (_Immediate Transfer_)
- Evaluation Type: `Execute Python Code`
- Protected: `Yes`
- Sudo Evaluation: `Yes`
- Logging: `Yes`
- *Python codes setting*:
    ```python
    ids = params['args'][0] if params['args'] else False
    context = params['with_context'] or env.context
    immediate = model.browse(ids)
    immediate.with_context(context).process()
    content = True
    ```
#### 3, Custom API Register Payment
- Name: Enter name of API  (ex: _Create Register Payment_)
- Endpoint: `create-register-payment`
- HTTP Method: `POST`
- Model: Select model `account.payment.register` (_Register Payment_)
- Evaluation Type: `Execute Python Code`
- Protected: `Yes`
- Sudo Evaluation: `Yes`
- Logging: `Yes`
- *Python codes setting*:
    ```python
    context = params["with_context"]
    data = params["args"][0]
    instance = model.with_context(context).create(data)
    content = instance.ids
    ```
  
### How to custom Webhook

### Frequently questions ?
