# ApplicantScout

Personal-tool WoW addon — emits M+ applicant data to `/chatlog` for an external Python companion that displays Warcraft Logs N/H/M/M+ percentiles per applicant.

This addon by itself does nothing user-visible — it's the data-source half of a two-component setup.

## Usage

1. Enable WoW chat logging once: `/chatlog`
2. Create your M+ key listing as usual.
3. Run the companion process (`applicant-scout-companion`).

## Slash commands

```
/apscout on / off      enable or disable emission
/apscout status        show current state, applicant count, /chatlog status
/apscout test          emit a fake applicant + listing for flush verification
/apscout reset         clear diff cache and re-emit current applicants
/apscout flush         force /chatlog to flush via LoggingChat toggle
```

## Emission format

All lines start with `[APSCOUT|` so the companion can grep them out of mixed chat.

| Tag | When | Payload |
|---|---|---|
| `[APSCOUT\|VERSION]` | once per login | `version\|gameVersion\|region\|playerName-realm` |
| `[APSCOUT\|LISTING]` | own listing changes | `activityID\|dungeonName\|listingName\|comment` |
| `[APSCOUT\|NOLISTING]` | own listing closed | (empty) |
| `[APSCOUT\|APP\|+]` | new applicant | `id\|name\|class\|specID\|ilvl\|score\|role` |
| `[APSCOUT\|APP\|=]` | applicant fields changed | (same shape as `+`) |
| `[APSCOUT\|APP\|-]` | applicant left queue | `id` |
| `[APSCOUT\|EMPTY]` | applicant set is empty | (empty) |

## License

MIT
