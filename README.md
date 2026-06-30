# Lotus Support AI

An AI-powered customer support chatbot platform. Sign up, train the bot on your own business knowledge, and embed a lightweight chat widget on any website with a single script tag — powered by Google Gemini.

## Screenshots

<p align="center">
  <img src="https://github.com/user-attachments/assets/2b31ff22-c541-4588-ac87-a753207096bf" width="200" alt="Screenshot 1" />
  <img src="https://github.com/user-attachments/assets/c67b2a6a-25e7-4792-94ac-38393778dd80" width="200" alt="Screenshot 2" />
  <img src="https://github.com/user-attachments/assets/c7cc4bf7-1b4f-490c-b176-de8da8000e6c" width="200" alt="Screenshot 3" />
  <img src="https://github.com/user-attachments/assets/6997def0-9b4b-4335-ad70-bc6b825a5f66" width="200" alt="Screenshot 4" />
</p>

## Features

- 🔐 Secure authentication and session management via Scalekit (login, logout, callback handling)
- 🤖 AI chat replies powered by Google Gemini (`gemini-2.5-flash`)
- ⚙️ Dashboard to configure business name, support email, and a custom knowledge base that shapes how the bot responds
- 💬 Lightweight, embeddable chat widget (`chatBot.js`) — drop one `<script>` tag into any website to add a floating support chatbot
- 📱 Responsive widget that adapts to mobile and desktop viewports
- 🗄️ MongoDB-backed settings storage per account

## Tech Stack

- **Framework:** Next.js 16 (App Router, Turbopack)
- **UI:** React 19, Tailwind CSS 4, Motion (animations)
- **Auth:** Scalekit (full-stack auth — sessions, login/callback flow)
- **Database:** MongoDB with Mongoose
- **AI:** Google Gemini API (`@google/genai`)
- **Language:** TypeScript

## Project Structure

```
src/
├── app/
│   ├── api/
│   │   ├── auth/         # login, callback, logout routes (Scalekit)
│   │   ├── chat/         # chat endpoint — calls Gemini with saved knowledge
│   │   └── settings/     # get/save business settings per account
│   ├── dashboard/        # business settings dashboard (authenticated)
│   ├── embed/            # preview page for the embeddable widget
│   └── layout.tsx        # root layout, metadata/title
├── components/           # HomeClient, DashboardClient, EmbedClient, etc.
├── lib/                  # db connection, Scalekit client, session helpers
└── model/                # Mongoose schemas (Settings)
public/
└── chatBot.js             # the embeddable widget script
```

## Getting Started

### Prerequisites

- Node.js 20+
- A MongoDB database (e.g. a free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster)
- A [Scalekit](https://scalekit.com) account/project (for authentication)
- A [Google Gemini API key](https://aistudio.google.com/apikey)

### Installation

```bash
git clone <your-repo-url>
cd lotus-support-ai
npm install
```

### Environment Variables

Create a `.env.local` file in the project root:

```dotenv
SCALEKIT_ENVIRONMENT_URL=your_scalekit_environment_url
SCALEKIT_CLIENT_ID=your_scalekit_client_id
SCALEKIT_CLIENT_SECRET=your_scalekit_client_secret
NEXT_PUBLIC_APP_URL=http://localhost:3000
MONGODB_URL=your_mongodb_connection_string
GEMINI_API_KEY=your_gemini_api_key
```

In your Scalekit dashboard, add the following as an allowed redirect/callback URI:

```
http://localhost:3000/api/auth/callback
```

(Update this to your production domain once deployed.)

### Run locally

```bash
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000).

## Configuring Your Bot

1. Log in via the **Login** button (handled by Scalekit).
2. Go to the **Dashboard** and fill in your business name, support email, and a knowledge base describing your business, products, policies, and FAQs.
3. Save — this knowledge is what the AI uses to answer customer questions.

## Embedding the Widget

Add the following script tag to any website's HTML, just before the closing `</body>` tag:

```html
<script
  src="https://your-deployed-domain.com/chatBot.js"
  data-owner-id="YOUR_OWNER_ID">
</script>
```

Your `data-owner-id` is your unique account ID, available from the embed code shown on the `/embed` page after logging in. The widget will appear as a floating chat bubble in the bottom-right corner of the page.

## Deployment

This project is built for deployment on [Vercel](https://vercel.com):

1. Push your repository to GitHub.
2. Import the project into Vercel.
3. Add all environment variables from `.env.local` under **Project Settings → Environment Variables**, updating `NEXT_PUBLIC_APP_URL` to your production URL.
4. Add your production callback URL (`https://your-domain.com/api/auth/callback`) to Scalekit's allowed redirect URIs.
5. In MongoDB Atlas, allow network access from `0.0.0.0/0` (or Vercel's IP ranges) so the deployed app can connect.
6. Update `chatBot.js`'s `api_Url` to point to your production domain before embedding it on live sites.

## License

This project is for personal/educational use. Update this section with your preferred license if distributing publicly.

## Author

Built by **Pankaj Maurya**.
