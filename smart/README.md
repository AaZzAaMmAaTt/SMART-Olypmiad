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

## Recommended Next Steps
1. Add server-backed auth and role policy hardening.
2. Add websocket/SSE for live support chat.
3. Add richer practice bank across all SMART subjects.
4. Add certificate verification page with verification code lookup.
5. Add media/file attachments for support messages.
6. Add analytics charts (Chart.js/ECharts) for dashboard trends.
