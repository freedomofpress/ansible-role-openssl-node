openssl_node
=========

Utilizes a pre-existing CA certificate stored in a variable file to spin-off a
new signed node certificate and copy that over to box.


Requirements
------------

A pre-existing CA certificate keypair must exist in a variable file in the
following format:

```yaml
openssl_node_certificate_authority:
    arbitrary_ca_name:
      pub: >
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
      private: >
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
```

See `defaults/main.yml` for available settings.

License
-------

MIT

