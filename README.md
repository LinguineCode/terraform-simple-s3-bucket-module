# terraform-simple-s3-bucket-module

## Example Usage

```terraform
module "terraform-simple-s3-bucket-module" {
  source = "github.com/solsglasses/terraform-simple-s3-bucket-module.git"

  bucket_prefix = "foo"
  logging = {
    target_bucket = aws_s3_bucket.logs.id
    target_prefix = "log/"
  }
  versioning = {
    enabled = true
  }
  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
}

resource "aws_s3_bucket" "logs" {
  acl = "log-delivery-write"
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| acl | (Optional) The canned ACL to apply. Defaults to 'private'. Conflicts with `grant` | `string` | `"private"` | no |
| bucket\_prefix | (Optional, Forces new resource) Creates a unique bucket name beginning with the specified prefix. Conflicts with bucket. | `string` | `null` | no |
| logging | Map containing access bucket logging configuration. | `map(string)` | `{}` | no |
| server\_side\_encryption\_configuration | Map containing server-side encryption configuration. | `any` | `{}` | no |
| tags | (Optional) A mapping of tags to assign to the bucket. | `map(string)` | `{}` | no |
| versioning | Map containing versioning configuration. | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | The ARN of the bucket. Will be of format arn:aws:s3:::bucketname. |
| id | The name of the bucket. |
| region | The AWS region this bucket resides in. |


## Testing

See [buildspec.yaml](buildspec.yaml)

## Requirements

  - [x] The module must implement KMS encryption.
  - [x] The module must consider the S3 logging, tags, and versioning
  - [x] Tests to test your module
  - [x] Well documented inputs and outputs.
  - [x] Provide instructions on how to build and use the module

