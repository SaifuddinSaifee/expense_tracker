# Notes

## Database schema

Database to handle the basic functionalities like tracking balance, expenses, earnings, and generating transaction statements. Here's a proposed schema:

### Tables and Attributes

1. **Users**
   - `user_id` (Primary Key): Unique identifier for each user.
   - `username`: User's name.
   - `email`: User's email address.
   - `password`: Password for security.

2. **Transactions**
   - `transaction_id` (Primary Key): Unique identifier for each transaction.
   - `user_id` (Foreign Key): Identifier linking to the Users table.
   - `type`: Type of transaction (expense or income).
   - `amount`: Amount of the transaction.
   - `category_id` (Foreign Key): Identifier linking to the Categories table.
   - `date`: Date of the transaction.
   - `description`: A brief description of the transaction.
   - `is_recurring`: Flag to indicate if it's a recurring transaction.

3. **Categories**
   - `category_id` (Primary Key): Unique identifier for each category.
   - `name`: Name of the category (e.g., Groceries, Utilities, Salary).

4. **Balances**
   - `balance_id` (Primary Key): Unique identifier for each balance record.
   - `user_id` (Foreign Key): Identifier linking to the Users table.
   - `current_balance`: Current balance of the user.
   - `last_updated`: Timestamp of the last update to the balance.

### Relationships

1. **Users to Transactions**: One-to-Many
   - Each user can have multiple transactions, but each transaction belongs to only one user.

2. **Transactions to Categories**: Many-to-One
   - Each transaction is associated with one category, but a category can be associated with multiple transactions.

3. **Users to Balances**: One-to-One
   - Each user has one balance record. This record is updated rather than having multiple entries per user.

### Extras

- **Normalization**: The schema is normalized to reduce redundancy (e.g., categories are separated from transactions).
- **Security**: Passwords should never be stored as plain text; hence, `password_hash` is used.
- **Date Handling**: The `date` in Transactions and `last_updated` in Balances should be stored in a standardized format, such as ISO 8601.
- **Recurring Transactions**: The `is_recurring` flag in Transactions can be used to identify and handle recurring expenses or incomes.
- **Scalability**: While the schema is simple, it's designed to be scalable and can handle additional features if needed in the future.

This schema provides a comprehensive foundation for the expense tracker app, ensuring that all necessary data is captured and organized efficiently.