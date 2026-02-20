CreditCare
CreditCare — Gestor de pagos de tarjeta de crédito para usuarios particulares, diseñado como proyecto de portafolio para demostrar habilidades en frontend, backend, arquitectura y seguridad. La aplicación permite registrar tarjetas como metas, planear y gestionar pagos, recibir recordatorios y simular escenarios de amortización sin procesar pagos reales ni almacenar datos completos de tarjeta.

Visión y características principales
Visión
Proveer una aplicación web responsiva que ayude a usuarios a evitar cargos por mora y optimizar pagos mediante recordatorios, simulaciones y un historial claro de amortización.
Características principales
- Autenticación con email y contraseña y tokens JWT.
- Gestión de tarjetas meta: emisor, últimos 4 dígitos, límite, saldo, APR, día de corte y día de pago.
- Dashboard con resumen de saldos, próximos vencimientos y gráfico simple.
- Recordatorios configurables por email y notificaciones in-app.
- Simulador de pago que calcula meses, intereses y total pagado según distintos escenarios.
- Historial y exportación CSV sin datos sensibles.
- Privacidad: no almacenar PAN ni CVV; TLS obligatorio en producción.

Tech Stack y arquitectura
Stack recomendado
- Frontend: React + TypeScript; Vite; Tailwind CSS.
- Backend: Node.js + TypeScript (NestJS o Express) o Python (FastAPI).
- Base de datos: PostgreSQL.
- Autenticación: JWT con refresh tokens; opción de Auth0 o NextAuth.
- Workers: Redis + Bull o similar para tareas asíncronas y envío de emails.
- Observabilidad: Sentry para errores; logging estructurado.
Arquitectura resumida
- Frontend consume API REST autenticada.
- Backend gestiona lógica financiera, validaciones y programación de recordatorios.
- DB relacional para consistencia en transacciones y auditoría.
- Worker para envíos de email y tareas programadas.
- CI/CD con GitHub Actions para lint, tests y despliegue.

Instalación y ejecución local
Requisitos
- Node.js 18+ o Python 3.10+ según stack elegido.
- PostgreSQL 13+.
- Git.
Clonar repositorio
git clone https://github.com/tu-usuario/creditcare.git
cd creditcare


Backend instalación y ejecución
cd backend
cp .env.example .env
# editar .env con credenciales
npm install
npm run migrate
npm run dev


Frontend instalación y ejecución
cd frontend
cp .env.example .env
# editar .env con URL de la API
npm install
npm run dev


Comandos útiles
- Ejecutar tests backend:
cd backend
npm test


- Ejecutar tests frontend:
cd frontend
npm test


Variables de entorno esenciales
- DATABASE_URL — URL de conexión a PostgreSQL.
- JWT_SECRET — secreto para firmar tokens.
- JWT_REFRESH_SECRET — secreto para refresh tokens.
- SMTP_HOST, SMTP_PORT, SMTP_USER, SMTP_PASS — para envío de emails.
- FRONTEND_URL — URL pública del frontend para enlaces en emails.

API Endpoints y reglas de negocio
Endpoints principales
- POST /api/auth/register — registrar usuario.
- POST /api/auth/login — autenticar y obtener JWT.
- GET /api/cards — listar tarjetas del usuario.
- POST /api/cards — crear tarjeta meta.
- PUT /api/cards/:id — actualizar tarjeta.
- DELETE /api/cards/:id — eliminar tarjeta.
- POST /api/cards/:id/payments — registrar pago.
- GET /api/cards/:id/history — historial de pagos.
- POST /api/simulate — simulador de pago.
- GET /api/reminders — listar recordatorios.
- POST /api/export/:cardId — generar CSV.
Modelo de datos clave
- User: id; email; hashed_password; timezone; preferences.
- CardMeta: id; user_id; issuer; last4; limit; balance; apr; cut_day; due_day.
- Payment: id; card_id; amount; date; note.
- Reminder: id; card_id; user_id; days_before; channel.
Reglas de negocio
- No almacenar PAN ni CVV; solo last4 y metadatos.
- Validaciones: apr entre 0 y 100; last4 exactamente 4 dígitos; balance >= 0.
- Cálculo de fechas: usar la zona horaria del usuario para calcular due_date y programar recordatorios.
- Registro de pagos: crear Payment decrementa CardMeta.balance y añade entrada en historial.
- Simulador: documentar fórmula usada y cubrir con tests unitarios casos de borde.

Seguridad privacidad pruebas y cumplimiento
Seguridad
- TLS obligatorio en producción.
- Hash de contraseñas con bcrypt o Argon2.
- JWT con expiración y refresh tokens.
- Rate limiting en endpoints de autenticación.
- Filtrado de logs para evitar exponer datos sensibles.
Privacidad
- Política de privacidad clara y consentimiento explícito para notificaciones.
- Retención mínima de logs que contengan metadatos de usuario.
Pruebas
- Unit tests para lógica financiera y simulador.
- Integration tests para endpoints críticos.
- E2E tests para flujos: registro, agregar tarjeta, simular, registrar pago.
- Objetivo de cobertura: > 70% en lógica financiera crítica.
Cumplimiento
- Mantener la app fuera del alcance PCI DSS evitando procesar o almacenar CHD.
- Si se integra con proveedores de pago, usar tokenización y delegar cumplimiento.

Despliegue CI CD contribución y licencia
CI CD
- GitHub Actions para lint, tests y despliegue automático.
- Despliegue recomendado: Vercel para frontend; Render, Railway o Heroku para backend y base de datos.
- Gestionar secrets en GitHub y en el proveedor de hosting.
Cómo contribuir
- Fork del repo, crear branch feature/tu-feature, abrir PR con descripción y tests.
- Mantener commits pequeños y descriptivos.
- Añadir pruebas para cambios en lógica financiera.
Licencia
- Este proyecto está Licensed under the Apache License 2.0. Consulta el archivo LICENSE en la raíz del repositorio para el texto completo.

Archivos incluidos en el repositorio
- README.md (este documento)
- LICENSE (Apache 2.0)
- backend/ con código, migraciones y tests
- frontend/ con UI y tests
- .github/workflows/ con pipelines CI
- .env.example con variables esenciales
