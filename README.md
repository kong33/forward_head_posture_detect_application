# 🧍 Forward Head Posture Detection Web Application


## 📌 Overview

Traditional posture correction systems rely on side-angle camera setups, <br/>
requiring no additional devices or physical space adjustments.

This web application estimates forward head posture using only a **front-facing webcam**,<br/>
allowing users to measure posture seamlessly during everyday computer use —
without extra hardware.

---

## 🧪 Scientific background

Forwarded posture is diagnosed when the CVA(Craniovertebral Angle) 

## 🎯 Key Features

- Real-time body landmark extraction using **MediaPipe Pose Landmarker**
- Client-side posture analysis built with **Next.js**
- 3D visualization of averaged posture using **Three.js**

---

## 🛠 Tech Stack

| Category | Technology |
|----------|------------|
| **Frontend** | Next.js, React, TypeScript, TailwindCSS |
| **Pose Estimation** | MediaPipe Pose Landmarker |
| **3D Visualization** | Three.js |
| **Backend / DB** | Next.js, PostgreSQL (NeonDB), prisma |
| **Collaboration** | GitHub, Jira, notion |

🔗 Jira Board:  
https://kge0211114.atlassian.net/jira/software/projects/TNA/boards/34

---

## Team members and roles
- Gaeun Kim: AI, Backend Lead, Frontend
<br>[김가은 | kge0211114@gmail.com](mailto:kge0211114@gmail.com)
- Jimin Nam: Frontend Lead
<br>[남지민 | dnpsel2737@gmail.com](mailto:dnpsel2737@gmail.com)
- Seunghyun park: Frontend(Three.js)
<br>[박승현 | seunghyuni00@khu.ac.kr](mailto:seunghyuni00@khu.ac.kr)
- Jun Hur: AI Lead
<br>[허준 | heojun8500@naver.com](mailto:heojun8500@naver.com)

---
# 📈 Optimization

### LCP

### INP

### lightHouse

### cpu usage

# 🔐 Focusing on Security

This project processes user health-related data. We got a lot of feedbacks concerning about privacy problem.
To minimize security risks and protect sensitive information, we implemented the following strategies:

---

### 1️⃣ Local Storage Strategy — IndexedDB

Regularly collected posture data is stored in **IndexedDB on the client side** instead of being continuously transmitted to the server.

This approach:

- Reduces exposure to network-based interception (e.g., MITM attacks)
- Minimizes unnecessary data transmission up to 90%
- Limits server-side accumulation of sensitive health data
- Hardly being influcned by network disconnection.

Only essential or aggregated data is persisted to the backend when necessary.

---

### 2️⃣ Full-Stack Architecture with Next.js - Server actions

We adopted **Next.js as a full-stack framework** to unify frontend and backend logic within a single controlled environment.

This provides:

- Reduced attack surface by avoiding publicly exposed REST endpoints
- Sensitive logic never exposed to the client bundle
- Strong type safety between client and server

By consolidating the stack, we minimized configuration inconsistencies and improved maintainability.

---

### 3️⃣ Zod Validation

- Enforce strict input validation
- Prevent malformed or malicious payloads
- Ensure runtime data integrity beyond TypeScript's compile-time checks

---

### 4️⃣ Security Headers in Middleware

This approach:

- Protects against clickjacking with X-Frame-Options: DENY
Prevents content-type sniffing attacks with X-Content-Type-Options: nosniff
Reduces cross-origin referrer leakage with a strict referrer policy
Restricts access to sensitive browser capabilities through Permissions-Policy

This middleware-based approach made security rules easier to maintain and ensured they were applied uniformly across the application.

---
# 🔒 Backend & API Architecture

## 🚀Type-Safe API Layer
Constructed robust APIs using Next.js Server Actions, strictly validating client payloads via **Zod** to ensure runtime safety.
```ts
//actions/summaryActions.ts
const PostDailySummarySchema = z.object({
  dateISO: z.string().regex(/^\d{4}-\d{2}-\d{2}$/, "wrong date formation"),
  sumWeighted: z.number().refine(Number.isFinite),
  weightSeconds: z.number().refine((n) => Number.isFinite(n) && n > 0),
  count: z.number().int().nonnegative(),
});

export type PostDailySummaryInput = z.infer<typeof PostDailySummarySchema>;

export async function postDailySummaryAction(_prevState: ActionState<unknown>, data: PostDailySummaryInput) {
  const session = await auth();
  if (!session?.user?.id) {
    return { ok: false, status: 401, message: SERVER_MESSAGES.AUTH_REQUIRED } as const;
  }

  const parsed = PostDailySummarySchema.safeParse(data);
  if (!parsed.success) {
    return { ok: false, status: 400, message: SERVER_MESSAGES.SYSTEM_MESSAGES } as const;
  }

  try {
    const result = await upsertDailySummary({
      ...parsed.data,
      userId: session.user.id,
    });
    revalidateTag("daily_summary");

    return { ok: true, data: result } as const;
  } catch (error: unknown) {
    logger.error("[postDailySummaryAction] Error:", error);
    return { ok: false, status: 500, message: SERVER_MESSAGES.INTERNAL_SERVER_ERROR } as const;
  }
}

```

## Why We Used Next.js Server Actions

1. **Eliminated Separate API Layer**  
   Reduced complexity by removing the need for dedicated REST endpoints.

2. **End-to-End Type Safety**  
   Shared TypeScript types between client and server without manual request/response contracts.

3. **Smaller Client Bundle Size**  
   Database logic stays on the server, preventing unnecessary client-side code bloat.

4. **Improved Security**  
   Sensitive logic and database access are never exposed to the browser.

5. **Seamless React Integration**  
   Works natively with React Server Components, Suspense, and streaming.

6. **Built-in Caching & Revalidation**  
   Leveraged `revalidatePath` and `revalidateTag` for automatic cache invalidation without external libraries. ( No need to add caching library like TQ )

   ---

## 🚀Robust Social System
Implemented scalable friendship management ensuring data consistency and integrity using Prisma `$transaction`.

```ts
// friends.service.ts
  return prisma.$transaction(async (tx) => {
    const updated = await tx.friendRequest.update({
      where: { id: requestId },
      data: { status: "ACCEPTED", respondedAt: new Date() },
      select: { id: true, status: true, respondedAt: true, fromUserId: true, toUserId: true },
    });
  ```
  ---
  
## 🚀Enterprise-level Error Handling
Integrated a centralized logging utility with **Sentry**, providing context-aware error tracking and i18n-ready, <br/>
user-friendly error messages while securing sensitive stack traces in production.

error message that developers see:
```ts
return json({ error: "UNAUTHORIZED" }, 401);
```
error message that users see:
```ts
  FRIEND_NOT_FOUND: {
    ko: "아직 저희 서비스를 이용하지 않는 친구 같아요. 이 기회에 초대해 보는 건 어떨까요? 💌",
    en: "It looks like your friend hasn't joined us yet. Why not invite them? 💌",
  },
```
---

### 🧠 Posture Detection Algorithm
- Processed MediaPipe landmark coordinates
- Calculated neck angle deviation based on shoulder–ear alignment
- Applied threshold-based classification for forward head posture detection

### 🖥 Frontend Architecture
- Designed component-based UI structure in Next.js
- Implemented real-time feedback system (visual + audio alerts)
- Optimized rendering to handle continuous webcam input

### ☁ Infrastructure Setup
- Connected PostgreSQL (NeonDB) for persistent data storage
- Structured measurement data schema for longitudinal tracking

---

## 🚀 Getting Started

```bash
git clone https://github.com/CapstoneDesign-KHU-2025/forward_head_posture_detect_application.git
cd forward_head_posture_detect_application
npm install
npm run dev
```



