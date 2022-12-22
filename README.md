# Payment-API-Fawry-
API DOC 


# Payment Entry API 

Sending Fawry Successful Payment Response to Payment Entry

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


| Key  | Description | 
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |


{
    "data": {
        "payment_type": "Receive",
        "posting_date": "2022-10-10",
        "party_type": "Customer",
        "party": "1710",
        "party_name": "محمود فتحى احمد احمد حسن",
        "paid_amount": "2,000.00",
        "received_amount": "2,000.00",
        "source_exchange_rate": "'1",
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
}


