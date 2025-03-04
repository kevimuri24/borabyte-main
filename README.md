# Furniture E-commerce Platform Architecture

## System Overview

This architecture outlines a complete e-commerce solution for a furniture store with:
- **Frontend**: React with Tailwind CSS
- **Backend**: Flask Python framework
- **Database**: PostgreSQL (for relational data), Redis (for caching)
- **Payment Processing**: Stripe integration
- **Authentication**: JWT-based auth system

## 1. Frontend Architecture (React + Tailwind CSS)

### Core Components
- **Layout Components**: Header, Footer, Navigation
- **Product Components**: ProductCard, ProductGrid, ProductDetail, ProductGallery
- **Shopping Components**: Cart, Checkout, OrderSummary
- **User Components**: Login, Register, UserProfile, OrderHistory
- **UI Components**: Button, Modal, Toast, Pagination, Ratings

### Pages
- Home Page
- Product Listing/Category Pages
- Product Detail Page
- Cart Page
- Checkout Process Pages
- User Account Pages
- About/Contact Pages
- Blog Section

### State Management
- React Context API for global state
- Redux for complex state management (optional)
- React Query for server-state management

## 2. Backend Architecture (Flask)

### API Endpoints

#### Products
- `GET /api/products` - List all products with pagination
- `GET /api/products/{id}` - Get product details
- `GET /api/categories` - List all categories
- `GET /api/categories/{id}/products` - List products by category
- `POST /api/products` - Add new product (admin)
- `PUT /api/products/{id}` - Update product (admin)
- `DELETE /api/products/{id}` - Delete product (admin)

#### Users/Auth
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/profile` - Get user profile
- `PUT /api/auth/profile` - Update user profile
- `GET /api/auth/orders` - Get user orders

#### Cart & Orders
- `GET /api/cart` - Get cart contents
- `POST /api/cart` - Add item to cart
- `PUT /api/cart/{id}` - Update cart item
- `DELETE /api/cart/{id}` - Remove cart item
- `POST /api/orders` - Create order
- `GET /api/orders/{id}` - Get order details

#### Payment
- `POST /api/payment/create-intent` - Create payment intent (Stripe)
- `POST /api/payment/webhook` - Handle Stripe webhooks

#### Admin
- `GET /api/admin/dashboard` - Admin dashboard data
- `GET /api/admin/orders` - List all orders
- `PUT /api/admin/orders/{id}` - Update order status

### Database Models
- User
- Product
- Category
- Cart
- CartItem
- Order
- OrderItem
- Payment
- Review

## 3. Database Schema

### Users Table
- id (PK)
- email
- password_hash
- first_name
- last_name
- address
- phone
- created_at
- is_admin

### Products Table
- id (PK)
- name
- description
- price
- discount_price
- category_id (FK)
- stock
- images (JSON)
- specifications (JSON)
- is_featured
- created_at

### Categories Table
- id (PK)
- name
- description
- image
- parent_id (FK, self-referential)

### Orders Table
- id (PK)
- user_id (FK)
- total_amount
- status (enum: pending, paid, shipped, delivered, canceled)
- shipping_address
- shipping_method
- payment_id
- created_at

### OrderItems Table
- id (PK)
- order_id (FK)
- product_id (FK)
- quantity
- price

### Reviews Table
- id (PK)
- product_id (FK)
- user_id (FK)
- rating
- comment
- created_at

## 4. Integration Points

### Payment Processing (Stripe)
- Payment intent creation
- Payment confirmation
- Webhook handling

### Email Service (SendGrid/Mailgun)
- Order confirmations
- Shipping updates
- Password resets
- Marketing emails

### Image Storage (AWS S3)
- Product images
- User avatars

## 5. Deployment Architecture
- Frontend: Vercel/Netlify
- Backend: Docker containers on AWS/GCP/Azure
- Database: Managed database service
- CI/CD: GitHub Actions

## 6. Security Considerations
- HTTPS everywhere
- JWT with proper expiration
- Input validation
- CSRF protection
- Rate limiting
- SQL injection prevention
- XSS prevention
