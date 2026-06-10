# RoastCV 🔥

### Get your resume brutally roasted — by AI and real people.

Most resume feedback is polite, vague, and useless. RoastCV gives you the brutal, honest critique your resume actually needs — instant AI analysis powered by GPT-4o, plus a community of developers and job seekers who won't hold back.

**[Live Demo](https://roastcv.vercel.app)** · **[Report a Bug](https://github.com/yourusername/roastcv/issues)** · **[Request a Feature](https://github.com/yourusername/roastcv/issues)**

---

## Why I built this

I was applying for jobs, getting ghosted, and had no idea why. Every "resume review" service gave me the same generic advice — add keywords, use bullet points, keep it one page. None of it was specific to me.

So I built RoastCV. Upload your resume anonymously, get an AI score with specific actionable fixes, then post it to a community of people who've been through the same grind and will tell you exactly what's wrong with it.

---

## What it does

- **Instant AI roast** — GPT-4o reads your resume and returns a score out of 100, weak bullet points flagged, missing impact numbers called out, ATS keyword gaps identified
- **Anonymous community feed** — post your resume publicly or anonymously, get roasts from real people
- **Version tracking** — upload v2 after improving, see your score delta, watch your resume get better over time
- **Roaster reputation** — people who give great feedback earn scores and badges. Quality over noise.

---

## Tech stack

| Layer         | Tech                                                 |
| ------------- | ---------------------------------------------------- |
| Frontend      | React, Redux, Tailwind CSS                           |
| Backend       | Node.js, Express.js                                  |
| Database      | MongoDB (Atlas)                                      |
| AI            | OpenAI GPT-4o API                                    |
| Auth          | JWT + bcrypt                                         |
| File handling | Multer + pdf-parse                                   |
| Deployment    | Vercel (frontend) · Render (backend) · MongoDB Atlas |

---

## Technical decisions

I kept the AI logic entirely inside `src/services/aiService.js`, isolated from the route controllers. This means if OpenAI's pricing changes and I need to swap models or providers, I change one file. PDF text extraction lives in its own `pdfService.js` for the same reason — separation of concerns that actually matters in production. I used Redux only for auth state and resume versions since those are the two pieces of state genuinely shared across multiple pages — everything else stays local. Resume versions are stored as a linked list in MongoDB (`previousVersionId` pointer), which keeps queries simple while allowing full version history traversal.

---

## Run it locally

**Prerequisites:** Node.js 18+, MongoDB Atlas account, OpenAI API key

```bash
# Clone the repo
git clone https://github.com/yourusername/roastcv.git
cd roastcv

# Backend setup
cd backend
cp .env.example .env
# Fill in your keys in .env
npm install
npm run dev

# Frontend setup (new terminal)
cd ../frontend
cp .env.example .env
# Set VITE_API_URL=http://localhost:5000
npm install
npm run dev
```

Frontend runs on `http://localhost:5173`, backend on `http://localhost:5000`.

---

## Environment variables

**Backend `.env`:**

```
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
OPENAI_API_KEY=your_openai_api_key
PORT=5000
```

**Frontend `.env`:**

```
VITE_API_URL=http://localhost:5000
```

---

## Folder structure

```
roastcv/
├── backend/
│   ├── src/
│   │   ├── config/        # DB and OpenAI setup
│   │   ├── controllers/   # Route logic
│   │   ├── middleware/     # Auth, upload, error handling
│   │   ├── models/        # Mongoose schemas
│   │   ├── routes/        # Express routers
│   │   ├── services/      # aiService.js, pdfService.js
│   │   └── utils/
│   └── server.js
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── store/         # Redux slices
│   │   ├── services/      # Axios instance
│   │   └── hooks/
│   └── main.jsx
└── README.md
```

---

## Roadmap

- [x] AI resume scoring with GPT-4o
- [x] Anonymous community feed
- [x] Resume version tracking
- [ ] Email notifications when roasts arrive
- [ ] ATS keyword gap analysis by job description
- [ ] Mobile app (React Native)

---

## Contributing

PRs are welcome. If you want to roast the codebase as hard as the resumes, open an issue.

---

## License

MIT — use it, build on it, just don't be boring with it.

---

_Built by [Rehan Pathan](https://github.com/yourusername) — because the job market is brutal and your resume feedback should be too._
