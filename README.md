# CreditCare

**CreditCare** — Credit card payment manager for individual users, designed as a portfolio project to demonstrate skills in frontend, backend, architecture, and security.  

The application allows users to register cards (metadata only), plan and manage payments, receive reminders, and simulate amortization scenarios without processing real payments or storing full card data.

---

##  Key Features
- Authentication with email and password (JWT).
- Card metadata management: issuer, last 4 digits, limit, balance, APR, cut-off day, and due date.
- Dashboard with balance summary and upcoming due dates.
- Configurable reminders via email and in-app notifications.
- Payment simulator calculating months, interest, and total paid.
- Payment history and CSV export without sensitive data.
- Privacy: no PAN or CVV storage; TLS required in production.

---

## Tech Stack
- **Frontend**: React + TypeScript, Vite, Tailwind CSS.
- **Backend**: Flask (Python) + SQLAlchemy + Marshmallow.
- **Database**: PostgreSQL.
- **Authentication**: JWT with refresh tokens.
- **Workers**: Celery + Redis for asynchronous tasks.
- **CI/CD**: GitHub Actions.
- **Observability**: Sentry for error tracking; structured logging.

---

##  Installation and Local Setup
### Requirements
- Python 3.10+
- Node.js 18+
- PostgreSQL 13+
- Git

### Clone repository
```bash
git clone https://github.com/your-username/creditcare.git
cd creditcare


**### BACKEND**
cd backend
cp .env.example .env
pip install -r requirements.txt
flask db upgrade
flask run

**###Frontend**
cd frontend
cp .env.example .env
npm install
npm run dev

**###Environment Variables**
"""Configure a .env file in each service (backend/frontend).
Example in backend/.env.example:"""

DATABASE_URL=postgres://user:password@localhost:5432/creditcare_dev
JWT_SECRET=replace_with_strong_secret
SMTP_HOST=smtp.example.com
SMTP_USER=your_user
SMTP_PASS=your_password
FRONTEND_URL=http://localhost:3000

<<<<<<< HEAD
=======


>>>>>>> 0bf4863286f4305f6ca19077dc81b9e1de8ffdce
