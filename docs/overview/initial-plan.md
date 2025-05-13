### **Final Documentation: Blog, Sooon.ai Q&A Repository & Resources Page**  
This document clarifies the **structure**, **functionality**, **layout**, and **tech stack** for your blog, Sooon.ai Q&A repository, and Resources page.  

---

### **1. Website Overview**  
#### **Pages**  
1. **Homepage**  
   - Landing page with navigation to *Sooon.ai*, *Blog*, and *Resources*.  
2. **Sooon.ai Page**  
   - Q&A repository (timeline format) requiring authentication.  
3. **Blog Page**  
   - Two tabs: *Activities* (to-do list) and *Techs* (skill progress).  
4. **Resources Page**  
   - Open-sourced resources (spreadsheets, videos, docs) with download tracking.  
5. **Admin Panel**  
   - Separate website for managing content, users, and backups.  

---

### **2. Page Functionality & Layout**  
#### **A. Homepage**  
- **Functionality**:  
  - Introduce the blog, Sooon.ai repository, and Resources page.  
  - Navigate to Sooon.ai (requires login), Blog, or Resources.  
- **Layout**:  
  - Hero section with brief description.  
  - Three cards:  
    1. **Sooon.ai Card**: "Access Q&A Repository" (login button).  
    2. **Blog Card**: "View Blog" (direct link).  
    3. **Resources Card**: "Explore Resources" (direct link).  

#### **B. Sooon.ai Page (Q&A Repository)**  
- **Functionality**:  
  - Timeline of Q&A entries (most recent → oldest).  
  - Filter entries by tags/categories (future feature).  
  - Clicking a card opens an inner page with detailed notes.  
  - Authentication via Google/Facebook/Instagram (whitelist-only access).  
- **Layout**:  
  1. **Timeline View**:  
     - Vertical line with alternating left/right cards (odd/even index).  
     - Each card shows:  
       - Title, date, tags.  
       - Thumbnail (image/video) if available.  
  2. **Inner Page**:  
     - Top section: Summary answering key questions (your notes).  
     - Bottom section: Linked articles/sources + your annotations.  
     - Back button to timeline.  

#### **C. Blog Page**  
- **Functionality**:  
  - Track progress of blog development and skills.  
- **Layout**:  
  - **Tab 1: Activities**  
    - To-do list with tasks like "Implement authentication."  
    - Filters: *Todo* / *In Progress* / *Done*.  
    - Drag-and-drop reordering.  
  - **Tab 2: Techs**  
    - Progress bars for skills (e.g., "Java: 70%").  
    - Filters: *Frontend* / *Backend* / *DevOps*.  

#### **D. Resources Page**  
- **Functionality**:  
  - Host open-sourced resources (spreadsheets, videos, docs, code).  
  - Track download counts for each resource.  
  - Filter by type (e.g., "Video", "Spreadsheet").  
- **Layout**:  
  1. **Grid View**:  
     - Resource cards with title, type, description, and download count.  
     - Download button triggers count increment + file download.  
  2. **Filters**:  
     - Dropdowns for resource type and sorting (newest/most downloaded).  

#### **E. Admin Panel (Separate Website)**  
- **Functionality**:  
  - Manage content (Sooon.ai entries, blog tasks, resources).  
  - Whitelist users and assign roles.  
  - Automated backups to Google Cloud Storage.  
- **Layout**:  
  1. **Dashboard**: Overview of recent activity.  
  2. **Content Management**:  
     - *Sooon.ai Manager*: CRUD timeline entries + upload media.  
     - *Blog Manager*: Edit Activities/Techs tasks.  
     - *Resources Manager*: Upload/delete resources + track downloads.  
  3. **User Management**:  
     - Add/remove users by email.  
     - Assign roles (`user`/`admin`).  
  4. **Backup Settings**: Schedule daily/weekly backups.  

---

### **3. Detailed Content Requirements**  
#### **Sooon.ai Page**  
- **Authentication**:  
  - Social login (Google/Facebook/Instagram via Auth0).  
  - Whitelist validation (users must be in `allowed_users` collection).  
- **Timeline Entries**:  
  - Title, date, tags, summary, media (image/video URL).  
  - Linked articles (title, URL, your notes).  
- **Filters** (Future Implementation):  
  - By date range, tags, or media type.  

#### **Blog Page**  
- **Activities Tab**:  
  - Task: Title, status, description.  
- **Techs Tab**:  
  - Skill: Title, progress percentage, category.  

#### **Resources Page**  
- **Resource Types**:  
  - Spreadsheets, videos, PDFs, code snippets.  
- **Download Tracking**:  
  - Firestore counter increments on each download.  
- **Data Structure**:  
  ```javascript  
  // Firestore Collection: resources  
  {  
    id: string,  
    title: string,  
    type: "spreadsheet" | "video" | "doc" | "code",  
    downloadUrl: string (Firebase Storage path),  
    downloadCount: number,  
    uploadDate: timestamp  
  }  
  ```  

#### **Website View Counter**  
- **Unique Visits**:  
  - Track using **Firebase Analytics** with a session cookie.  
  - Logic:  
    1. On page load, check for a session cookie.  
    2. If no cookie exists:  
       - Send a "unique_visit" event to Firebase.  
       - Set a session cookie (expires when browser closes).  
- **Exclude Your Visits**:  
  - **Option 1**: Filter your IP in Firebase Analytics.  
  - **Option 2**: Use a Firebase Function to block counting your IP.  

#### **Admin Panel**  
- **Security**:  
  - 2FA for admin accounts.  
  - IP whitelisting (restrict access to your IP).  
- **Backups**:  
  - Automated daily exports of Firestore data.  

---

### **4. Technology Stack**  
#### **Frontend**  
| Tool             | Usage                                     |
| ---------------- | ----------------------------------------- |
| **Vue 3**        | Core framework.                           |
| **Quasar**       | UI components & mobile responsiveness.    |
| **Pinia**        | State management (auth, tasks).           |
| **Firebase SDK** | Real-time data (Firestore) + auth.        |
| **js-cookie**    | Manage session cookies for view tracking. |

#### **Backend**  
| Tool                 | Usage                                 |
| -------------------- | ------------------------------------- |
| **Firebase**         | Auth, Firestore, Storage, Analytics.  |
| **Auth0**            | Instagram OAuth integration.          |
| **Java/Spring Boot** | Future migration (replaces Firebase). |

#### **Deployment**  
| Tool                 | Usage                                      |
| -------------------- | ------------------------------------------ |
| **Firebase Hosting** | Deploy main blog, Sooon.ai, and Resources. |
| **Google Cloud**     | Host Admin Panel (Cloud Run) + backups.    |

---

### **5. Development Plan**  
#### **Phase 1: Core Features (4 Weeks)**  
1. **Week 1**:  
   - Set up Firebase project + Auth0 integration.  
   - Build Homepage & Blog skeleton.  
2. **Week 2**:  
   - Implement Sooon.ai timeline (static data).  
   - Add social login + whitelist check.  
3. **Week 3**:  
   - Design inner page for Q&A entries.  
   - Add Activities/Techs tabs to Blog.  
4. **Week 4**:  
   - Build Resources page with download tracking.  
   - Deploy main site to Firebase Hosting.  

#### **Phase 2: Admin Panel (2 Weeks)**  
1. Build Admin Panel as a separate site.  
2. Implement user/content management.  

#### **Phase 3: Iterations (Ongoing)**  
1. Add filters to Sooon.ai timeline.  
2. Migrate backend to Java/Spring Boot.  
3. Implement website view counter.  

---

This documentation aligns with your goal of a **Q&A repository (Sooon.ai)**, **progress-tracking blog**, **open-sourced resources hub**, and **secure admin panel**. Let me know if you’d like to adjust priorities! 📘