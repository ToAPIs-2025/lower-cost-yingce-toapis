# Yingce: integration scope

完成独立 API 图片生成、首帧上传和视频生成；提供声明式图片插件候选包。尚未运行原生 Go 校验器、插件导入及画布端验收；候选插件尚无宿主内报价门控，视频首帧上传仍需专门映射。

Standalone image and first-frame video calls succeeded. A declarative image plugin candidate is included. Native Go validation, import, canvas execution and host-side price gating remain unverified; video upload mapping is not implemented in the manifest.

## Contract

- HTTPS origin: `https://toapis.com`, Bearer API Key; no key forwarded to assets.
- Price: `GET /v1/pricing?model=...&type=image|video`, match every catalog condition; no quote means stop.
- Create: `POST /v1/images/generations` or `/v1/videos/generations`; persist submission state before POST and ID immediately afterward.
- Poll existing ID only; `in_progress` is running; `completed` is success; failed/cancelled/expired stop.
- Result: `result.data[0].url`; validate actual image/MP4 bytes.
- Cost: only settled billing is actual; a missing image bill is not zero.

## Native work remaining

`backend/internal/protocol/manifest.go`, `manifest_request.go`, `manifest_adapter.go`: review the candidate manifest, validate with native Go loader, import into an isolated installation, verify async status/result paths and cost approval. No native validator pass is claimed. Candidate excludes reference images; video first-frame upload needs a separate adapter. Before native use, run quote checks externally; host-native budget/settlement integration is still needed.

## Acceptance / 待维护者确认

Target app version and supported model presets; existing supplier/referral ownership; key storage and deployment proxy policy; quote/approval display; create/poll/result/import; refresh/restart resumes same task; actual billing and error handling. Supply test credits by agreement, with no guaranteed quota, SLA or acceptance deadline.
