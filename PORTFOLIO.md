# Portfolio OS for PomoDag (beta)

This is an optional, local-only project portfolio view.

## Deployment
- Review and merge the draft pull request after manual smoke tests.
- Open `https://shmlr.github.io/pomo/portfolio.html` after GitHub Pages updates.
- Import a private portfolio JSON file **locally in your browser**. No project data is committed to GitHub by this feature.
- Choose today's future start time and the repeat mode, then press "В PomoDag" for one project.
- Open the main PomoDag page and verify the added task. Do not assume a task has executed merely because it was added.

## Storage
- Existing PomoDag entries are kept in the unchanged key `pomo_tasks`.
- The dashboard uses its own key `r01_portfolio_v1`.
- Both keys are local to the exact browser origin and device, not synced to Google Drive, other browsers, or devices.
- The portfolio export/import covers **only project records**. It does not back up `pomo_tasks`. Back up the PomoDag task store separately before browser data clearing or migration.

## Compatibility
PomoDag uses `{id,name,start,dur,repeat,lastDone}` for tasks. The dashboard adds the optional `portfolioId` field, ignored by PomoDag. Repeats: `none`, `weekdays`, and new `sixdays` (Mon-Sat). Existing `daily` tasks remain valid in the main PomoDag.

The portfolio checks today's capacity (240 minutes), today's time overlaps, Sunday guard, and a conservative buffer around 20:00. It **does not** verify overlaps or capacity for every future recurrence. One-off tasks have no calendar date in PomoDag.

## Smoke tests before merge
1. Open old PomoDag with existing locally stored tasks and record the count.
2. Open portfolio in another tab on the same origin; verify existing tasks are not modified by viewing/filtering/import.
3. Import a private JSON configuration; confirm counts and priorities.
4. Add one test task in the future today. Verify exactly one new item in PomoDag (including if the first tab was already open).
5. Retry the same task and verify duplicate protection.
6. Try overlapping task, >240-minute day, Sunday condition, and 20:00 reserve. Verify rejection.
7. Mark one project as done and export/reimport portfolio.
8. Verify PomoDag alarm, namaz UI, and existing repeats still work, including new Mon-Sat mode.
9. On a second device verify no automatic sync is claimed.
10. Check mobile widths ~390px and 1440px; no horizontal clipping or JS errors.

## Known limitations / separate issues
- No offline queue, cross-device sync, automatic Google Sheets updates or 1C connection.
- Original PomoDag currently has fixed historical prayer-time fallback values when the remote API fails. This is a **separate, safety-relevant issue**: they must not be interpreted as a verified live schedule.
- Main PomoDag does not record the completion history of one-off tasks after automatic removal.
