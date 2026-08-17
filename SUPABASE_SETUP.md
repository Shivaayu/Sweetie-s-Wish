# Sweetie's Wish — persistent short-link setup

The old site generated a complete copy of the wish inside the URL. That is why the links became huge and could break when a chat app/browser truncated them. A random code also had no server-side record to look up.

This version uses a small persistent store:

`Sweetie’s Wish form → Supabase Edge Function → Postgres row → short random slug → website/#wish=slug`

The public link contains only the short slug. The actual wish data stays in the database and is fetched when the recipient opens the link.

## 1. Create a Supabase project

Create a project at Supabase. The current free plan is suitable for a small/personal site and currently includes 500 MB database size and 500,000 Edge Function invocations. Free projects can pause after a week of inactivity, so a production site with regular visitors may eventually need a paid plan.

## 2. Create the table

Open the SQL Editor and run `supabase/schema.sql`.

RLS is enabled and there are no public table policies. The browser talks only to the Edge Function; the function uses the server-side service-role key.

**Never put the service-role key in `index.html`.** Only the publishable/anon key is safe to expose in a browser, and even that must be protected by RLS when used directly.

## 3. Deploy the Edge Function

Deploy `supabase/functions/wish-share/index.ts` as `wish-share`.

Set the function's server-side secret:

- `SUPABASE_SERVICE_ROLE_KEY` = the project's service-role key

Supabase supplies `SUPABASE_URL` automatically to Edge Functions.

The function is intentionally public because the recipient does not have an account. The secret stays server-side.

## 4. Put the function URL into `index.html`

After deployment the URL is:

`https://YOUR_PROJECT_ID.supabase.co/functions/v1/wish-share`

Set:

```js
const SHARE_API_URL='https://YOUR_PROJECT_ID.supabase.co/functions/v1/wish-share';
const SHARE_PUBLIC_KEY='';
```

`SHARE_PUBLIC_KEY` can remain empty with this function configuration.

## 5. What users will get

Example display code:

`SW-ANAYA-A7K4`

Example link:

`https://your-site.example/#wish=Q7k3mA91Zx`

The **link does not put the birthday date or name into the URL**. That is deliberate: a birthday date is personal information, and a random slug gives us a much better privacy boundary while still keeping the link tiny.

The share code contains a short name prefix because it is convenient for the sender to recognise, but it is not the secret that protects the wish.

## 6. Important limitation

The ZIP can contain all code and setup files, but no assistant can make the final public links work until the site is connected to a real Supabase project and deployed. The project URL is unique to your account, and the database must actually exist.

Once the project is connected, **Create a Wish** creates a database row, returns a unique short slug/code, and the recipient route fetches that row. The existing offline format remains as a fallback for local testing.
