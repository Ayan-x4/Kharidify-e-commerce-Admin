# Ecommerce Admin Dashboard

The Admin application is the management dashboard for the ecommerce project. It allows an administrator to authenticate, add products, view the product catalog, and remove products.

The dashboard communicates with the project [Backend](../Backend) API.

## Features

- Admin login using the backend admin authentication endpoint
- Persistent admin session token stored in `localStorage`
- Product creation with:
  - Product name and description
  - Category and subcategory
  - Price
  - Product sizes
  - Bestseller flag
  - Up to four product images
- Product list with images, names, categories, and prices
- Product deletion
- Toast notifications for successful and failed requests
- Responsive sidebar navigation

The Orders page is currently included in the navigation but does not yet contain order-management functionality.

## Tech stack

- React 19
- Vite
- React Router
- Tailwind CSS
- Axios
- React Toastify

## Project structure

```text
Admin/
├── public/                  # Public static files
├── src/
│   ├── assets/              # Images and dashboard assets
│   ├── components/
│   │   ├── Login.jsx        # Admin login form
│   │   ├── Navbar.jsx       # Header and logout action
│   │   └── Sidebar.jsx      # Dashboard navigation
│   ├── pages/
│   │   ├── Add.jsx          # Add product form
│   │   ├── List.jsx         # Product list and deletion
│   │   └── Orders.jsx       # Orders page placeholder
│   ├── App.jsx              # Authentication gate and routes
│   ├── index.css            # Global styles and Tailwind import
│   └── main.jsx             # React entry point
├── .env                    # Local environment variables
├── package.json
└── vite.config.js
```

## Requirements

- Node.js and npm
- The ecommerce backend running locally or at a reachable URL

## Environment variables

Create an `.env` file in the `Admin` directory and set the backend URL:

```env
VITE_BACKEND_URL=http://localhost:4000
```

The value is exposed to the Vite client through `import.meta.env.VITE_BACKEND_URL` and is used by the Admin app for API requests.

## Installation

From the `Admin` directory, install the dependencies:

```bash
npm install
```

## Development

Start the Vite development server:

```bash
npm run dev
```

The Admin app is configured to run on:

```text
http://localhost:5174
```

The backend should be running separately, normally on `http://localhost:4000`.

## Available scripts

```bash
npm run dev       # Start the development server
npm run build     # Create a production build
npm run lint      # Run ESLint
npm run preview   # Preview the production build locally
```

## Dashboard routes

| Route | Purpose |
| --- | --- |
| `/add` | Add a new product |
| `/list` | View and remove products |
| `/orders` | Orders page placeholder |

The application displays the login screen when no admin token is available. After successful authentication, the dashboard layout, navbar, sidebar, and routes are shown.

## Backend API integration

The Admin app currently uses these backend endpoints:

| Method | Endpoint | Used for |
| --- | --- | --- |
| `POST` | `/api/user/admin` | Admin login |
| `POST` | `/api/product/add` | Add a product with multipart form data |
| `GET` | `/api/product/list` | Load all products |
| `POST` | `/api/product/remove` | Delete a product |

Authenticated product operations send the admin token in the request's `token` header.

## Related application

The Admin dashboard is part of the larger ecommerce project:

- `../Backend` — Express API, MongoDB, authentication, products, carts, and orders
- `../Frontend` — Customer-facing ecommerce storefront
