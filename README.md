# SMART-Olypmiad
# SMART Olympiad Platform (Static Frontend)

## Project Goal
A premium, responsive SMART Olympiad web platform for courses, olympiad registration, results, support, practice, admin management, and certificate generation — implemented as a static HTML/CSS/JS application.

## Main Features
- Multi-page SPA experience (Home, Courses, Olympiad, About, Methodology, Certificates, FAQ, Contact)
- Auth extension (email/password + demo Google flow)
- User dashboard and results center
- Admin panel for users/courses/results/sections/activity/messages/support/logs
- Support chat (threaded by user, admin can switch between users)
- Practice zone with SMART-subject filtering
- PDF certificate generation with improved visual design
- Saved downloaded certificates in Dashboard achievements
- Notifications modal with SVG bell icon + unread badge
- Mobile hamburger menu with scrollable navigation

## Recently Completed (This Update)
1. **Mobile menu scrolling fix**
   - `#mobile-nav` is now scrollable on mobile with touch-friendly behavior.
2. **Notifications icon upgrade**
   - Replaced plain text/emoji behavior with SVG bell icon + unread badge.
3. **Support redesign + multi-user admin support chat**
   - Improved support UI layout and chat presentation.
   - Conversation model now uses per-user threads (`support-{userId}`).
   - Admin support tab now allows selecting and chatting with different users.
4. **Practice filtering by SMART subjects**
   - Added subject chips: All, Science, Math, Academy, Research, Technology.
5. **Beautiful certificates + dashboard persistence**
   - Certificate PDF redesigned with styled landscape layout.
   - On download, certificate records are saved into `issued_certificates`.
   - Dashboard now includes:
     - Achievements / Downloaded Certificates
     - My Past Olympiads

## Functional Entry URIs (Client-side Routes)
> Navigation uses `data-page` state (single `index.html`).

- `home`
- `courses`
- `olympiad`
- `about`
- `methodology`
- `certificates`
- `faq`
- `contact`
- `privacy`
- `terms`
- `results` *(auth required)*
- `dashboard` *(auth required)*
- `practice` *(auth required)*
- `support` *(auth required)*
- `history`
- `testimonials`
- `admin` *(admin/moderator only)*

### Key UI Parameters / State
- `state.catFilter`, `state.subFilter`, `state.levelFilter`, `state.searchQuery` (courses)
- `state.resultSearch`, `state.gradeFilter` (results)
- `state.practiceSubjectFilter` (practice)
- `state.adminTab` (admin tab switching)
- `state.selectedSupportUserId` (admin support thread target)

## Public URLs
- Production URL: **Publish via the platform Publish tab**
- API base (relative): `tables/{table}`
- File currently edited: `index.html`

## Data Models / Storage Services Used
### Storage
- RESTful Table API (`fetch('tables/{table}')`)
- Local fallback: `localStorage` (`smart_ext_local_v1`)
- Session persistence: `sessionStorage` (`smart_ext_session_v1`)

### Tables Used
- `users`
- `results`
- `bookmarks`
- `messages`
- `content_sections`
- `notifications`
- `courses`
- `activity_logs`
- `error_logs`
- `practice_attempts`
- `issued_certificates` *(added for certificate achievement persistence)*

### Core Record Structures
- **messages**: `{id, conversation_id, from_user_id, to_role, text, read, created_at_custom}`
- **results**: `{id, user_id, exam_name, score, grade, published, notes, issued_at}`
- **practice_attempts**: `{id, user_id, score, details, created_at_custom}`
- **issued_certificates**: `{id, user_id, result_id, exam_name, grade, score, created_at_custom}`

## Not Yet Implemented
- Real backend authentication/session security (server-side)
- Real-time socket chat (currently polling)
- Actual Google OAuth client configuration in production (`GOOGLE_CLIENT_ID` empty)
- Certificate verification endpoint/QR validation backend
- Full localization/i18n settings panel



📊 Olympiad Results: How Data Was Recorded (No Database)
The Olympiad was conducted offline at the school. All tests were graded manually by teachers, so there is no automated database.
To ensure transparency, verifiability, and practical organisation, the following approach was used.

1. Why names may appear "out of order"
Due to the very large number of students, the school administration first created preliminary lists. Based on those lists, each student received a unique login and password.

As a result, student names in the raw files are not necessarily sorted alphabetically or by ID — this is simply a technical side effect of preparing for a large‑scale event.

✅ This is not an error, but a conscious organisational decision made to handle many participants efficiently.

2. How students took the Olympiad (important for integrity)
Each student completed both stages of the Olympiad using the same account (login / password).

This was done intentionally to:

keep statistics consistent

ensure every result is linked to the real student

show honest progress (no duplicate or fake entries)

🔐 The login and password acted as a permanent student identifier throughout the entire Olympiad.

3. Excel – official primary record
Teachers entered final results as percentages for each test.
The school administration then compiled all data into a Excel spreadsheet.

📄 The Excel file serves as the school‑approved official document.

4. Visual dashboard (screenshot: image.png)
Based on the Excel data, the administration created a final visual dashboard — exactly what you see in the attached screenshot:

239 students across 16 classes

monthly comparison (October → November)

average percentages per class

top class (5D with 86.8%)

subject breakdown (Geography, Science, English, Mathematics, History)

✅ The dashboard has been confirmed by the school as the official representation of the results.

5. All Olympiad tests are included in the repository
All test materials used in the Olympiad are provided in this repository.
Anyone reviewing the results can:

see the difficulty level of the questions

recalculate scores if needed

confirm that the grades match the actual test content

🧾 Summary: Evidence for Authenticity (Past Olympiad)
Provided item	Role in proving results
Excel spreadsheet (school administration)	primary official record
Dashboard screenshot (image.png)	visual confirmation of final results
Folder with all tests	ability to verify questions and grading
One account per student (login / password)	honest, consistent linking of results
❌ No database was used because all grading was done manually by teachers.
✅ However, the combination of Excel + dashboard + tests + per‑student accounts provides a fully verifiable and well‑documented record of the Olympiad.

🚀 Future Olympiad (July 15) – What We Are Improving
We have fully acknowledged the limitations of the manual approach.

For the upcoming Olympiad on July 15, we are already building a proper database‑driven system that will allow:

students to take different tests remotely

participants from anywhere in the world (not just one physical location)

automatic result tracking and real‑time analytics

🌍 The goal is to make the Olympiad truly global.

Why the website is not hosted yet
The new platform is currently under heavy reformation — we are restructuring both the architecture and the user experience.

Once the system is stable, complete, and properly tested, we will host it.
Hosting right now does not make sense, as the platform is still in active development and frequent breaking changes are expected.

⚙️ We prefer to release a working, reliable product rather than an unfinished prototype.
