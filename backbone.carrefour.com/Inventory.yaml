apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: inventory.backbone.carrefour.com
spec:
  group: backbone.carrefour.com
  conversion:
    #strategy: None
    strategy: Webhook
    # # webhook is required when strategy is `Webhook` and it configures the webhook endpoint to be called by API server.
    webhook:
    # #   # conversionReviewVersions indicates what ConversionReview versions are understood/preferred by the webhook.
    # #   # The first version in the list understood by the API server is sent to the webhook.
    # #   # The webhook must respond with a ConversionReview object in the same version it received.
      conversionReviewVersions: ["v1"]
      clientConfig:
        service:
          namespace: localhost
          port: 8090
          name: example-conversion-webhook-server
          path: /backbone/convert

  # list of versions supported by this CustomResourceDefinition
  versions:
    - name: v1
      deprecated: true
      deprecationWarning: "backbone.carrefour.com/v1 is deprecated; see http://backbone.c4.com/v1 for instructions to migrate to backbone.carrefour.com/v2 Inventory"
      served: true
      storage: false
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              required:
                - "replicas"
              properties:
                image:
                  type: string
                replicas:
                  description: Number of replicas to be created.
                  type: integer
                  minimum: 1
                  maximum: 3
                  
    - name: v2
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              required:
                - "replicas"
              properties:
                cronSpec:
                  type: string
                image:
                  type: string
                replicas:
                  type: integer
                  minimum: 2
                  maximum: 5
                  
  scope: Namespaced
  names:
    # plural name to be used in the URL: /apis/<group>/<version>/<plural>
    plural: inventory
    # singular name to be used as an alias on the CLI and for display
    singular: inventory
    # kind is normally the CamelCased singular type. Your resource manifests use this.
    kind: Inventory
    listKind: Inventories
    # shortNames allow shorter string to match your resource on the CLI
    shortNames:
    - invb
