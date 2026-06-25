# Cloudflare Images migration plan

## Goal
Move every marketing image out of this public repo and serve it from Cloudflare Images, then update every `studio.video` reference.

## Asset inventory

| File | Old jsDelivr / raw URL (example) | New Cloudflare Images URL | Status |
|------|----------------------------------|---------------------------|--------|
| `audience-v2.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/audience-v2.png` | TBD | not migrated |
| `hero-meeting.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/hero-meeting.png` | TBD | not migrated |
| `logo-record.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/logo-record.png` | TBD | not migrated |
| `team/face-1.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/team/face-1.png` | TBD | not migrated |
| `team/face-2.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/team/face-2.png` | TBD | not migrated |
| `team/face-3.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/team/face-3.png` | TBD | not migrated |
| `team/face-4.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/team/face-4.png` | TBD | not migrated |
| `team/face-5.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/team/face-5.png` | TBD | not migrated |
| `trust/be-mobile.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/be-mobile.png` | TBD | not migrated |
| `trust/dreambody-club.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/dreambody-club.png` | TBD | not migrated |
| `trust/dsc.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/dsc.png` | TBD | not migrated |
| `trust/genuine-shift.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/genuine-shift.png` | TBD | not migrated |
| `trust/gkr-karate.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/gkr-karate.png` | TBD | not migrated |
| `trust/launchpad.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/launchpad.png` | TBD | not migrated |
| `trust/lifemap.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/lifemap.png` | TBD | not migrated |
| `trust/motivation.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/motivation.png` | TBD | not migrated |
| `trust/speech-time-fun.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/speech-time-fun.png` | TBD | not migrated |
| `trust/time-rich-recruiter.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/trust/time-rich-recruiter.png` | TBD | not migrated |
| `waiting-bg.png` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/waiting-bg.png` | TBD | not migrated |
| `webinar-audience.jpg` | `https://cdn.jsdelivr.net/gh/OWNER/studio-video-assets@main/webinar-audience.jpg` | TBD | not migrated |

## Required next steps

1. **Cloudflare Images account / bucket**
   - Confirm the Cloudflare account hash, Images account ID, and bucket name.
2. **Authentication**
   - Provide an API token or service token with Images upload permissions.
3. **Upload**
   - Use the Cloudflare Images API (`POST /accounts/{account_id}/images/v1`) or Direct Creator Upload URLs.
   - Upload all files above (~16 MB total, well within Cloudflare’s per-image limits and moderate rate limits; use reasonable concurrency).
   - Record the returned image IDs / version IDs in this table.
4. **Update consumers**
   - Search every Studio/Workflow OS repo that builds studio.video for strings such as: `cdn.jsdelivr.net`, `github.com/OWNER/studio-video-assets`, `raw.githubusercontent.com/OWNER/studio-video-assets`, or `studio-video-assets`.
   - Replace each with the corresponding Cloudflare Images URL (`https://imagedelivery.net/<account_hash>/<image_id>/<variant>`).
   - Deploy each repo and verify correct rendering on studio.video.
5. **Make this repo private**
   - Use the GitHub repository settings or admin API; this tool cannot change visibility.
   - After privatization, jsDelivr/GitHub raw URLs for these assets will stop working for unauthenticated callers, so all consumers must be migrated first.
