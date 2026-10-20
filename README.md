# StockPilot - Smart Inventory Management System

StockPilot is a product inventory management application with a FastAPI backend and a React frontend. It provides a web interface and REST API for viewing, adding, editing, and deleting products.

## Features

- View the product inventory
- Add products with a name, description, price, and quantity
- Edit and delete products
- Run the API with in-memory data or use the PostgreSQL-backed implementation
- Explore the API through FastAPI's interactive documentation

## Project structure

```text
.
|-- frontend/          # React application
|-- without_using_db/  # FastAPI API using in-memory product data
|-- with_using_db/     # FastAPI API backed by PostgreSQL
|-- requirements.txt   # Python dependencies
```

## Requirements

- Python 3.10 or newer
- Node.js and npm
- PostgreSQL only if using the database-backed API

## Run the API without a database

From the project root, create and activate a virtual environment, then install the Python dependencies:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Start the API:

```powershell
uvicorn without_using_db.main:app --reload
```

The API will be available at <http://localhost:8000>. Interactive API documentation is at <http://localhost:8000/docs>.

This implementation keeps products in memory, so changes are lost when the server restarts.

## Run the frontend

Open a second terminal:

```powershell
cd frontend
npm install
npm start
```

The React application will be available at <http://localhost:3000>. Its development server proxies API requests to <http://localhost:8000>.

## Run the API with PostgreSQL

The database-backed implementation is in `with_using_db/`. Before starting it:

1. Create a PostgreSQL database.
2. Configure the database connection URL in `with_using_db/database.py`. Do not commit database passwords or other secrets.
3. Install the SQLAlchemy package and a PostgreSQL driver compatible with your connection URL if they are not already installed.
4. From the project root, start the API:

   ```powershell
   uvicorn with_using_db.main:app --reload
   ```

On startup, the API creates the product table and inserts sample products if the table is empty.

## API endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/products/` | List products |
| `GET` | `/products/{product_id}` | Get a product by ID |
| `POST` | `/products/` | Create a product |
| `PUT` | `/products/{product_id}` | Update a product |
| `DELETE` | `/products/{product_id}` | Delete a product |

Example product JSON:

```json
{
  "id": 5,
  "name": "Notebook",
  "description": "A ruled notebook",
  "price": 4.99,
  "quantity": 25
}
```

## Notes

- The API currently does not include authentication.
- Use the in-memory implementation for a quick local demo; use PostgreSQL when persistent storage is needed.
