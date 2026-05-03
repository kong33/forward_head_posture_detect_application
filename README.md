# 🐢Boogi Boogi: AI based Forward Head Posture Detection Web Application
- you can see my working flow (pr, review ...) from the original [organization repository](https://github.com/CapstoneDesign-KHU-2025/forward_head_posture_detect_application)!
---

## 📑 Table of Contents
- [📌 Overview](#-overview)
- [💚 Demo](#-demo)
- [👉 Why do you need BoogiBoogi?](#-why-do-you-need-boogiboogi)
- [🧪 Scientific Background](#-scientific-background)
- [📋 How was the detection threshold set?](#detection-threshold)
- [📊 Detection Sensitivity Levels](#-detection-sensitivity-levels)
- [🛠 Tech Stack](#-tech-stack)
- [🧑‍🤝‍🧑 Team members and roles](#team-members-and-roles)
- [💻 My contribution](#my-contribution)
  - [📍 Features](#-features)
  - [📈 Optimization](#-optimization)
  - [🔐 Focusing on Security](#-focusing-on-security)
  - [👾 Backend & API Architecture](#-backend--api-architecture)
  - [🤖 Ai using philosophy](#-ai-using-philosophy)
  - [📉 Data analysis for accuracy](#-data-analysis-for-accuracy)
  

---
## 📌 Overview

Most web-based posture correction systems rely on a **side-view camera setup**, which often requires additional space or inconvenient camera placement.

This application estimates forward head posture using only a **front-facing webcam**, <br/>
allowing users to measure posture naturally during everyday computer use without extra hardware or environmental adjustments.<br/>
Plus, no video or photo data of the user is serving to server for the privacy!

## 💚 Demo
[📱production](https://forward-head-posture-detect-applica.vercel.app/en)
<table>
  <tr>
    <td width="45%">
      <img src="https://github.com/user-attachments/assets/7016e40e-2891-431e-84c0-4e848003409b" width="100%" alt="image1" />
    </td>
    <td width="55%">
      <b>1. Main Page </b><br/>
     The personalized home screen includes: <br/>
     - A monthly calendar showing posture status by date.<br/>
     - Warning messages and feedback based on posture measurements.<br/>
     - Cards for measurement time, warning count, and cumulative average angle.<br/>
     - A 3D avatar for visualizing the user’s posture status.<br/>
     - A character growth UI for tracking posture improvement progress.<br/>
     - Language switching for multilingual support.<br/>
     - Sound controls.<br/>
    - A profile button for account/character/sensitivity settings.<br/>
    </td>
  </tr>
  <tr>
    <td width="45%">
      <img src="https://github.com/user-attachments/assets/99fbb8a7-fd88-4a0d-97e5-d5c6d08eb7ac" width="100%" alt="image2" />
    </td>
    <td width="55%">
      <b>2. Estimate page</b><br/>
      - Users can check their posture in this page.<br/>
      - Start measuring by clicking the button. <br/>
    </td>
  </tr>
  <tr>
    <td width="45%">
      <img src="https://github.com/user-attachments/assets/92b47fe0-9cc1-4989-9713-93a5bceaec64" width="100%" alt="image3" />
    </td>
    <td width="55%">
      <b>3. Tip modal</b><br/>
      - Users can check tips for the best measuring environment.
    </td>
  </tr>
  <tr>
    <td width="45%">
      <img src="https://github.com/user-attachments/assets/b7b76ac6-0758-48d7-b0f7-afb1074fbc67" width="100%" alt="image4" />
    </td>
    <td width="55%">
      <b>4. Estimating UI</b><br/>
      - Users can see themselves through the video canvas, but any video or photo is not sent to server. <br/>
      - If users have bad posture, badge will change into red and beep sound is played.<br/>
      
    </td>
  </tr>
  <tr>
    <td width="45%">
      <img src="https://github.com/user-attachments/assets/4592a4d9-211a-4700-af12-25570d28de7f" width="100%" alt="image5" />
    </td>
    <td width="55%">
      <b>5. Popup function </b><br/>
      - Provides a picture-in-picture popup so users can check their posture in a small floating window instead of keeping the full browser open.
    </td>
  </tr>
</table>

---
### 🧠 Posture Detection Algorithm
- Processed MediaPipe landmark coordinates
- Calculated neck angle deviation based on shoulder–ear alignment
- Applied threshold-based classification for forward head posture detection

### 🖥 Architecture
- Designed component-based UI structure in Next.js
- Implemented real-time feedback system (visual + audio alerts)
- Optimized rendering to handle continuous webcam input
- Designed a type-safe backend API layer using Next.js Server Actions and Zod validation
- Integrated PostgreSQL (NeonDB) via Prisma ORM for scalable data management and secure transactions

### ☁ Infrastructure Setup
- Connected PostgreSQL (NeonDB) for data storage
- Released with Vercel.
---
## 👉 Why do you need **BoogiBoogi**?

Have you seen this woman?

<img width="616" height="346" alt="image" src="https://github.com/user-attachments/assets/4f1cbb75-8d36-45f9-9fc9-090ba5cc51be" /> <br/>
[source](https://www.chosun.com/national/welfare-medical/2021/07/17/25SRDOHGPFH5TBEL4FFE5KKDO4/)

This image was created by British behavioral futurist **William Higham**, <br/>
which explored how the body of an office worker might change after **20 years of desk-based work**.

It shows how long hours of office work and poor posture can gradually affect the human body. <br/>
Today, posture-related problems are becoming increasingly common among modern workers.

According to the **Korea Disease Control and Prevention Agency (KDCA)**, <br/>
forward head posture is reported in more than **70% of adults aged 25 to 42**.

[Source](https://health.kdca.go.kr/healthinfo/biz/health/gnrlzHealthInfo/gnrlzHealthInfo/gnrlzHealthInfoView.do?cntnts_sn=5972)

For this reason, there is a clear need for a tool that helps users monitor and improve their posture easily during everyday work.


---

## 🧪 Scientific Background

**Forward head posture (FHP)** is commonly assessed using the **craniovertebral angle (CVA)**.

In many clinical studies, FHP is identified when the CVA falls below approximately **45° to 50°**. <br/>
One of the early studies frequently referenced for this range is:

[Reference](https://pubmed.ncbi.nlm.nih.gov/17368075/)

### 🧐 What is CVA?

The **craniovertebral angle (CVA)** is a widely used measurement for evaluating forward head posture. <br/>
It is generally defined as the angle formed between:

- a horizontal line through the **C7 vertebra**
- a line connecting **C7** to the **tragus of the ear**

<img width="331" height="260" alt="image" src="https://github.com/user-attachments/assets/f6af6a15-ec3c-4b76-b444-c7698179dc70" />

[Source](https://www.researchgate.net/figure/Measurement-of-craniovertebral-angle-with-the-CAV_fig1_284018894)

---
<a id="detection-threshold"></a>
## 📋 How was the detection threshold set?

A recent study published in **2024** classified **severe forward head posture** as a CVA below **45°**.

The same study also reported that CVA tends to be measured **lower in the sitting position than in the standing position**, <br/>
regardless of whether the participant has forward head posture.

Since this application is mainly intended for users who are **sitting at a desk**,<br/>
this difference was considered when setting the detection thresholds. <br/>

[Reference](https://pubmed.ncbi.nlm.nih.gov/38665167/) (Evaluation of the Craniovertebral Angle in Standing versus Sitting Positions in Young Adults with and without Severe Forward Head Posture
David A. Titcomb et al. / January 2024)


---

## 📊 Detection Sensitivity Levels

This application provides three posture sensitivity levels <br/>
so that users can choose how strictly posture changes should be monitored:

- **Low**: **45°**
- **Middle**: **48°**
- **High**: **50°**

### Why these values?

- **45°** was used for **Low**, based on the threshold used in the paper for **severe forward head posture**
- **48°** was used for **Middle** as a more moderate threshold for everyday monitoring
- **50°** was used for **High** because many studies treat angles above **50°** as being within a normal posture range

This allows the application to support different levels of detection sensitivity depending on the user's preference.

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

# My contribution 
- 51% out of 4 team members (based on commit numbers)
---
# 📍 features
### Frontend

- state managing with zustand ( MeasurementController, PipController, Soundcontroller )
- custom hooks ( useFriendsData, useHandleHotKey ... )
- UI component/page ( HelpMessageModal, CharacterSelectionPage ... )<br/>

I am working on my code with this rules. <br/>

#### 1. Clean code: Write codes that you can find logic quickly.
😭 before refactoring <br/>
```ts
useEffect(() => {
    const handleKeyDown = (e: KeyboardEvent) => {
      if (e.key === "Enter" && selectedCharacter) {
        handleConfirm();
      } else if (e.key === "Escape") {
        handleSkip();
      }
    };

    window.addEventListener("keydown", handleKeyDown);
    return () => window.removeEventListener("keydown", handleKeyDown);
  }, [selectedCharacter]);
```
🥰 after refactoring <br/>
```ts
  useHandleHotKey("Enter", () => {
    if (selectedCharacter) {
      handleConfirm();
    }
  });
  useHandleHotKey("Escape", () => {
    handleSkip();
  });
```
#### 2. One task in one function: Function does one job at once.
😭 before refactoring <br/>
```ts
 const handleConfirm = () => {
    if (selectedCharacter) {
      if (typeof window !== "undefined") {
        localStorage.setItem("selectedCharacter", selectedCharacter);
      }
      router.push("/");
    }
  };

  const handleSkip = () => {
    if (typeof window !== "undefined") {
      localStorage.setItem("selectedCharacter", "remy");
    }
    router.push("/");
  };
```
🥰 after refactoring <br/>
```ts
 const saveCharacterAndRedirect = (characterId: string) => {
    if (typeof window != "undefined") {
      localStorage.setItem("selectedCharacter", characterId);
    }
    router.replace("/");
  };
  const handleConfirm = () => {
    if (selectedCharacter) {
      saveCharacterAndRedirect(selectedCharacter);
    }
  };
  const handleSkip = () => {
    saveCharacterAndRedirect("remy");
  };
```
#### 3. Similar levels of abstraction: Make sure that level of abstraction is similar in a component, page ...etc.
😭 before refactoring <br/>
```ts
     <div>
        <Button>
           ...
        </Button>
            <div
                className={`grid transition-all duration-300 ease-in-out ${
                isAccordionOpen ? "grid-rows-[1fr] opacity-100" : "grid-rows-[0fr] opacity-0"
                    }`}
                  >
                    <div className="overflow-hidden">
                      <div className="px-3.5 pb-3.5 pt-0 text-[13px] leading-relaxed text-[var(--green)]">
                        <ul className="flex flex-col gap-1.5">
                          {item.descriptions.map((desc, idx) => (
                            <li key={idx} className="flex gap-1.5 items-start">
                              <span className="mt-0.5 text-[var(--green-mid)] text-[10px]">●</span>
                              <span>{desc}</span>
                            </li>
                          ))}
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
              );
            })}
          </div>
        </div>
      </div>
    </>
```
🥰 after refactoring <br/>
```ts
 <div>
    <Button>
       ...
    </Button>
      <div className="custom-scrollbar flex max-h-[400px] flex-col gap-2.5 overflow-y-auto pr-1">
          {GUIDE_DATA.map((item) => (
              <HelpAccordionItem
                key={item.id}
                item={item}
                isOpen={openAccordionId === item.id}
                onToggle={() => toggleAccordion(item.id)}
              />
            ))}
          </div>
        </div>
      </div>
```
#### 4. Birds of a feather flock together: Make the codes that has same goal gather together.


### Backend
- All logic on BE side.

---
# 📈 Optimization

### ⚡LCP
#### home page - Reduced 45% 
- Parallelized AI & Camera Loading: Eliminated waterfall loading bottlenecks by executing <br/>
`PoseLandmarker.createFromOptions` (MediaPipe AI) and `navigator.mediaDevices.getUserMedia` (Camera API) asynchronously in parallel.
- Unblocked UI Rendering: Seperated the `CanvasRenderingContext2D.drawImage` logic from the AI worker's readiness, <br/>
providing an instant camera feed to users while the model downloads in the background.
  
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/7aa1690b-3ad6-4bea-8093-cfa6bdbbb4da" width="420" alt="Before optimization" />
    </td>
    <td align="center" style="font-size: 28px; font-weight: bold; padding: 0 10px;">
      =&gt;
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ede962a5-4ceb-453c-8eec-5209084299c2" width="420" alt="After optimization" />
    </td>
  </tr>
  <tr>
    <td align="center"><sub>Before</sub></td>
    <td></td>
    <td align="center"><sub>After</sub></td>
  </tr>
</table>

### 💻cpu usage 
#### estimate page - Reduced Computer CPU 52% / Reduced browser CPU 63%
- Dynamic FPS Throttling: Leveraged the Page Visibility API (document.hidden) to dynamically reduce the measurement polling rate <br/>
(e.g., 10fps down to 5fps) when the tab is inactive, significantly optimizing CPU usage and battery consumption.

<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/d39f05a2-9ad2-4652-8b79-39d6a93e5f34"  width="420" alt="Before optimization" />
    </td>
    <td align="center" style="font-size: 28px; font-weight: bold; padding: 0 10px;">
      =&gt;
    </td>
    <td align="center">
      <img  src="https://github.com/user-attachments/assets/13dfb8b7-02ed-45dc-bc5a-b6f766f08110"  width="420" alt="After optimization" />
    </td>
  </tr>
  <tr>
    <td align="center"><sub>Before</sub></td>
    <td></td>
    <td align="center"><sub>After</sub></td>
  </tr>
</table>

<table align="center">
  <tr>
    <td align="center">
      <img  src="https://github.com/user-attachments/assets/2f07665d-5ccf-4e54-a46a-0b3eeb85fb12"   width="420" alt="Before optimization" />
    </td>
    <td align="center" style="font-size: 28px; font-weight: bold; padding: 0 10px;">
      =&gt;
    </td>
    <td align="center">
      <img   src="https://github.com/user-attachments/assets/b59213e1-1879-4d41-a88d-326800d2cc51"  width="420" alt="After optimization" />
    </td>
  </tr>
  <tr>
    <td align="center"><sub>Before</sub></td>
    <td></td>
    <td align="center"><sub>After</sub></td>
  </tr>
</table>

### 🖱️INP
- Web Worker Architecture (`poseDetection.worker.ts`): Offloaded heavy landmark computations to a background thread. <br/>
Utilized `createImageBitmap` to transfer video frames efficiently, preventing main thread blocking.

### ❇️lightHouse
- Memory Leak Prevention: Enforced strict useEffect cleanups in Estimate.tsx to reliably execute <br/>
`worker.terminate()`, `PiP window.close()`, and `MediaStreamTrack.stop()` upon component unmount.


---
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

- Prevents content-type sniffing attacks with `X-Content-Type-Options: nosniff`
- Reduces cross-origin referrer leakage with a `strict referrer policy`
- Restricts access to sensitive browser capabilities through `Permissions-Policy`

This middleware-based approach made security rules easier to maintain and ensured they were applied uniformly across the application.

---
# 👾 Backend & API Architecture

## 🚀 Type-Safe API Layer
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

## 🚀 Robust Social System
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
  
## 🚀 Enterprise-level Error Handling
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

### 🤖 AI using philosophy
- I added our coding philosopy to Claude Code skills.
- I use this skills for repeated, simple tasks. Such as ...
    - Change `<button>` into `<Button>` in whole code base.
    - Move componets that has to do with 'estimate'page into app/estimate/components folder.
- I also consider Claude Code as a senior developer I can discuss about the refactoring.

### 📉 Data analysis for accuracy
[data analysis board](https://github.com/kong33/boogiboogi-streamlit)
- I analyzed our CVA data and removed the noises.

### 🍀 Thanks for reading! 
## 🌝 We are waiting for the contribution!! Every feedback is welcomed !!
[feedback link](https://docs.google.com/forms/d/e/1FAIpQLSeRNoOKH3aNfmu0_JMZFy6Vslur6jfBuNlrj-5-Cekjen9wpw/viewform?usp=dialog)
---
