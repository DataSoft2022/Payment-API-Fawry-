# Payment-API-Fawry-
API DOC 



# Payment Request API  [ GET] Request 

Get all Invoices from Payment Request Document 

* GET  /Payment Request 

* Method : GET

* url :  {{base_url}}/api/resource/Payment Entry

* body : {form-data}

| key | Value |
| ---- | ----- |
| filters | [["party", "=", "1710"],["status","=","Requested"]] |
| fields | ["status","party","reference_doctype","reference_name","currency","grand_total"] |

**filters** : on which the data will be filtered

**Note** : **"party"** is the only variable in this API , the rest are **FIXED**

**party** : It Is Member ID that will retrieve all the invoices belongs to this Member ID to pay it via Fawry 

**fields** : data fields on the response 


* Sample Request 

```

curl --location --request GET '{{base_url}}/api/resource/Payment Request' \
--header 'Authorization: token apiKey:apiSecret ' \
--header 'Cookie: full_name=Guest; sid=Guest; system_user=no; user_id=Guest; user_image=' \
--form 'filters="[[\"party\", \"=\", \"1710\"],[\"status\",\"=\",\"Requested\"]]"' \
--form 'fields="[\"status\",\"party\",\"reference_doctype\",\"reference_name\",\"currency\",\"grand_total\"]"'

```

* Sample Response 

```
{
    "data": [
        {
            "status": "Requested",
            "party": "1710",
            "reference_doctype": "Sales Invoice",
            "reference_name": "INV-2022-01299",
            "currency": "EGP",
            "grand_total": 500.0
        }
    ]
}

```





# Payment Entry API [POST]

Sending Fawry Successful Payment from Payment Request Response to Payment Entry

* POST /Payment Entry 

* Method: POST
* url : {{base_url}}/api/resource/Payment Entry

* body : {form-data}

| Key  | Value |
| ------------- | ------------- |
| data  | {data attributes} |


data attributes

| Key  | Description | Value |
| ----- | ----- | ----- |
| payment_type | Type of Payment, it will be **FIXED**  | Receive |
| posting_date  | posting date in ISO Format  | YYYY-MM-DD |
| party_type | party type of the member is Customer, it will be **FIXED** | Customer |
| party | it is member's Number | number |
| part_name | it is member's name | member's name |
| paid_amount | it is the amount he paid throug fawry | amount |
| received_amount | it is the same value as paid_amount | amount |
| source_exchange_rate | exchange rate of the currency | string |
| paid_to | to be determined | ttt |
| reference_no | it will be the transaction ID or any reference number of Fawry successfull Response | fawry ref |
| reference_date | date of the transaction in iso format | YYYY-MM-DD |
| references | a list of sales invoces references | list
| reference_doctype | sales invoice reference | Sales Invoice |
| reference_name | Invoice Name | Text |
| total_amount | sales invoice's amount to be paid by the user | amount


 #f03c15 Note : reference_name & total_amount were retrieved in a previous api sent before :  GET {base_url}/api/Sales Invoice 
 
 
```diff
- Note : reference_name & total_amount were retrieved in a previous api sent before :  GET {base_url}/api/Sales Invoice
```


* Sample 


```
curl --location --request POST 'http:{{base_url}}/api/resource/Payment Entry' \
--header 'Authorization: token ' \
--header 'Content-Type: application/json' \
--header 'Cookie: full_name=Guest; sid=Guest; system_user=no; user_id=Guest; user_image=' \
--data-raw '{
    "data": {
        "payment_type": "Receive",
        "posting_date": "2022-10-10",
        "party_type": "Customer",
        "party": "1710",
        "party_name": "محمود فتحى احمد احمد حسن",
        "paid_amount": "500.00",
        "received_amount": "500.00",
        "source_exchange_rate": "'\''1",
        "paid_to": "13211 - بنك الاستثمار العربى جنيه - TC",
        "reference_no": "2333",
        "reference_date": "2022-10-10",
        "references": [
            {
                "reference_doctype": "Sales Invoice",
                "reference_name": "INV-2022-01298",
                "total_amount": "500.000"
            }
        ]
    }
}'

```




* Sample Response 

```
{
    "data": {
        "name": "ACC-REC-2022-00233",
        "owner": "ahmed.m@datasofteg.com",
        "creation": "2022-12-22 15:00:52.986696",
        "modified": "2022-12-22 15:00:53.379009",
        "modified_by": "ahmed.m@datasofteg.com",
        "parent": null,
        "parentfield": null,
        "parenttype": null,
        "idx": 0,
        "docstatus": 0,
        "naming_series": "ACC-REC-.YYYY.-",
        "payment_type": "Receive",
        "payment_order_status": "Initiated",
        "posting_date": "2022-10-10",
        "company": "The Club",
        "mode_of_payment": null,
        "party_type": "Customer",
        "party": "1710",
        "party_name": "محمود فتحى احمد احمد حسن",
        "bank_account": null,
        "party_bank_account": null,
        "contact_person": null,
        "contact_email": null,
        "party_balance": 0.0,
        "paid_from": "العضويات قسط بالفائدة - TC",
        "paid_from_account_type": null,
        "paid_from_account_currency": "EGP",
        "paid_from_account_balance": -17117158.0,
        "paid_to": "13211 - بنك الاستثمار العربى جنيه - TC",
        "paid_to_account_type": "Bank",
        "paid_to_account_currency": "EGP",
        "paid_to_account_balance": 6501580.0,
        "paid_amount": 500.0,
        "paid_amount_after_tax": 500.0,
        "source_exchange_rate": 0.0,
        "base_paid_amount": 0.0,
        "base_paid_amount_after_tax": 0.0,
        "received_amount": 500.0,
        "received_amount_after_tax": 500.0,
        "target_exchange_rate": 0.0,
        "base_received_amount": 0.0,
        "base_received_amount_after_tax": 0.0,
        "total_allocated_amount": 0.0,
        "base_total_allocated_amount": 0.0,
        "unallocated_amount": 0.0,
        "difference_amount": 0.0,
        "purchase_taxes_and_charges_template": null,
        "sales_taxes_and_charges_template": null,
        "apply_tax_withholding_amount": 0,
        "tax_withholding_category": null,
        "base_total_taxes_and_charges": 0.0,
        "total_taxes_and_charges": 0.0,
        "reference_no": "2333",
        "cheque_": null,
        "cheque_status": "Open",
        "reference_date": "2022-10-10",
        "clearance_date": null,
        "number_of_checks": null,
        "customer_bank": null,
        "check_no": null,
        "check_amount": null,
        "check_date": null,
        "mode_of_payment_per_check": null,
        "supplier": null,
        "employee": null,
        "department": null,
        "contact": null,
        "customer": null,
        "project": null,
        "cost_center": null,
        "status": "Draft",
        "custom_remarks": 0,
        "remarks": "Amount EGP 500.00 received from 1710\nTransaction reference no 2333 dated 2022-10-10",
        "letter_head": "The Club",
        "print_heading": null,
        "bank": null,
        "bank_account_no": null,
        "payment_order": null,
        "auto_repeat": null,
        "amended_from": null,
        "title": "1710",
        "doctype": "Payment Entry",
        "references": [],
        "taxes": [],
        "deductions": [],
        "check_list": []
    }
}
```





