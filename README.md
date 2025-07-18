# 🧾 Personal CRM — SvelteKit + Appwrite Functions

A modern personal CRM application built with **SvelteKit** and **Appwrite Functions**. Features a beautiful spreadsheet-like interface for managing contacts with real-time CRUD operations. No authentication required — perfect for personal use.

---

## 🚀 Tech Stack

- **Frontend:** SvelteKit with modern CSS
- **Backend:** Appwrite Functions (Node.js runtime)
- **Database:** Appwrite Database
- **Deployment:** Appwrite Cloud

---

## 📦 Features

- ✅ Spreadsheet-like interface for contact management
- ✅ Real-time CRUD operations (Create, Read, Update, Delete)
- ✅ Bulk editing capabilities
- ✅ Modern responsive design with gradient backgrounds
- ✅ No authentication required (personal use)
- ✅ CSV import/export support

---

## 📁 Project Structure

```
/src
├── /routes
│   ├── +page.svelte          # Main UI with spreadsheet interface
│   └── +layout.js           # Layout configuration
├── /lib
│   └── appwrite.js          # Appwrite client configuration
└── app.css                  # Global styles and modern UI
/functions
└── /database-operations     # Appwrite Function for CRUD operations
    ├── src/
    │   ├── main.js          # Function entry point
    │   └── db.js            # Database operations
    └── package.json         # Function dependencies
```

---

## 🛠️ Appwrite Setup

### 1. Create Project & Database
1. **Create a project** on [Appwrite Console](https://cloud.appwrite.io)
2. **Create a Database** with ID: `db`
3. **Create a Collection** with ID: `crm` and these attributes:
   - `name` → String (required, 255 chars)
   - `email` → String (required, 255 chars)
   - `phone` → String (optional, 50 chars)
   - `notes` → String (optional, 1000 chars)

### 2. Deploy Appwrite Function
```bash
# Install Appwrite CLI
npm install -g appwrite-cli

# Login to Appwrite
appwrite login

# Deploy the function
appwrite deploy function
```

---

## 🔐 Environment Setup

### Frontend Environment
Create a `.env` file in the project root:

```env
PUBLIC_APPWRITE_ENDPOINT=https://region.cloud.appwrite.io/v1
PUBLIC_APPWRITE_PROJECT_ID=your_project_id
PUBLIC_APPWRITE_FUNCTION_URL=https://654321.fra.appwrite.network
```

### Function Environment
The function environment is configured automatically through the Appwrite console. Required variables:
- `CORS_ORIGIN`
- `APPWRITE_DATABASE_ID=db`
- `APPWRITE_COLLECTION_ID=crm`

---

## 🧪 Development

```bash
# Install dependencies
npm install

# Copy the environment template
cp .env.example .env

# Edit .env with your Appwrite project details
# Then start the development server
npm run dev
```

The app will be available at `http://localhost:5173`

### Development with Functions

For local function development:

```bash
# Navigate to the function directory
cd functions/database-operations

# Install function dependencies
npm install

# Test the function locally (optional)
appwrite run functions
```

---

## 🌐 Deployment

### Frontend Deployment

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

Deploy to any static hosting provider (Vercel, Netlify, etc.) or use Appwrite's hosting feature.

### Function Deployment

Functions are deployed automatically when you run:

```bash
appwrite push function
```

The function will be available at your Appwrite project's function URL.

---

## 📖 API Documentation

The Appwrite Function provides the following endpoints:

### GET `/contacts`
Returns all contacts from the database.

**Response:**
```json
{
  "total": 1,
  "documents": [
    {
      "$id": "contact_id",
      "name": "John Doe",
      "email": "john@example.com",
      "phone": "+1-555-0123",
      "notes": "Important client"
    }
  ]
}
```

### PUT `/contacts`
Creates new contacts or updates existing ones (bulk upsert).

**Request Body:**
```json
{
  "contacts": [
    {
      "name": "Jane Smith",
      "email": "jane@example.com",
      "phone": "+1-555-0124",
      "notes": "New prospect"
    }
  ]
}
```

### DELETE `/contacts?id=<id>`
Deletes contact by their ID in the query.

### DELETE `/contacts`
Deletes all contacts.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request
