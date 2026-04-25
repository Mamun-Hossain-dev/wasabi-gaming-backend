# Wasabi Gaming Backend API

This repository contains the core logic, databases, and microservice orchestration routines for the Wasabi Gaming platform. Built for blazing-fast speed, high concurrency, and secure AI collaboration.

## 🛠 Tech Stack

- **Runtime**: Node.js, Express.js (v5), TypeScript
- **Database**: MongoDB (Mongoose Schema Architecture)
- **Real-Time Communication**: Socket.io
- **Security & Authorization**: JSON Web Tokens (JWT), bcryptjs
- **Cloud Delivery & Storage**: AWS SDK, Cloudinary, Multer
- **Background Tasks**: `node-cron`, Puppeteer (for generating autonomous reports)

## 🚀 Scalability & Backend Best Practices

Our backend is built around enterprise standards to guarantee infinite horizontal scale and minimum latency:

* **Stateless Operations**: All requests are entirely stateless via JWT, allowing instances to be arbitrarily placed behind high-traffic Load Balancers seamlessly.
* **Aggressive Indexing Strategy**: Mongoose schemas utilize targeted compound and single-field text indexes prioritizing fast `$match` and read-heavy aggregation pipelines over large data volumes.
* **Decoupled Architecture**: Routes, controllers, robust schema validation (`zod`), and heavily abstracted services ensure each file does strictly one job.
* **Offloaded Heavy Lifting**: Instead of saving images locally or overloading the disk, binary data flows straight into **AWS S3** and **Cloudinary** using streamlined buffer streams. Heavy PDF generation via Puppeteer runs in background loops safely detaching from high-priority HTTPS server threads.

## 🤖 AI Integration & Synchronization Workflow

The AI engines interacting with Wasabi Gaming were developed by a dedicated external AI team. Our responsibility at the backend is strictly **secure orchestration, integration, and real-time presentation**.

Here's how we efficiently collaborate and sync our backend with their AI modules:

1. **Decoupled Microservice Communication**: The AI layer operates externally. We initiate the AI workflows from our backend via secure REST API Webhooks. This means we never block the main Node.js event-loop during long AI inference execution.
2. **Asynchronous Webhook Sync**: When an AI request processing resolves, the AI module triggers our designated, authenticated webhook endpoints to push back the calculated metadata securely.
3. **Strict Validation Pipeline**: Every payload incoming from the AI service is strictly typed and validated against strict `Zod` schemas before it touches our MongoDB database. This protects our system against faulty model outputs.
4. **Real-time Pipeline (Socket.io)**: The moment our node receives the Webhook payload from the AI, we dispatch the updated payload to connected users via **Socket.io**. This creates a magical *"real-time"* generation experience for our clients.

## ⚙️ Getting Started

1. **Install Dependencies**:
   ```bash
   npm install
   ```
2. **Environment Configuration**:
   Create a `.env` file referencing variables for `MONGO_URI`, `JWT_SECRET`, `AWS_ACCESS_KEY_ID`, `CLOUDINARY_URL`, etc.
3. **Run Dev Environment**:
   ```bash
   npm run dev
   ```

*Runs through `ts-node-dev` on the port specified in `.env` or defaulting to 5000.*
