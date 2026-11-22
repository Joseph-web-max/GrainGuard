# Security Policy

## Reporting

Do not publish live credentials, access tokens, private records or security-sensitive site details in a GitHub issue. Contact the repository maintainer privately with a minimal reproducible report.

## Deployment security

- Never commit Supabase service-role/secret keys, passwords, device Wi-Fi passwords or personal data.
- Keep Supabase RLS enabled and review policies before inviting users.
- The supplied single-user RLS model is not a multi-tenant organisation security design.
- Use HTTPS for device access APIs.
- Do not expose the device outside a controlled environment without a network and physical security review.
- V1 has no fan or actuator control. Do not add it without a separate safety assessment.
- Validate inputs from sensor packets; devices and BLE data are not inherently trusted.
- Do not use the application as the sole basis for food-safety or regulatory decisions.
