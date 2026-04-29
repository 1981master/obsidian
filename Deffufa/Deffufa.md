<mark>Database + UI Connection Diagram (Flight → Contract → Services → Invoice)</mark>

```text
+----------------+         +--------------------+         +----------------+
|    Flight UI   |         |  Database Tables   |         |   Service UI   |
+----------------+         +--------------------+         +----------------+
| - Add Flight   |  --->   | flights            |  <---   | - Select Flight|
| - Select       |         |   id               |         | - Load services|
|   Contract     |  --->   |   flight_name      |         | - Merge contract|
| - Save Flight  |  --->   |   contract_id  ----|-------> |   pricing      |
|                |         |   departure_time   |         | - Display services|
|                |         |   arrival_time     |         | - Add to flight|
+----------------+         +--------------------+         | - Edit/Delete assigned|
                                                          |   services          |
                                                          +--------------------+
                                                                   |
                                                                   v
                                                          +----------------+
                                                          | Flight Services|
                                                          |  (invoice_services)|
                                                          +----------------+
                                                          | - flight_id    |
                                                          | - service_id   |
                                                          | - quantity     |
                                                          | - unit_price   |
                                                          | - line_total   |
                                                          +----------------+
                                                                   |
                                                                   v
                                                          +----------------+
                                                          | Invoice / Billing|
                                                          +----------------+
                                                          | - Aggregate    |
                                                          |   flight services|
                                                          | - Calculate total|
                                                          | - Generate invoice|
                                                          +----------------+
```

### **Step-by-Step Data Flow**

1. **Flight UI → flights table**
    
    - User fills flight info.
        
    - User selects a contract.
        
    - Flight is saved → `flights.contract_id` links flight to contract.
        
2. **Service UI → services + contract pricing**
    
    - User selects a flight → `flights.id`.
        
    - Load all services (`services` table).
        
    - Merge contract-specific pricing:
        
        - `additional_charges` (items/services)
            
        - `additional_stuff`
            
        - `aircraft_rates` (if flight has aircraft type)
            
    - Show user a table with pre-filled prices.
        
    - User adds selected services → saved in `invoice_services` table (or temporary `flight_services` table if you track pre-invoice).
        
3. **Invoice / Billing**
    
    - Aggregate services assigned to flight(s) → `invoice_services`.
        
    - Calculate `line_total = quantity * unit_price`.
        
    - Sum totals → store in `invoices.total_amount`.
        
    - Optionally, push back to database (`invoice_services.invoice_id` links line items to invoice).
        

---

### **Key Notes**

- Contract is the “pricing source.” Every flight inherits default or custom prices from its contract.
    
- Service UI allows **overrides**: user can adjust unit price or quantity before committing to invoice.
    
- `invoice_services` acts as a **bridge** between services and invoices.
    
- This approach keeps the UI modular: **Flight UI** → **Service UI** → **Invoice UI**.
    

---

If you want, I can make a **visual ERD-style diagram** that shows **tables, relationships, and UI connection points** in a single diagram, so you can give it directly to developers. That’s even easier to read than the text flow above.

---
```text
+---------------------+           +---------------------+
|      contracts      |           |      services       |
+---------------------+           +---------------------+
| id (PK)             |           | id (PK)             |
| contract_name       |           | name                |
| created_at          |           | default_price       |
| updated_at          |           | description         |
+---------------------+           | is_active           |
        ^                        | created_at          |
        |                        | updated_at          |
        | 1:M                    | deleted_at          |
+---------------------+           +---------------------+
|       flights       | <---------------------- Flight UI
+---------------------+        - Add/Edit flight
| id (PK)             |        - Select contract
| flight_name         |          (merges contract pricing)
| departure_time      |
| arrival_time        |
| contract_id (FK) ---|
| base_price          |
| status              |
| created_at          |
| updated_at          |
| deleted_at          |
+---------------------+
        |
        | 1:M
+---------------------+          +---------------------+
| flight_schedules    |          | flight_daily_counts |
+---------------------+          +---------------------+
| id (PK)             |          | id (PK)             |
| flight_id (FK) -----|----------| flight_id (FK)      |
| flight_number       |          | service_id (FK) ----|----+
| eta                 |          | activity_date       |    |
| etd                 |          | count               |    |
| days_of_week flags  |          | created_at          |    |
| routing             |          | updated_at          |    |
+---------------------+          +---------------------+    |
                                                           1:M
                                                           |
                                                   +---------------------+
                                                   |   flight_delays     |
                                                   +---------------------+
                                                   | id (PK)             |
                                                   | flight_id (FK)      |
                                                   | flight_daily_count_id|
                                                   | reason              |
                                                   | recorded_at         |
                                                   +---------------------+

        |
        | 1:M
+---------------------+ <---------------------- Service UI
|  flight_services    |        - Assign services to flight
+---------------------+        - Quantity / price adjustments
| id (PK)             |
| flight_id (FK) -----|---+
| service_id (FK) ----|---+
| quantity            |
| unit_price          |
| line_total          |
| description         |
| created_at          |
| updated_at          |
| deleted_at          |
+---------------------+
        |
        | M:1
+---------------------+ <---------------------- Invoice UI / Billing
| invoice_services    |        - Assign billed services to invoice
+---------------------+
| id (PK)             |
| invoice_id (FK) ----|---+
| flight_id (FK)      |   |
| service_id (FK) ----|---+
| quantity            |
| unit_price          |
| line_total          |
| description         |
| created_at          |
| updated_at          |
| deleted_at          |
+---------------------+
        |
        | M:1
+---------------------+
|      invoices       |
+---------------------+
| id (PK)             |
| invoice_number      |
| issue_date          |
| status              |
| total_amount        |
| created_at          |
| updated_at          |
| deleted_at          |
+---------------------+
```