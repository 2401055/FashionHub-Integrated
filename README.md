# FashionHub - E-Commerce Platform

A complete e-commerce platform built with Flask (Backend) and HTML/CSS/JavaScript (Frontend).

## Features

- User authentication with JWT tokens
- Product catalog with categories
- Shopping cart functionality
- Order management
- User profile management
- Search and filtering capabilities

## Project Structure

```
FashionHub/
├── app.py                 # Flask backend application
├── index.html             # Frontend (HTML + CSS + JS)
├── database.sql           # Database schema
├── requirements.txt       # Python dependencies
├── Procfile              # Render deployment configuration
├── render.yaml           # Render service configuration
├── runtime.txt           # Python version specification
├── .env.example          # Environment variables template
└── README.md             # This file
```

## Local Development

### Prerequisites
- Python 3.11+
- pip

### Installation

1. Clone the repository:
```bash
git clone https://github.com/2401055/FashionHub-Integrated.git
cd FashionHub-Integrated
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run the application:
```bash
python app.py
```

The application will be available at `http://localhost:10000`

## Deployment to Render

### Step 1: Push to GitHub
Make sure your code is pushed to GitHub:
```bash
git add .
git commit -m "Ready for Render deployment"
git push origin main
```

### Step 2: Connect to Render

1. Go to [render.com](https://render.com)
2. Sign up or log in with your GitHub account
3. Click "New +" → "Web Service"
4. Select your GitHub repository (`FashionHub-Integrated`)
5. Fill in the deployment settings:
   - **Name**: fashionhub
   - **Environment**: Python 3
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn app:app`
   - **Plan**: Free (or paid if you need better performance)

### Step 3: Environment Variables
Add these environment variables in Render dashboard:
- `FLASK_ENV`: `production`
- `SECRET_KEY`: Generate a strong secret key (e.g., using `python -c "import secrets; print(secrets.token_hex(32))"`)

### Step 4: Deploy
Click "Create Web Service" and Render will automatically:
1. Install dependencies from `requirements.txt`
2. Initialize the database
3. Start the application with gunicorn

Your app will be live at: `https://fashionhub.onrender.com` (or similar URL)

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user

### Products
- `GET /api/products` - Get all products
- `GET /api/products/<id>` - Get single product
- `GET /api/products/search?q=<query>` - Search products
- `GET /api/categories` - Get all categories

### Cart
- `GET /api/cart` - Get cart contents
- `POST /api/cart` - Add item to cart
- `DELETE /api/cart/<product_id>` - Remove item from cart
- `DELETE /api/cart` - Clear cart

### Orders
- `POST /api/orders` - Create order
- `GET /api/orders` - Get user orders
- `GET /api/orders/<order_id>` - Get order details

### Users
- `GET /api/users/<user_id>` - Get user profile
- `PUT /api/users/<user_id>` - Update user profile

## Database

The application uses SQLite with the following tables:
- `users` - User accounts
- `categories` - Product categories
- `products` - Product listings
- `orders` - Customer orders
- `order_items` - Order line items

Database is automatically initialized on first run.

## Technology Stack

**Backend:**
- Flask 2.3.3
- Flask-CORS 4.0.0
- PyJWT 2.8.0
- Werkzeug 2.3.7
- Gunicorn 21.2.0

**Frontend:**
- HTML5
- CSS3
- JavaScript (Vanilla)

**Database:**
- SQLite3

## Environment Variables

Create a `.env` file based on `.env.example`:

```
FLASK_ENV=production
SECRET_KEY=your-secret-key-here
DATABASE_PATH=fashionhub.db
PORT=10000
```

## Troubleshooting

### Database Issues
If the database doesn't initialize:
1. Delete `fashionhub.db` file
2. Restart the application
3. The database will be recreated automatically

### Port Already in Use
If port 10000 is already in use:
```bash
PORT=5000 python app.py
```

### CORS Issues
If you get CORS errors, ensure the frontend is making requests to the same domain or the API is properly configured with CORS headers.

## License

MIT License

## Support

For issues or questions, please open an issue on GitHub.
