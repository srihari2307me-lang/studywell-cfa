# Studywell hosted app setup

## Supabase sign-in and private progress

The project is provisioned in the Mumbai region, the `studywell_data` table is created with row-level security enabled, and `site/config.js` already contains the project URL and publishable key. The key is intended for browser use; never put a secret/service-role key there. Each login can access only its own row.

Before login works on a hosted site, add its final URL to Supabase Auth's allowed redirect URLs. Email verification may be required for new accounts.

Row-level security restricts each record to its signed-in owner. The app keeps an offline copy in that browser. Each cloud upload asks for confirmation. On a new device, sign in and confirm loading the existing account record.

## GitHub Pages

The workflow publishes the contents of `site/` on pushes to `main` and when run manually. In GitHub repository settings, enable Pages with GitHub Actions.

GitHub Pages sites are publicly accessible. On GitHub Free, the repository must also be public. A public app page does not make the Supabase study records public: access depends on Supabase Auth and the row-level security migration.

## Google Calendar and Apple Calendar

For automatic timetable writes, create a Google OAuth 2.0 Web client, enable the Google Calendar API, add the published site origin to authorized JavaScript origins, and set its client ID in `site/config.js`. Use the narrow `calendar.events` scope. The app asks before every timetable write and does not ask for or store a Google password. OAuth setup requires completing Google's app consent configuration.

To see the same Google calendar in Apple Calendar on Mac and iPad, add that Google account to Apple's Internet Accounts / Calendar settings on those devices. Direct writes into a separate iCloud calendar are not enabled in this version; that needs a separate Apple CalDAV authorization design.

## Account password handling

The email and password are submitted to Supabase Auth over its sign-in flow. Studywell does not save the password. The account session is retained by the Supabase browser client so the user does not need to re-enter the password for every save; a separate confirmation appears before each cloud upload and each calendar write.
