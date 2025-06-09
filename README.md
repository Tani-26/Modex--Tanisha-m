# Ticket Booking System

A scalable ticket booking system built with Node.js, Express.js, and PostgreSQL that handles concurrent booking requests efficiently.

## Features

- Show/Trip Management
- Concurrent Seat Booking
- Booking Status Management
- Automatic Booking Expiry
- High Concurrency Handling

## Prerequisites

- Node.js (v14 or higher)
- PostgreSQL (v12 or higher)
- npm or yarn

## Setup Instructions

1. Clone the repository:
```bash
git clone <repository-url>
cd ticket-booking-system
```

2. Install dependencies:
```bash
npm install
```

3. Create a PostgreSQL database named `ticket_booking`

4. Copy `.env.example` to `.env` and update the configuration:
```bash
cp .env.example .env
```

5. Run database migrations:
```bash
npm run migrate
```

6. Start the server:
```bash
# Development
npm run dev

# Production
npm start
```

## API Documentation

The API documentation is available at `/api-docs` when the server is running.

### Main Endpoints

#### Shows/Trips
- `GET /api/shows` - List all available shows
- `POST /api/shows` - Create a new show (Admin only)
- `GET /api/shows/:id` - Get show details

#### Bookings
- `POST /api/bookings` - Create a new booking
- `GET /api/bookings/:id` - Get booking status
- `GET /api/bookings/user/:userId` - Get user's bookings

## Concurrency Handling

The system uses PostgreSQL transactions and row-level locking to ensure data consistency during concurrent booking operations. Each booking attempt is wrapped in a transaction that:

1. Checks seat availability
2. Locks the selected seats
3. Creates the booking
4. Updates seat status

## Technical Architecture

The system is designed with scalability in mind:

- **Database**: PostgreSQL with row-level locking
- **Caching**: Redis for frequently accessed data
- **Message Queue**: RabbitMQ for handling booking requests
- **Load Balancing**: Nginx for request distribution
- **Monitoring**: Prometheus and Grafana

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT 