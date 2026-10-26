# Physical verification records

This directory stores **one immutable bundle per real-machine verification run**.

## Layout

```text
verification/
  README.md
  runs/
    VERIFY-YYYYMMDDTHHMMSSZ-<random>/
      report.json
      ui-history.log
      error-details.txt
      raw-logs/
        <RawLog-ID>.log
```

## Bundle rules

- Verification-run IDs are independent of RawLog IDs and measurement session numbers.
- Include the timestamped UI/controller/sequence history and the error code/message captured for the run.
- Record firmware/device identity, selected motor instance, recipe/mode, and the exact included RawLog IDs when available.
- Attach only RawLogs explicitly selected for that verification run. Never automatically include every historical RawLog for an instance.
- Copy RawLog bytes/text unchanged; do not rewrite, normalize, or reassign the original RawLog.
- Keep report metadata separate from raw log bodies.
- A failed upload must leave a recoverable local bundle; secrets/tokens must never be included.
- GitHub credentials may be entered in the app's masked token dialog/control; the UI-entered token is kept in memory for that app session only and is not written into the bundle or settings files. `MINI4WD_GITHUB_TOKEN` remains supported as an environment-variable alternative.
- Source/specification changes do not belong in this data directory.

The application must show a preview of the target instance and selected RawLogs and require operator confirmation before upload.
