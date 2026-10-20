# Validation boundary

- Start the loopback bridge on the same self-hosted server. Configure a custom channel at http://127.0.0.1:8769/v1 with the separate bridge token.
- For each image model copy the matching text-to-image group fields from integration/novanova-custom-image-groups.json. The wrapper is documentation, not a claimed import endpoint.
- CustomProviderAdapter only polls VIDEO tasks in the pinned code; the bridge waits for ToAPIs image completion and returns the expected data[0].url synchronously.
- The native references placeholder is an array, while each ToAPIs image_with_roles item needs a scalar URL. The native poller also needs explicit terminal-status handling. integration/novanova-video-plan.json records both gaps instead of offering a broken paste-ready template.
- The Spring/Java app, channel persistence, media registration and complete image/video UI workflows remain unverified.

No full upstream UI acceptance, native video/reference editing acceptance or audio acceptance is claimed. Check cases.json for API output and billing evidence.
