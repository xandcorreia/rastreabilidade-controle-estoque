# Database Schema for Rastreabilidade Controle Estoque

## 1. Products Table
- **Table Name**: `products`
- **Fields**:
  - `id`: integer (Primary Key, Auto Increment)
  - `name`: varchar(255) (Not Null)
  - `description`: text (Null)
  - `price`: decimal(10, 2) (Not Null)
  - `created_at`: timestamp (Default: current timestamp)
  - `updated_at`: timestamp (Default: current timestamp on update)

## 2. Deposits Table
- **Table Name**: `deposits`
- **Fields**:
  - `id`: integer (Primary Key, Auto Increment)
  - `location`: varchar(255) (Not Null)
  - `capacity`: integer (Not Null)
  - `created_at`: timestamp (Default: current timestamp)
  - `updated_at`: timestamp (Default: current timestamp on update)

## 3. Batches Table
- **Table Name**: `batches`
- **Fields**:
  - `id`: integer (Primary Key, Auto Increment)
  - `product_id`: integer (Foreign Key references products(id)) (Not Null)
  - `quantity`: integer (Not Null)
  - `manufactured_at`: date (Not Null)
  - `expires_at`: date (Null)
  - `created_at`: timestamp (Default: current timestamp)
  - `updated_at`: timestamp (Default: current timestamp on update)

## 4. Stock Movements Table
- **Table Name**: `stock_movements`
- **Fields**:
  - `id`: integer (Primary Key, Auto Increment)
  - `batch_id`: integer (Foreign Key references batches(id)) (Not Null)
  - `deposit_id`: integer (Foreign Key references deposits(id)) (Not Null)
  - `movement_type`: enum('in', 'out') (Not Null)
  - `quantity`: integer (Not Null)
  - `movement_date`: timestamp (Default: current timestamp)

## 5. Deposit Balances Table
- **Table Name**: `deposit_balances`
- **Fields**:
  - `id`: integer (Primary Key, Auto Increment)
  - `deposit_id`: integer (Foreign Key references deposits(id)) (Not Null)
  - `product_id`: integer (Foreign Key references products(id)) (Not Null)
  - `balance`: integer (Not Null)
  - `last_updated`: timestamp (Default: current timestamp)

## Relationships
- **One-to-Many**: A product can have many batches.
- **Many-to-One**: A batch belongs to a single product.
- **Many-to-One**: A stock movement is associated with a single batch.
- **Many-to-One**: A stock movement is associated with a single deposit.
- **Many-to-One**: A deposit balance is related to a single deposit and a single product.