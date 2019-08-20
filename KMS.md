# KMS Notes

### KMS - Key Management Service

Control encryption keys

### Notes

- Setup 2 users, one to manage the keys, but cannot encrypt/decrypt. The other user can encrypt/decrypt but not manage the keys.

### AWS CLI

- aws kms [encrypt](https://docs.aws.amazon.com/cli/latest/reference/kms/encrypt.html)
- aws kms [decrypt](https://docs.aws.amazon.com/cli/latest/reference/kms/decrypt.html)
- aws kms [re-encrypt](https://docs.aws.amazon.com/cli/latest/reference/kms/re-encrypt.html)
- aws kms [enable-key-rotation](https://docs.aws.amazon.com/cli/latest/reference/kms/enable-key-rotation.html)

### KMS Envelope Encryption

- Encrypt envelope key with a CMK.
- CMK is Customer Master Key
- Keys used in KMS are envelope keys
