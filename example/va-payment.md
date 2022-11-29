# Xfers static va payment method

Source:
Fazz documentation : https://docs.fazz.com/v4-ID/docs/virtual-account#creating-a-static-va-for-unlimited-payments

landx xfres sdk : https://github.com/landx-id/xfers-python-sdk

## Use Cases
Static VA payment method digunakan untuk melakukan top up dana yang akan menjadi fitur landx kedepan, penggunaannya antara lain adalah 
- booking lot top up saldo aktif


## Database Schema

Kita memerlukan beberapa perubahan pada database untuk menyimpan static VA milik `user` yang nantinya akan digunakan untuk melakukan validasi pembayaran.

Nama Table: `users`

Kolom:
- `user_id` *string(50) nullable* - digunakan untuk menyimpan id user yang telah membuat atau merequest static VA.
- `bank` *string(50) nullable* - digunakan untuk menyimpan referensi bank dari va yang didaftarkan.
- `va_number` *string(50) nullable* - digunakan untuk menyimpan nomor static VA.
- `is_active` *string(50) nullable* - digunakan untuk melakukan pengecekan apakah VA masih aktif.
- `created_at` *string(50) nullable* - menyimpan data kapan static va dibuat.

## Creating Static VA

![xfers-create-va-screenshot](/images/xfres-create-va.png)

Please check [LandX XFers SDK Reference](ttps://github.com/landx-id/xfers-python-sdk).

1. Requesting Static VA
```python
payment_method = xfers.PaymentMethod

payment_method.create(
  type="virtual_bank_accounts", # type of payment method
  reference_id="12345678", # reference id ex user_id, transaction_id .etc
  bank_short_code="SAHABAT_SAMPOERNA", # bank code
  display_name="Your preferred name", # name of static VA (already include IKN-)
  suffix_no="12345678" # suffix number from static VA
)
```

## Xfers payment notification
![xfers-registration-status-screenshot](/images/xfers-received-payment.png)

URL:
- Production URL: https://example-url.landx.id
- Staging URL: https://example-url.staging.landx.id
- Endpoint: [POST] `/xfers/callback`
- Auth : HMAC ENCRYPTION

Auth Verification Function:

```python
def check_signature(signature_payload,payload):
    """Xfers Auth Middleware"""
    signature = hmac.new(
        bytes(FAZZ_SIGNATURE , 'latin-1'), 
        msg = payload, 
        digestmod = hashlib.sha256).hexdigest()
    verify = hmac.compare_digest(signature, signature_payload)
    return verify
```

Payload Example:

```json
{
    "data": {
        "id": "contract_480d338b1a3d43b0b2c550a0c677855f",
        "type": "payment",
        "attributes": {
            "status": "paid",
            "amount": "50000.0",
            "createdAt": "2022-09-30T14:50:15+07:00",
            "description": null,
            "expiredAt": null,
            "referenceId": "external_id_37a6ef01a3",
            "fees": "3663.0",
            "paymentMethod": {
                "id": "va_e2c53cd65b6f640d552d0bebe11f4af2",
                "type": "virtual_bank_account",
                "referenceId": "2-rafly",
                "instructions": {
                    "bankShortCode": "SAHABAT_SAMPOERNA",
                    "accountNo": "2020240083617485",
                    "displayName": "IKN-Rafly Lesmana putra"
                }
            }
        }
    }
}
```

