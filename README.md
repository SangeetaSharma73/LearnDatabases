# Interview Question and Solution

What are REST APIs?
REST (Representational State Transfer) APIs are a set of rules that allow systems to communicate over the internet using HTTP methods like GET, POST, PUT, DELETE, etc. They follow RESTful principles, making them scalable, stateless, and flexible.

Characteristics of REST APIs
1. Stateless
Each request from a client contains all the necessary information, and the server does not store any client-specific session data.
Example: If a user requests data, the server doesn’t remember previous requests.

2. Client-Server Architecture

The client (frontend) and server (backend) are separate, allowing them to evolve independently.
Example: A mobile app can consume the same API as a web app.
Uniform Interface

Follows standard HTTP methods:
GET → Fetch data
POST → Create data
PUT → Update data
DELETE → Remove data
Cacheable

Responses can be stored in a cache to improve performance.
Example: Static resources like product lists can be cached to reduce repeated API calls.

3. Layered System

APIs can have multiple layers (e.g., security, load balancing) without the client knowing.
Example: A request may pass through an authentication layer before reaching the database.
Code on Demand (Optional)

The server can send executable code (like JavaScript) to the client if needed.
Use of JSON or XML

Most REST APIs use JSON for data exchange as it is lightweight and easy to parse.
Example of a REST API Request & Response
Request: GET /users/123
Response (JSON):
json


{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com"
}




Let's build a REST API using Node.js, Express, and MongoDB 🚀. We'll create a simple User Management API with CRUD operations.

📌 Steps to Create REST API
Initialize a Node.js project (npm init -y)
Install dependencies (express, mongoose, dotenv, cors, body-parser)
Set up Express server
Connect MongoDB using Mongoose
Create RESTful routes (CRUD)
Test API using Postman
1️⃣ Install Dependencies
Run this command in your project folder:




npm install express mongoose dotenv cors body-parser
2️⃣ Setup Express Server
Create a file server.js and add:

javascript


const express = require("express");
const mongoose = require("mongoose");
const dotenv = require("dotenv");
const cors = require("cors");

dotenv.config();

const app = express();
app.use(express.json()); // Middleware to parse JSON
app.use(cors()); // Enable CORS

const PORT = process.env.PORT || 5000;

// Connect to MongoDB
mongoose.connect(process.env.MONGO_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
}).then(() => console.log("MongoDB Connected"))
  .catch(err => console.log(err));

app.get("/", (req, res) => {
  res.send("Welcome to REST API");
});

app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
3️⃣ Configure MongoDB Connection
Create a .env file and add:

ini


MONGO_URI=mongodb+srv://your_username:your_password@cluster.mongodb.net/mydb
PORT=5000
4️⃣ Create User Model
Create a folder models and a file User.js:

javascript


const mongoose = require("mongoose");

const UserSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  age: { type: Number, required: true },
}, { timestamps: true });

module.exports = mongoose.model("User", UserSchema);
5️⃣ Create User Routes (CRUD)
Create a folder routes and a file userRoutes.js:

javascript


const express = require("express");
const User = require("../models/User");
const router = express.Router();

/** 🔵 CREATE USER */
router.post("/", async (req, res) => {
  try {
    const { name, email, age } = req.body;
    const newUser = new User({ name, email, age });
    await newUser.save();
    res.status(201).json(newUser);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

/** 🟢 GET ALL USERS */
router.get("/", async (req, res) => {
  try {
    const users = await User.find();
    res.status(200).json(users);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

/** 🟡 GET SINGLE USER BY ID */
router.get("/:id", async (req, res) => {
  try {
    const user = await User.findById(req.params.id);
    if (!user) return res.status(404).json({ message: "User not found" });
    res.status(200).json(user);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

/** 🟠 UPDATE USER */
router.put("/:id", async (req, res) => {
  try {
    const { name, email, age } = req.body;
    const user = await User.findByIdAndUpdate(
      req.params.id,
      { name, email, age },
      { new: true }
    );
    if (!user) return res.status(404).json({ message: "User not found" });
    res.status(200).json(user);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

/** 🔴 DELETE USER */
router.delete("/:id", async (req, res) => {
  try {
    const user = await User.findByIdAndDelete(req.params.id);
    if (!user) return res.status(404).json({ message: "User not found" });
    res.status(200).json({ message: "User deleted" });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

module.exports = router;
6️⃣ Connect Routes to Server
Modify server.js to include the routes:

javascript


const userRoutes = require("./routes/userRoutes");

app.use("/api/users", userRoutes); // Base path for user API
7️⃣ Test API using Postman
📍 Create User (POST)
URL: http://localhost:5000/api/users
Body (JSON):
json


{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 25
}
📍 Get All Users (GET)
URL: http://localhost:5000/api/users
📍 Get Single User (GET)
URL: http://localhost:5000/api/users/:id
📍 Update User (PUT)
URL: http://localhost:5000/api/users/:id
Body (JSON):
json


{
  "name": "John Updated",
  "email": "johnnew@example.com",
  "age": 30
}
📍 Delete User (DELETE)
URL: http://localhost:5000/api/users/:id
🚀 Your REST API is Ready!
Now you can integrate it with a frontend like React, Vue, or Angular.

 😊











