# Optimistic updates with TanStack Query (the real app behind the video)

```bash
npm install
npm run dev        # http://localhost:5173
```

The profile picker from the TanStack Query videos, with the edit-city form from the useMutation video. Type a new city
for Alice (Mumbai), press **Save**: with `onMutate` the card says Mumbai at once, before the `PATCH` has even left, because
the mutation writes the expected result straight into the query cache (`setQueryData`) and keeps a snapshot of the old
data. Type **Atlantis** instead: the server refuses it (`500`), `onError` puts the snapshot back, and the card snaps back to
Pune. Either way `onSettled` invalidates the query, so the server's copy is what you end up with. Throttle the network in
DevTools (Slow 3G) to feel the difference between waiting for the server and not.

- `vite.config.js` serves a tiny API from `api/users.json`: `GET /api/users/:id` (Alice is delayed 2 s on purpose,
  everyone else 0.4 s) and `PATCH /api/users/:id` (0.6 s), which merges the JSON body into that user and answers with
  the updated user. A city of `Atlantis` answers `500 "No such city"`. The changes live in memory: restarting the dev
  server puts everyone back (the file is never written).
- `src/main.jsx` creates one `QueryClient` and wraps the app in `QueryClientProvider` (plus `ReactQueryDevtools`).
- `src/versions/` holds each step of the story (see its README). `src/Profile.jsx` is whichever version was copied in
  last (the finished app: `onMutate` + `onError` + `onSettled`).

Sources: [Optimistic updates](https://tanstack.com/query/latest/docs/framework/react/guides/optimistic-updates) ·
[Mutations](https://tanstack.com/query/latest/docs/framework/react/guides/mutations) ·
[Query cancellation](https://tanstack.com/query/latest/docs/framework/react/guides/query-cancellation)
