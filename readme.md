# Extra Technical Challenge: Applying Discount

## Objective

Modify the `POST /order` endpoint to allow customers to apply a percentage discount to the total order amount. The discount will not be persisted in the database but will be used to calculate the `final_total` and returned in the response.

## Implementation Scope

1. Add support for the `discount` field in the existing endpoint
2. Implement necessary validations
3. Calculate discount values and final total
4. Return new fields in the response

### Endpoint

`POST /order`

### New Optional Field in Request Body

```json
"discount": 10 // (optional, number between 0 and 100)
```

### Additional Validations

- The discount is applied after calculating the total of items
- The discount value must be a number between 0 and 100
- If discount is null, undefined, or empty string, consider it as 0

## New Expected Response Format

```json
{
  "id": 1,
  "customer_id": 1,
  "total": 50,
  "discount": 10,
  "discount_amount": 5,
  "final_total": 45,
  "items": [
    {
      "menu_item_id": 2,
      "quantity": 2
    }
  ]
}
```

## Details of Added Response Fields

| Field             | Description                                          |
| ----------------- | ---------------------------------------------------- |
| `total`           | Total value of items without discount                |
| `discount`        | Percentage discount applied (if provided)            |
| `discount_amount` | Absolute discount value (total * (discount / 100))   |
| `final_total`     | Final total after discount (total - discount_amount) |
