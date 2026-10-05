# Versions

Each file here is one step of the story. The video's code panels read these files, and
`../../../capture.mjs` copies each one into `src/Profile.jsx` before capturing (on a fresh dev server each time,
so Alice is back in Pune), the way you'd edit and save the real file. Edit a version here, then re-run the capture.

| File | Shown in beats |
|---|---|
| `Profile.mutation-invalidate.jsx` | hook.last … hook.staring, optimistic.fn: the useMutation video's finished `Profile.jsx` (`onSuccess` awaits `invalidateQueries`), unchanged: the "before" |
| `Profile.optimistic.jsx` | optimistic.*, rollback.atlantis … rollback.lying: adds `onMutate` (`cancelQueries`, `getQueryData`, `setQueryData`, returns the snapshot). No rollback yet: after a failed save the card keeps the stand-in |
| `Profile.optimistic-rollback.jsx` | rollback.onerror … rollback.yourself: adds `onError`, which puts `onMutateResult.previous` back on the shelf |
| `Profile.optimistic-settled.jsx` | settled.*: `onSuccess` becomes `onSettled`, so the invalidation runs after a failure too (the finished app) |

The server (`vite.config.js`) refuses one city, `Atlantis`, with `500 "No such city"`, so the failed save is real.
