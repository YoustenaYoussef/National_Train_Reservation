🚆 National Train Reservation System
.NET 8 ASP.NET Core MVC SQL Server EF Core C#

A full-featured web application for train ticket search, booking, and management — built with ASP.NET Core MVC and SQL Server.

📋 Table of Contents
About the Project
Features
Tech Stack
Database Schema
Project Structure
Getting Started
Prerequisites
Installation
Database Setup
Usage
User Roles
Contributing
License
🎯 About the Project
The National Train Reservation System is a web-based platform that enables passengers to search for available train journeys, book tickets online, make payments, and manage their reservations — all from a single, user-friendly interface.

Administrators have a dedicated panel to manage trains, add available seats, and oversee the entire fleet and booking data.

✨ Features
👤 User Features
Register & Sign In — Secure account creation with validation (email, Egyptian national ID, phone number, strong password)
Profile Photo Upload — Users can upload a profile picture (.jpg/.jpeg)
Search Trains — Filter by departure station, destination, travel date, and seat class
Book a Ticket — Automatically assigns an available car and seat number
Online Payment — Credit/debit card payment with full validation (16-digit card number, CVV, expiry date)
View My Tickets — List all booked tickets at a glance
Cancel a Ticket — Cancel any reservation, which automatically frees the seat back to the pool
Change Password — Secure password update with old-password verification
Delete Account — Permanently remove the account from the system
Suggestions & Complaints — Submit feedback directly linked to the user's profile
🛠️ Admin Features
Add New Train Journey — Define train number, stations, class, stops, price, departure, and arrival times
Manage Trains — View and delete scheduled journeys
Add Available Tickets/Seats — Assign car and seat numbers to a specific journey
🔒 Security
Cookie-based Authentication — Session persists across requests with a 60-minute idle timeout
SHA-256 Password Hashing — Passwords are never stored in plain text
Input Validation — Server-side regex validation on all critical fields
🛠️ Tech Stack
Layer	Technology
Framework	ASP.NET Core 8.0 MVC
Language	C#
ORM	Entity Framework Core 7.0
Database	Microsoft SQL Server
Authentication	ASP.NET Core Cookie Authentication
Session	ASP.NET Core Session Middleware
Serialization	Newtonsoft.Json
Frontend	Razor Views (.cshtml), HTML, CSS, JavaScript
🗄️ Database Schema
The system uses 6 database entities with the following relationships:

Users ──< Tickets
Users ──< Payment
Users ──< Suggestions_Complaints
Trains ──< AvailableTickets
Trains ──< Tickets
Entity	Key Fields
Users	User_ID, National_Pass_Number, Name, Email, Password (hashed), Phone, Gender, Type
Trains	Journey_ID, TrainNumber, Launching_Station, Destination, Date, Time, Price, Class, Stoppages
Tickets	ID, Pickup_Station, Destination, Date, Time, Seat, Car, Class, Price → FK Users, Trains
AvailableTickets	ID, Journey_ID, carNumber, seatNumber, IsBooked → FK Trains
Payment	ID, Card_Number, CVV, Expiration_date, Card_Owner_name → FK Users
Suggestions_Complaints	ID, Message_Type (Suggestion/Complaint), Subject, Details → FK Users
📁 Project Structure
National_Train_Reservation/
│
├── Controllers/
│   ├── HomeController.cs          # Landing page
│   ├── UsersController.cs         # Auth, profile, admin train/ticket management
│   └── TicketsController.cs       # Search, booking, payment, cancellation
│
├── Models/
│   ├── Users.cs
│   ├── Trains.cs
│   ├── Tickets.cs
│   ├── AvailableTickets.cs
│   ├── Payment.cs
│   └── Suggestions_Complains.cs
│
├── Data/
│   └── ApplicationDBcontext.cs    # EF Core DbContext
│
├── Views/
│   ├── Home/
│   ├── Users/                     # SignUp, SignIn, Settings, AddTrain, etc.
│   ├── Tickets/                   # Search, Book, Payment, ViewTickets, etc.
│   └── Shared/                    # Layout, error pages
│
├── Migrations/                    # EF Core migration history
├── wwwroot/                       # Static files (CSS, JS, images)
├── Program.cs                     # App entry point & service configuration
└── appsettings.json               # Connection strings & configuration
🚀 Getting Started
Prerequisites
Make sure you have the following installed:

.NET 8 SDK
SQL Server (Express or Developer edition)
Visual Studio 2022 (recommended) or VS Code with C# extension
Installation
Clone the repository:

git clone https://github.com/your-username/National_Train_Reservation.git
cd National_Train_Reservation/National_Train_Reservation
Restore NuGet packages:

dotnet restore
Database Setup
Update the connection string in appsettings.json:

{
  "ConnectionStrings": {
    "myConnection": "Server=YOUR_SERVER_NAME;Database=NationalTrainDB;Trusted_Connection=True;TrustServerCertificate=True;"
  }
}
Apply database migrations:

dotnet ef database update
Run the application:

dotnet run
Open your browser and navigate to https://localhost:5001 (or the port shown in the terminal).

📖 Usage
First-Time Setup (Admin)
After running the app and creating your first account:

Manually set your user type to "admin" in the database.
Log in and navigate to Add Train to schedule your first journey.
Use Add Ticket to assign available seats (car + seat number) to the journey.
Passenger Booking Flow
Register / Sign In
       ↓
Search for a train (From → To, Date, Class)
       ↓
Select an available journey
       ↓
Book Ticket (auto-assigned seat & car)
       ↓
Enter payment details
       ↓
Ticket confirmed ✅
👥 User Roles
Role	Capabilities
User	Register, sign in, search trains, book & cancel tickets, view history, submit feedback, change password, delete account
Admin	All user capabilities + add/delete train journeys, add available seats/tickets
User roles are stored in the type column of the Users table ("user" / "admin").

🤝 Contributing
Contributions are welcome! Please follow these steps:

Fork the repository
Create your feature branch: git checkout -b feature/AmazingFeature
Commit your changes: git commit -m 'Add some AmazingFeature'
Push to the branch: git push origin feature/AmazingFeature
Open a Pull Request
Made with ❤️ using ASP.NET Core MVC
