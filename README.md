### Using Muk APIs
### How to custom Endpoint:
- Access Setting -> API -> Configuration -> Endpoint
- On listing endpoints click to button Create
#### 1. Sales Advance Payment Invoices
- Name: _Sales Advance Payment Invoices_
- Endpoint: `sale-order-create-invoices`
- HTTP Method: `POST`
- Model: `sale.advance.payment.inv`
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
#### 2. Immediate Transfer
- Name: _Delivery Order Immediate Transfer_
- Endpoint: `delivery-order-immediate-transfer`
- HTTP Method: `POST`
- Model: `stock.immediate.transfer`
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

### Any Question ?
