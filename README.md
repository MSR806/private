# Purchase Receipt - Client Side

Assigned To: M Sujith Reddy
Created: Apr 30, 2021 12:13 AM
Created By: M Sujith Reddy
Last Edited By: M SUJITH REDDY
Last Edited Time: May 14, 2021 5:12 PM
Status: In Progress 🙌
Tags: ERPNext, Purchase Receipt
Type: Tech documentation

# Purchase Receipt

## Custom Variables

[Purchase Receipt](https://www.notion.so/d9316da0ecb04fc09fe455840c8f3bd9)

## Custom Triggers

### `add_rows:`

- Add `number_of_rows` more to the existing rows.

### `validate:`

- Lorem Ipsum

### `onload:`

- Call `new_entry_button()`

### `refresh:`

- Call `change_color_code()`
- Call `new_entry()`
- Call `add_delete_button()`
- Call `create_item_template()`

    ### `cash_discount_type:`

- Lorem Ipsum

### `gst:`

- Call `calculate_item_level()` for each item
- When `gst == "INCLUSIVE"` then assign `included_in_print_rate == 1` in the taxes table in purchase receipt which is hidden, then erpnext will calculate the amount as tax include which will also do the entries properly in the ledgers.
- `frm.refresh_field("taxes");`

# Purchase Receipt Item

## Custom Variables

Not Used variable are deleted from the client side but they still exist in the database. But when you install this customized app into a new instance then they won't be created.

[Purchase Receipt Item](https://www.notion.so/638a0fa4184a41f489ea822949ccd58c)

## Custom Triggers

### `item_code:`

- If `item_code`
    - check if this `item_code` is not a template(sometimes templates gets selected)
- Call `calculate_item_level()`

### `data_quantity:`

- Parse `data_quantity` to float
- Copy the `data_quantity` to qty
- Call `calculate_item_level()`

### `qty:`

- Call `calculate_item_level()`

### `bill_amount`

- Call `calculate_item_level()`

### `change_bill_mrp:`

- Call `calculate_item_level()`

### `bill_mrp_c:`

- Call `calculate_item_level()`

### `item_tax_template_custom:`

- From the custom tax template selected, fetch the `tax_percentage` of that template and store that value in `gst_percentage`
- Call `calculate_item_level()`

# Custom Functions

## `calculate_item_level`

Check if these values are entered

- `item_code`
- `data_quantity`
- `bill_amount`
- If `change_bill_mrp`
    - Make sure `bill_mrp_c` is entered(msg.print)
- **Two cases — GST : INC & EXC**
    - Create two variables `bill_total` & `bill_tax`
    - `gst == "INCLUSIVE"`
        - bill MRP change
            - set `received_mrp_c` to this variant's MRP
            - Calculate `sk_amount`
        - bill MRP no change
            - Calculate `sk_amount`
        - Calculate
            - `sk_rate`
            - `rate`
            - `gst_amount`
    - `gst == "EXCLUSIVE"`
        - bill MRP change
            - Calculate `sk_amount`
        - bill MRP no change
            - Calculate `sk_amount`
        - Calculate
            - `sk_rate`
            - `rate`
            - `gst_amount`
- Check if the `sk_rate` is greater than MRP — msg.print
- Call `change_color_code()`
- `calculate_receipt_level`
- `row.amount = row.sk_amount;` — COME BACK TO THIS (ig Not Needed)
- refresh fields

## `add_delete_button`

- Once Discard button is clicked the form should be deleted and it should go back.

## `new_entry_button`

## `change_color_code`

## `create_item_template`

## `check_template`

## `create_doc`
