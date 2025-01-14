# Webhook

> Since: v1.3

Webhooks are a way to receive notifications. With this `Goreleaser` functionality, you can send events to any server
exposing a webhook.

If your endpoints are not secure, you can use following environment variables to configure them:

- BASIC_AUTH_HEADER_VALUE like `Basic <base64(username:password)>`
- BEARER_TOKEN_HEADER_VALUE like `Bearer <token>`

Add following to your `.goreleaser.yaml` config to enable the webhook functionality:

```yaml
# .goreleaser.yaml
announce:
  webhook:
    # Whether its enabled or not.
    enabled: true

    # Check the certificate of the webhook.
    skip_tls_verify: true

    # Message template to use while publishing.
    #
    # Default: '{{ .ProjectName }} {{ .Tag }} is out! Check it out at {{ .ReleaseURL }}'
    # Templates: allowed
    message_template: '{ "title": "Awesome project {{.Tag}} is out!"}'

    # Content type to use.
    #
    # Default: 'application/json; charset=utf-8'
    content_type: "application/json"

    # Endpoint to send the webhook to.
    endpoint_url: "https://example.com/webhook"
    # Headers to send with the webhook.
    # For example:
    # headers:
    #   Authorization: "Bearer <token>"
    headers:
      User-Agent: "goreleaser"

```

!!! tip
  Learn more about the [name template engine](/customization/templates/).
