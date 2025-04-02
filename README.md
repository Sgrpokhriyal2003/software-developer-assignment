# software-developer-assignment
# Load Management System API

A RESTful API for managing load bookings and transportation logistics. This system allows shippers to post loads and transporters to book them.

## Setup Instructions

1. Clone the repository:

git clone <repository-url>
cd <project-directory>


2. Install dependencies:

npm install


4. Start the development server:

npm run dev


For production:

npm start


## API Documentation

### Load Management

#### Create Load
- **POST** `/load`
- Creates a new load posting
- Required fields:
  - shipperId
  - facility.loadingPoint
  - facility.unloadingPoint
  - facility.loadingDate (ISO8601)
  - facility.unloadingDate (ISO8601)
  - productType
  - truckType
  - noOfTrucks (min: 1)
  - weight (min: 0)
  - status (optional: POSTED, BOOKED, CANCELLED)

#### Get All Loads
- **GET** `/load`
- Retrieves all load postings

#### Get Load by ID
- **GET** `/load/:id`
- Retrieves a specific load posting

#### Update Load
- **PUT** `/load/:id`
- Updates an existing load posting
- Same validation as create load

#### Delete Load
- **DELETE** `/load/:id`
- Deletes a load posting

### Booking Management

#### Create Booking
- **POST** `/booking`
- Creates a new booking for a load
- Required fields:
  - loadId
  - transporterId
  - proposedRate (min: 0)
  - status (optional: PENDING, ACCEPTED, REJECTED)

#### Get All Bookings
- **GET** `/booking`
- Retrieves all bookings

#### Get Booking by ID
- **GET** `/booking/:id`
- Retrieves a specific booking

#### Update Booking Status
- **PUT** `/booking/:id/status`
- Updates the status of a booking
- Required field:
  - status (ACCEPTED or REJECTED)

#### Delete Booking
- **DELETE** `/booking/:id`
- Deletes a booking

## Logging

The application uses Winston for logging with the following configuration:
- Error logs are stored in 'error.log'
- Combined logs are stored in 'combined.log'
- Console logging is enabled in development mode

## Error Handling

The application includes a global error handling middleware that:
- Logs errors using Winston
- Returns a 500 status code with a generic error message
- Preserves the error stack trace in logs

## Development

To run the application in development mode with auto-reload:

npm run dev

## Production

For production deployment:
1. Set NODE_ENV=production in .env
2. Run the application using:

npm start

